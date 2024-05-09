- DONE [First meeting](((660f9803-86fb-4d27-8592-f471e3712eba)))
  :LOGBOOK:
  CLOCK: [2024-04-04 Thu 23:11:09]--[2024-04-15 Mon 13:16:47] =>  254:05:38
  :END:
	- DONE Follow up with [instructional](((660fab83-c0af-4019-8e61-d168f0f8ff42))) response
	- DONE Read [[Safety of Linear Systems under Severe Sensor Attacks]]
	  :LOGBOOK:
	  CLOCK: [2024-04-04 Thu 23:06:46]--[2024-04-15 Mon 13:15:11] =>  254:08:25
	  :END:
- DONE Prepare a small demonstration for second meeting
  :LOGBOOK:
  CLOCK: [2024-04-04 Thu 23:05:41]--[2024-04-04 Thu 23:06:44] =>  00:01:03
  CLOCK: [2024-04-04 Thu 23:11:07]--[2024-04-04 Thu 23:11:07] =>  00:00:00
  CLOCK: [2024-04-15 Mon 13:16:47]--[2024-04-17 Wed 15:58:33] =>  50:41:46
  :END:
	- DONE Split the directed attacks to the accelerometer for x, y and z-axis
	  :LOGBOOK:
	  CLOCK: [2024-04-15 Mon 13:18:10]--[2024-04-15 Mon 16:03:38] =>  02:45:28
	  :END:
	- DONE Create a node spinner that can induce a targeted attack on these axes
	  :LOGBOOK:
	  CLOCK: [2024-04-15 Mon 16:03:36]--[2024-04-16 Tue 14:31:10] =>  22:27:34
	  :END:
	- DONE Create a visualisation that captures this behaviour
	  :LOGBOOK:
	  CLOCK: [2024-04-16 Tue 14:31:08]--[2024-04-17 Wed 15:58:32] =>  25:27:24
	  :END:
- DONE [Second meeting](((66214ed0-8de1-4d80-aa69-b65f4e3be402)))
  :LOGBOOK:
  CLOCK: [2024-04-18 Thu 15:52:39]--[2024-04-18 Thu 21:04:48] =>  05:12:09
  :END:
	- DONE Read [paper]([[Secure State Reconstruction in Differentially Flat Systems Under Sensor Attacks Using Satisfiability Modulo Theory Solving]])
	  id:: 66215121-a83a-4448-9960-9ddf25ef204f
	  :LOGBOOK:
	  CLOCK: [2024-04-18 Thu 21:05:15]--[2024-04-18 Thu 21:05:16] =>  00:00:01
	  CLOCK: [2024-04-18 Thu 21:05:16]--[2024-04-18 Thu 21:05:17] =>  00:00:01
	  CLOCK: [2024-04-18 Thu 21:20:49]--[2024-04-23 Tue 11:55:09] =>  110:34:20
	  :END:
- DONE [Third meeting](((66260755-1d06-44fc-a270-ca1cbec2c0e2)))
  :LOGBOOK:
  CLOCK: [2024-04-22 Mon 10:45:06]--[2024-04-22 Mon 23:57:52] =>  13:12:46
  :END:
- DONE Implement simple data extraction and injection module as an external ROS Node
  id:: 6626c020-2327-420e-b629-822e1cb565d4
  :LOGBOOK:
  CLOCK: [2024-04-23 Tue 11:55:14]--[2024-04-30 Tue 20:59:57] =>  177:04:43
  :END:
	- DONE Research into how the data pipeline is arranged in the flight controller
	  :LOGBOOK:
	  CLOCK: [2024-04-23 Tue 11:55:13]--[2024-04-26 Fri 10:17:44] =>  70:22:31
	  :END:
	- DONE Research existing strategies to achieve the data interception and injection
	  collapsed:: true
	  :LOGBOOK:
	  CLOCK: [2024-04-26 Fri 10:17:47]--[2024-04-30 Tue 15:17:32] =>  100:59:45
	  :END:
		- [[PX4 - Controls]]
	- DONE Test implementation
	  collapsed:: true
	  :LOGBOOK:
	  CLOCK: [2024-04-30 Tue 15:18:31]--[2024-04-30 Tue 15:18:33] =>  00:00:02
	  :END:
		- ((6630d364-3fd7-43f5-9124-1a4b07efaad2))
- DONE [Fourth meeting](((66386c1a-c19b-46a9-b6ed-2469fe003da8)))
- DONE Verify and validate if the position obtained from the FC's EKF is the same as the actual position of the drone in the simulation environment
  id:: 6633c7e4-1bb7-4a2a-87c6-1d85b1034088
  :LOGBOOK:
  CLOCK: [2024-05-06 Mon 09:36:05]--[2024-05-06 Mon 14:22:28] =>  04:46:23
  :END:
- DONE [Fifth meeting](((66392067-cc32-4121-922f-0f072aa546e2)))
- TODO Look up MATLAB Cell
  id:: 663923ce-a39f-45de-b997-6c7b0cdc97c9
- TODO Try out state reconstruction method with simple example
  id:: 6639243a-3acc-4468-a10d-594e60b555ef
- ___
- # Instructional
  id:: 660fab83-c0af-4019-8e61-d168f0f8ff42
  collapsed:: true
	- ## Running the SITL Simulation
	  collapsed:: true
		- First pull the repository with the faulty controller implementation.
		- ```bash
		  git clone --recursive https://www.github.com/tiiuae/px4-firmware.git -b faulty-controller
		  cd px4-firmware
		  # To make life simpler, export the `FIRMWARE_DIR`
		  # variable so that the simulation can then be launched from anywhere
		  echo export FIRMWARE_DIR=$(pwd) > ~/.bashrc
		  source ~/.bashrc
		  ```
		- We can run this simulation in a container, but first we need to pull the appropriate docker image:
		- ```bash
		  docker pull px4io/px4-dev-simulation-jammy:latest
		  ```
		- The simulation can be launched with the following command:
		- ```bash
		  # Run once to ensure that any remote client (like the container)
		  # to connect to the X Server. Essentially allows you to run GUI
		  # apps launched in the container to be forwarded to your local system
		  xhost +
		  
		  # This command serves multiple purposes
		  # We mount the firmware root directory into the container to build the SITL environment
		  # We forward the X11 server so that the Gazebo simulator GUI runs on local machine
		  # We set network=host so that we can alter subscribe to the rostopics through the DDS
		  docker run -it --privileged --rm \
		    -v ${FIRMWARE_DIR}:/home/user/Firmware:rw \
		    -v /tmp/.X11-unix:/tmp/.X11-unix:ro \
		    -e DISPLAY=${DISPLAY} \
		    -e LOCAL_USER_ID="$(id -u)" \
		    -w /home/user/Firmware \
		    --network=host  \
		    --name=container_name px4io/px4-dev-simulation-jammy \
		    make px4_sitl gz_x500
		  ```
	- ## Injecting Faults in Accelerometer
	  collapsed:: true
		- The implementation has the fault injection features built in. In order to inject targeted and specific faults to accelerator sensor modules, you can type the following commands in the MAVLink console running within the same terminal where the SITL simulation is active.
		- ```bash
		  param set SENS_ACCEL_FAULT 1
		  param set SENS_ACCEL_SET <Any Float Value>
		  ```
		- The first command exposes the fault interface within the firmware, and the second command sets the Accelerometer x, y, and z values to the float value provided.
		- **Note:** Before closing the simulator make sure to revert the values:
		- ```bash
		  param set SENS_ACCEL_SET 0
		  param set SENS_ACCEL_FAULT 0
		  ```
	- ## Imitating an attack
	  collapsed:: true
		- The plan of action will be to design a program (either a ROS 2 node or a standalone script) that changes the `SENS_ACCEL_SET` parameter according to a predefined behaviour of the malicious agent.
		- As the agent will have access to the system's internal dynamics, they will also be a node in the ROS 2 network and will subscribe to the necessary topics being published from the PX4 flight controller.
- # ROS 2 Modular Control
  id:: 6630d364-3fd7-43f5-9124-1a4b07efaad2
  collapsed:: true
	- There are three ROS 2 nodes:
		- **EKF**
			- ![ekf.png](../assets/ekf_1714475976448_0.png)
			- Subscribes to the `vehicle_local_position` topic from the Flight Controller.
			- Publishes ground truth (`gt`) and raw copy (`raw`), separately.
		- **Attacker**
			- ![attacker.png](../assets/attacker_1714475981345_0.png)
			- Subscribes to the `raw` position and introduces an attack. In this case it can be a simple halving operation.
			- ```cpp
			  void Attacker::attack(VehicleLocalPosition& copy)
			  {
			      if (attack_flag)
			      {
			          copy.x /= 2;
			          copy.y /= 2;
			          copy.z /= 2;
			      } else {
			          copy.x *= 1;
			          copy.y *= 1;
			          copy.z *= 1;
			      }
			  }
			  ```
			- It then publishes an `attacked` version of the `gt`.
		- **Controller**
			- ![controller.png](../assets/controller_1714475986120_0.png)
			- Uses the `attacked` and `gt` versions of `vehicle_local_position` to generate a controller input.
			- In this example, we are using a velocity controller - it can also accommodate acceleration controls.
			- Basic averaging operation is used to merge the `gt` with the `attacked` EKF outputs.
			- ```cpp
			  VehicleLocalPosition reference;
			  this->state_merger(reference); // <-- Standard averaging
			  
			  vx = coordinates[target][0] - reference.x;
			  vy = coordinates[target][1] - reference.y;
			  vz = coordinates[target][2] - reference.z;
			  
			  if (abs(vx) > 5)
			  {
			  	  vx = vx / abs(vx) * 5; // Input in x
			  }
			  if (abs(vy) > 5)
			  {
			  	  vy = vy / abs(vy) * 5; // Input in y
			  }
			  if (abs(vz) > 5)
			  {
			  	  vz = vz / abs(vz) * 5; // Input in z
			  }
			  
			  float vxs = vx * vx;
			  float vys = vy * vy;
			  float vzs = vz * vz;
			  float separation = (float)sqrt(vxs + vys + vzs);
			  
			  if (separation < threshold)
			  {
			      target++;
			      if (target > (int)coordinates.size() - 1)
			      {
			        	target = 0;
			      }
			  }
			  
			  // offboard_control_mode needs to be paired with trajectory_setpoint
			  publish_offboard_control_mode();
			  publish_trajectory_setpoint();
			  ```
	- The mission is square periodic.
	- The attack is introduced at a random time point. The results while observing the ground truth are shown below:
	- ![results.png](../assets/results_1714476410791_0.png)