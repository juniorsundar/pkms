# Tasks
	- DONE [[Literature review for Data Generation Task]]
	- DONE Generate plan of action
	  :LOGBOOK:
	  CLOCK: [2024-03-20 Wed 16:21:03]--[2024-03-27 Wed 22:27:29] =>  174:06:26
	  :END:
		- DONE Figure out how to make a ((65fc12cb-7576-445f-a824-0bce95119dc2))
		  :LOGBOOK:
		  CLOCK: [2024-03-20 Wed 16:35:22]
		  CLOCK: [2024-03-20 Wed 16:35:24]--[2024-03-21 Thu 15:48:01] =>  23:12:37
		  CLOCK: [2024-03-21 Thu 15:48:02]--[2024-03-21 Thu 15:48:02] =>  00:00:00
		  CLOCK: [2024-03-21 Thu 15:48:03]--[2024-03-21 Thu 15:48:04] =>  00:00:01
		  :END:
		- DONE Figure out how to set up ROS in a containerised environment
		  collapsed:: true
		  :LOGBOOK:
		  CLOCK: [2024-03-21 Thu 15:47:06]--[2024-03-22 Fri 15:59:28] =>  24:12:22
		  CLOCK: [2024-03-22 Fri 16:00:13]--[2024-03-25 Mon 13:34:05] =>  69:33:52
		  :END:
			- DONE Launch ROS in containerised environment
			  :LOGBOOK:
			  CLOCK: [2024-03-25 Mon 10:17:34]
			  CLOCK: [2024-03-25 Mon 10:17:41]--[2024-03-25 Mon 10:18:37] =>  00:00:56
			  :END:
			- DONE Clone and build ROS 2 workspace into containerised environment
			  :LOGBOOK:
			  CLOCK: [2024-03-25 Mon 10:17:53]
			  CLOCK: [2024-03-25 Mon 10:17:57]--[2024-03-25 Mon 10:18:39] =>  00:00:42
			  :END:
			- DONE Be able to run the ((65fd6a71-d167-47e0-819c-7e3645319411)) as well as launch all the built nodes
			  :LOGBOOK:
			  CLOCK: [2024-03-25 Mon 10:18:17]
			  CLOCK: [2024-03-25 Mon 10:18:20]--[2024-03-25 Mon 10:38:45] =>  00:20:25
			  :END:
			- DONE The `.bag` files need to be obtainable as well
			  collapsed:: true
			  :LOGBOOK:
			  CLOCK: [2024-03-22 Fri 16:00:14]--[2024-03-25 Mon 13:33:54] =>  69:33:40
			  :END:
				- We may need to be able to dump bags in `.mcap` format. So this means that a drive needs to be mounted and exposed when launching the container.
				- ```bash
				  docker run -it --rm \
				      --network=host -p 14540:14540/udp \
				      --ipc=host --pid=host \
				      --env UID=$(id -u) \
				      --env GID=$(id -g) \
				      -v $HOME/rosbags:/ros_workspace/bags \
				  	px4-ros ros2 bag record /parameter_events -s mcap -o ./bags/new
				  ```
		- DONE Install and set up mechanism to convert log files.
		  collapsed:: true
		  :LOGBOOK:
		  CLOCK: [2024-03-22 Fri 16:15:18]--[2024-03-26 Tue 16:15:37] =>  96:00:19
		  :END:
			- **NOTE** that the rate at which data is being recorded is throttled.
		- DONE Formalise a PoA
		  collapsed:: true
		  :LOGBOOK:
		  CLOCK: [2024-03-26 Tue 16:16:38]--[2024-03-27 Wed 22:27:08] =>  30:10:30
		  :END:
			- The goal is to generate data sets that are diverse, and sufficiently large to be able to train and test models.
			- In deployment, the experiment environment must be able to run simulations and record data *ad inifinitum* given a preset list of parameters.
			- The simulation may cycle through a preset list of movement tasks, or it may generate a randomised movement task.
			- The simulation will start and end with each iteration for thorough safety during deployment.
				- Parameters will be cleansed to remove all faults before the simulation is killed.
				- Data will be recorded in bags, and all pertinent topics will be dumped.
				- ULOG file must also be copied over.
				- Fault data must also be copied over (time of injection, type, etc.).
			- To that end, the following prerequisites are important to get fully set up:
				- ROS bags being recorded as `.mcap` files and being dumped somewhere safe.
				- ROS nodes to initiate rosbag records when trigger is received.
				- Mission controller node to handle generating executing missions.
				- Fault handler to trigger and record faults.
				- Drone state monitor that checks if the drone is functioning. If crash, then crash time needs to be recorded.
			- **How to handle when the mission starts and finishes?**
				- This is necessary for segregating the bag files, and also to manage the sequencing for continuous mission records.
				- #+BEGIN_TIP
				  We could use the termination of the mission thread to signify a end of mission.
				  #+END_TIP
				- #+BEGIN_TIP
				  Should we resort to end of mission in all chases? Even if there is a crash?
				  #+END_TIP
			- Mission finishes normally -->
				- run through normal cleanup sequence
				- restart simulation.
			- Drone crashes -->
				- trigger a preempt on the requesting thread
				- run cleanup sequence
				- restart simulation
	- DONE Deploy simulation and data collection system in local machine
	  id:: 65fc53d3-67f7-4f29-891c-c16e8ba9ae0f
	  :LOGBOOK:
	  CLOCK: [2024-03-27 Wed 22:27:13]--[2024-04-04 Thu 16:27:40] =>  186:00:27
	  :END:
		- DONE Complete the data recording node with automatic folder dumping
		  :LOGBOOK:
		  CLOCK: [2024-03-29 Fri 17:13:58]--[2024-04-01 Mon 15:16:17] =>  70:02:19
		  :END:
		- DONE Add auto dumping of whether the mission was completed successfully or failed
		- DONE Create a HTTP server to manage the auto-launch and killing of simulation
		  collapsed:: true
		  :LOGBOOK:
		  CLOCK: [2024-04-01 Mon 15:16:22]
		  CLOCK: [2024-04-01 Mon 15:16:24]--[2024-04-02 Tue 14:57:28] =>  23:41:04
		  :END:
			- Since the simulation runs on a separate container this needs to be achieved through a server call
		- DONE Expose the records/bag folder for autodump of rosbags
		  collapsed:: true
		  :LOGBOOK:
		  CLOCK: [2024-04-02 Tue 14:57:27]--[2024-04-02 Tue 16:31:20] =>  01:33:53
		  :END:
			- ```bash
			  docker run -it --rm \
			      --network=host -p 14540:14540/udp \
			      --ipc=host --pid=host \
			      --env UID=$(id -u) \
			      --env GID=$(id -g) \
			      -v $HOME/records:/ros_workspace/records \
			      px4-ros ros2
			  ```
		- DONE Test full pipeline for robustness for a simple deployment
		  :LOGBOOK:
		  CLOCK: [2024-04-02 Tue 16:31:26]--[2024-04-04 Thu 16:27:01] =>  47:55:35
		  :END:
	- DONE Deploy to container registry
		- DONE Test once and observe if it is allowed
		  :LOGBOOK:
		  CLOCK: [2024-04-04 Thu 10:36:58]
		  CLOCK: [2024-04-04 Thu 10:37:05]
		  :END:
		- CANCELLED Set up GitHub Actions to do this automatically
		  :LOGBOOK:
		  CLOCK: [2024-04-04 Thu 16:27:27]
		  :END:
	- DONE Run test batch
	  :LOGBOOK:
	  CLOCK: [2024-04-04 Thu 16:27:37]--[2024-05-06 Mon 15:04:45] =>  766:37:08
	  :END:
		- DONE Obtain a few data sets with short time-frame large fault injection
		  :LOGBOOK:
		  CLOCK: [2024-04-04 Thu 16:27:35]--[2024-05-06 Mon 15:04:34] =>  766:36:59
		  CLOCK: [2024-05-06 Mon 15:04:35]--[2024-05-06 Mon 15:04:36] =>  00:00:01
		  :END:
		- DONE Create a convenient `.mcap` converter script
		  collapsed:: true
		  :LOGBOOK:
		  CLOCK: [2024-04-05 Fri 10:22:55]
		  CLOCK: [2024-04-05 Fri 10:22:59]--[2024-04-18 Thu 15:52:35] =>  317:29:36
		  :END:
			- ```python
			  #!/usr/bin python3
			  
			  import argparse
			  import pandas as pd
			  import os
			  import px4_msgs.msg
			  from mcap_ros2.reader import read_ros2_messages
			  from rosidl_runtime_py import message_to_ordereddict
			  import importlib
			  from glob import glob
			  import yaml
			  
			  def px4_mcap_to_csv(mcap_dir: str) -> None:
			      """
			      Convert PX4 MCAP files to CSV format.
			  
			      Args:
			          mcap_dir (str): Path to the directory containing MCAP directories.
			  
			      Raises:
			          FileNotFoundError: If no MCAP files are found in the specified directory.
			      """
			      df = pd.DataFrame()
			      
			      try:
			          mcap_filename = glob(os.path.join(mcap_dir, "*.mcap"))[0]
			          metadata = glob(os.path.join(mcap_dir, "*.yaml"))[0]
			      except IndexError:
			          print(f"No MCAP files found in {mcap_dir}")
			          return
			  
			      with open(metadata, "r") as file:
			          metadata = yaml.safe_load(file)
			  
			      for i in range(len(metadata["rosbag2_bagfile_information"]["topics_with_message_count"])):
			          msg_addr = metadata["rosbag2_bagfile_information"]["topics_with_message_count"][i]["topic_metadata"]["type"]
			  
			          msg_addr = msg_addr.split("/")
			  
			          module = importlib.import_module(msg_addr[0])
			          message_package = getattr(module, msg_addr[1])
			          message = getattr(message_package, msg_addr[2])
			  
			          empty_msg_dict = message_to_ordereddict(message())
			          header = []
			          for sub_key in list(empty_msg_dict.keys()):
			              if sub_key == 'timestamp':
			                  header.append(sub_key)
			              else:
			                  try:
			                      for j in range(len(empty_msg_dict[sub_key])):
			                          header.append(sub_key + f"_{j}")
			                  except TypeError:
			                      header.append(f"{sub_key}")
			          header = ",".join(header) + "\n"
			  
			          full_csv = ""
			  
			          try:
			              for msg in read_ros2_messages(mcap_filename):
			                  try:
			                      current_line = ",".join([f"{msg.ros_msg.__getattribute__(key)}" for key in list(empty_msg_dict.keys())]) + "\n"
			                      current_line = current_line.replace("[", "")
			                      current_line = current_line.replace("]", "")
			                      current_line = current_line.replace(", ", ",")
			                      full_csv += current_line
			                  except:
			                      continue
			  
			              dat = [x.split(",") for x in (header + full_csv).strip("\n").split("\n")]
			              df = pd.DataFrame(dat)
			              df = df.T.set_index(0, drop=True).T
			          except Exception as e:
			              print(f"Message versions probably aren't matching. Confirm if message fields are matching: {e}")
			  
			          dumpfile = f"{mcap_dir}{msg_addr[2]}.csv"
			          df.to_csv(dumpfile, index=False)
			  
			      return
			  
			  
			  def main():
			      parser = argparse.ArgumentParser(description="Convert PX4 MCAP files to CSV")
			      parser.add_argument("directory", help="Path to the directory containing all MCAP folders")
			  
			      args = parser.parse_args()
			  
			      mcap_dir = args.directory
			  
			      dir = os.listdir(mcap_dir)
			      for entry in dir:
			          is_dir = os.path.isdir(f"{mcap_dir}/{entry}")
			          if is_dir:
			              px4_mcap_to_csv(f"{mcap_dir}/{entry}/")
			  
			  
			  if __name__ == "__main__":
			      main()
			  ```
		- DONE Actively maintain and improve the rosnodes
		  :LOGBOOK:
		  CLOCK: [2024-04-04 Thu 16:27:36]--[2024-05-06 Mon 15:04:44] =>  766:37:08
		  :END:
	- DONE Organisation/Packaging of datasets
	  :LOGBOOK:
	  CLOCK: [2024-05-06 Mon 15:03:19]
	  CLOCK: [2024-05-06 Mon 15:03:21]
	  CLOCK: [2024-05-06 Mon 15:03:24]--[2024-05-07 Tue 10:53:24] =>  19:50:00
	  :END:
		- DONE Write script to merge `.ulog` files into one `.csv` file
		  :LOGBOOK:
		  CLOCK: [2024-05-06 Mon 15:03:40]--[2024-05-06 Mon 15:05:08] =>  00:01:28
		  :END:
		- DONE Some fixes to the merging process:
		  :LOGBOOK:
		  CLOCK: [2024-05-06 Mon 15:04:01]
		  CLOCK: [2024-05-06 Mon 15:04:11]--[2024-05-07 Tue 10:53:21] =>  19:49:10
		  :END:
			- DONE Sort headers alphabetically after merging
			  :LOGBOOK:
			  CLOCK: [2024-05-06 Mon 15:04:15]--[2024-05-07 Tue 10:53:14] =>  19:48:59
			  :END:
			- DONE Change `label` header --> `filename`
			  :LOGBOOK:
			  CLOCK: [2024-05-07 Tue 10:53:16]--[2024-05-07 Tue 10:53:17] =>  00:00:01
			  :END:
	- DOING Data collection
	  :LOGBOOK:
	  CLOCK: [2024-05-08 Wed 15:15:19]
	  :END:
		- DOING Hardware datasets
		  :LOGBOOK:
		  CLOCK: [2024-05-08 Wed 15:15:16]
		  :END:
			- DONE Set up meeting with F4F to discuss possibility for anomalous tests
			  id:: 663b5e94-aac1-4c11-91c3-48f6fdf3a1c0
			  :LOGBOOK:
			  CLOCK: [2024-05-08 Wed 15:14:33]--[2024-05-10 Fri 17:56:43] =>  50:42:10
			  :END:
			- DONE Discuss data collection with broken propeller with F4F
			  id:: 663b5eaf-de76-4d72-8f3f-9bd0c64025f2
			  :LOGBOOK:
			  CLOCK: [2024-05-10 Fri 17:56:40]--[2024-05-10 Fri 17:56:42] =>  00:00:02
			  :END:
			- DOING Collect normal and abnormal flight data from F4F
			  :LOGBOOK:
			  CLOCK: [2024-05-10 Fri 17:57:34]
			  :END:
		- DOING Simulation datasets
		  :LOGBOOK:
		  CLOCK: [2024-05-07 Tue 11:02:58]
		  :END:
	- DONE Append the `resample` function into the `ulog_converter.py`
	  :LOGBOOK:
	  CLOCK: [2024-05-09 Thu 20:14:26]
	  CLOCK: [2024-05-09 Thu 20:14:30]--[2024-05-10 Fri 17:59:12] =>  21:44:42
	  CLOCK: [2024-05-10 Fri 17:59:13]--[2024-05-10 Fri 17:59:14] =>  00:00:01
	  :END:
	- TODO Consider numeric suffix for project folder
	  id:: 664498b2-da80-418c-ac4b-49c004bc01cb
- # Notes