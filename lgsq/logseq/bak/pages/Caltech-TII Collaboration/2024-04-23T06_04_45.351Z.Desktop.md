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
- DOING [Second meeting](((66214ed0-8de1-4d80-aa69-b65f4e3be402)))
  :LOGBOOK:
  CLOCK: [2024-04-18 Thu 15:52:39]--[2024-04-18 Thu 21:04:48] =>  05:12:09
  :END:
	- DOING Read [paper]([[Secure State Reconstruction in Differentially Flat Systems Under Sensor Attacks Using Satisfiability Modulo Theory Solving]])
	  id:: 66215121-a83a-4448-9960-9ddf25ef204f
	  :LOGBOOK:
	  CLOCK: [2024-04-18 Thu 21:05:15]--[2024-04-18 Thu 21:05:16] =>  00:00:01
	  CLOCK: [2024-04-18 Thu 21:05:16]--[2024-04-18 Thu 21:05:17] =>  00:00:01
	  CLOCK: [2024-04-18 Thu 21:20:49]
	  :END:
- DOING Third meeting
  :LOGBOOK:
  CLOCK: [2024-04-22 Mon 10:45:06]
  :END:
- ___
- # Instructional
  id:: 660fab83-c0af-4019-8e61-d168f0f8ff42
	- ## Running the SITL Simulation
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
		- The plan of action will be to design a program (either a ROS 2 node or a standalone script) that changes the `SENS_ACCEL_SET` parameter according to a predefined behaviour of the malicious agent.
		- As the agent will have access to the system's internal dynamics, they will also be a node in the ROS 2 network and will subscribe to the necessary topics being published from the PX4 flight controller.