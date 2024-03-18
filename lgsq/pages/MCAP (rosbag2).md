# Installing and setting up `mcap`
	- ## Installing packages
		- You will need the Python package as well as the ROS 2 packages in order to take full advantage of the `mcap` formatted rosbags. Alternatively, `mcap` has packages in other languages as well (C++, Go, etc.) which can be found at their repository: https://github.com/foxglove/mcap?tab=readme-ov-file#developer-quick-start.
		- To install for Python, run:
		- ```bash
		  python3 -m pip install mcap
		  ```
		- Next we need to install the ROS 2 packages to be able to record the bags in `mcap` format as this feature is not available with the standard installation of [[ROS 2]]. So, for this, create a local ROS workspace. Refer [here](((65e9f4fd-8054-4cdb-8175-4a5c51b73616))) for instructions on how to do that.
		- ```bash
		  # Start at ROS Workspace root directory
		   cd src  
		  
		   git clone https://github.com/ros2/test_interface_files.git -b ${ROS_DISTRO}
		   git clone https://github.com/ros2/rcl_interfaces.git -b ${ROS_DISTRO}
		   git clone https://github.com/ros2/rosbag2.git -b ${ROS_DISTRO}
		  
		   cd ..
		  
		   colcon build --allow-overriding action_msgs builtin_interfaces composition_interfaces lifecycle_msgs rcl_interfaces rosbag2 rosgraph_msgs statistics_msgs test_interface_files test_msgs
		   source install/local_setup.bash
		  ```
	- ## Compatibility with `px4_msgs`
		- If you want to record rosbags of topics carrying interfaces from `px4_msgs`, then follow the instructions [here]([[PX4 - ROS 2 Integration]]) to create a ROS workspace with all the required packages for compatibility with the PX4 frameworks.
		- Then, you can clone the above repositories inside the same workspace, and run the `colcon build` command as shown above.
- # Recording data from topic in `.mcap` format
	- ## Using `ros2` CLI
		- This is simple. Run the command after ensuring that the local workspace is sourced. **Note** that if you are listening to `px4_msgs.msg.SensorAccel` as  in this example, you need to have `px4_msgs` topic in the local workspace.
		- ```bash
		  ros2 bag record -s mcap /fmu/out/sensor_accel
		   ```
		- This will dump the bag into a folder with the `.mcap` file and a `metadata.yaml` file that contains metadata about the topic and the messages in it.
	- ## Using a ROS Node (Python)
		- Create a node with the following contents. In this example, we are listening to a topic from the PX4 flight controller that is carrying the acceleromete messages. While the node is active, the topic will be listened to and recorded into a rosbag. When the node is terminated, the folder with a `.mcap` bag will be created with the messages inside it, as well as a `metadata.yaml` file.
		- ```python
		  #!/usr/bin/env python3
		  
		   import time
		  
		   import rclpy
		   from rclpy.node import Node
		   from rclpy.qos import QoSProfile, ReliabilityPolicy, HistoryPolicy, DurabilityPolicy
		   from rclpy.serialization import serialize_message
		   import rosbag2_py
		  
		   from px4_msgs.msg import SensorAccel
		   import yaml
		  
		  
		   class SensorRecorder(Node):
		  
		       def __init__(self) -> None:
		           super().__init__("sensor_recorder")
		  
		           self.qos_profile = QoSProfile(
		               reliability=ReliabilityPolicy.BEST_EFFORT,
		               durability=DurabilityPolicy.TRANSIENT_LOCAL,
		               history=HistoryPolicy.KEEP_LAST,
		               depth=1,
		           )
		           self.offered_qos_profiles = "- history: keep_last\n  depth: 1\n  reliability: best_effort\n  durability: transient_local\n  deadline:\n    sec: 0\n    nsec: 0\n  lifespan:\n    sec: 0\n    nsec: 0\n  liveliness: system_default\n  liveliness_lease_duration:\n    sec: 0\n    nsec: 0\n  avoid_ros_namespace_conventions: false"
		           self.converter_options = rosbag2_py.ConverterOptions("", "")
		          # ====Accelerometer====
		           self.accel_writer = rosbag2_py.SequentialWriter()
		           self.accel_storage_options = rosbag2_py.StorageOptions(uri="sensor_accel", storage_id="mcap")
		           self.accel_writer.open(self.accel_storage_options, self.converter_options)
		           self.accel_topic_info = rosbag2_py.TopicMetadata(
		               name="/fmu/out/sensor_accel",
		               type="px4_msgs/msg/SensorAccel",
		               serialization_format="cdr",
		               offered_qos_profiles=self.offered_qos_profiles,
		           )
		           self.accel_writer.create_topic(self.accel_topic_info)
		           self.accel_subscriber = self.create_subscription(
		               SensorAccel, "/fmu/out/sensor_accel", self._accel_callback, self.qos_profile
		           )
		  
		           self.start_time = time.time()
		  
		       def _accel_callback(self, msg: SensorAccel):
		           self.accel_writer.write(
		               "/fmu/out/sensor_accel",
		               serialize_message(msg),
		               self.get_clock().now().nanoseconds,
		           )
		  
		  
		   def main(args=None) -> None:
		       print("Starting sensor_recorder node...")
		       rclpy.init(args=args)
		  
		       try:
		           sensor_recorder = SensorRecorder()
		           rclpy.spin(sensor_recorder)
		       except KeyboardInterrupt:
		           pass
		       try:
		           rclpy.shutdown()
		       except Exception as e:
		           pass
		  
		  
		   if __name__ == "__main__":
		       main()
		  ```
- # Convert `.mcap` to `.csv`
	- If for some reason, you need to convert the `.mcap` file into a `.csv` file, below you will find an example that does so with `px4_msgs`. You can adapt this snippet for your purposes.
	- ```python
	  #!/usr/bin python3
	  
	  import pandas as pd
	  from mcap_ros2.reader import read_ros2_messages
	  from rosidl_runtime_py import message_to_ordereddict
	  import importlib
	  import os
	  from glob import glob
	  import yaml
	  import px4_msgs.msg
	  
	  def px4_mcap_to_csv(mcap_dir: str, output_csv_filename: str) -> pd.DataFrame:
	  
	      mcap_filename = glob(os.path.join(mcap_dir, "*.mcap"))[0]
	      metadata = glob(os.path.join(mcap_dir, "*.yaml"))[0]
	  
	      with open(metadata, "r") as file:
	          metadata = yaml.safe_load(file)
	  
	      msg_addr = metadata["rosbag2_bagfile_information"]["topics_with_message_count"][0]["topic_metadata"]["type"]
	      msg_addr = msg_addr.split("/")
	  
	      module = importlib.import_module(msg_addr[0])
	      message_package = getattr(module, msg_addr[1])
	      message = getattr(message_package, msg_addr[2])
	  
	      empty_msg_dict = message_to_ordereddict(message())
	      header = ",".join([f"{str(key)}" for key in list(empty_msg_dict.keys())]) + "\n"
	  
	      full_csv = ""
	      try:
	          for msg in read_ros2_messages(mcap_filename):
	              full_csv += ",".join([f"{msg.ros_msg.__getattribute__(key)}" for key in list(empty_msg_dict.keys())]) + "\n"
	  
	          dat = [x.split(",") for x in (header + full_csv).strip("\n").split("\n")]
	          df = pd.DataFrame(dat)
	          df = df.T.set_index(0, drop=True).T
	      except Exception as e:
	          print(f"Message versions probably aren't matching. Confirm if message fields are matching: {e}")
	  
	      output_csv_filename = mcap_dir + output_csv_filename
	      df.to_csv(output_csv_filename, index=False)
	  
	      return df
	  
	  
	  df = px4_mcap_to_csv("./test_bags/sensor_gps/", "my_data.csv")
	  ```