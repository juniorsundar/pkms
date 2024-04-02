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
- DOING Deploy simulation and data collection system in local machine
  id:: 65fc53d3-67f7-4f29-891c-c16e8ba9ae0f
  :LOGBOOK:
  CLOCK: [2024-03-27 Wed 22:27:13]
  :END:
	- DONE Complete the data recording node with automatic folder dumping
	  :LOGBOOK:
	  CLOCK: [2024-03-29 Fri 17:13:58]--[2024-04-01 Mon 15:16:17] =>  70:02:19
	  :END:
	- DONE Add auto dumping of whether the mission was completed successfully or failed
	- DONE Create a HTTP server to manage the auto-launch and killing of simulation
	  :LOGBOOK:
	  CLOCK: [2024-04-01 Mon 15:16:22]
	  CLOCK: [2024-04-01 Mon 15:16:24]--[2024-04-02 Tue 14:57:28] =>  23:41:04
	  :END:
		- Since the simulation runs on a separate container this needs to be achieved through a server call
	- DONE Expose the records/bag folder for autodump of rosbags
	  :LOGBOOK:
	  CLOCK: [2024-04-02 Tue 14:57:27]--[2024-04-02 Tue 16:31:20] =>  01:33:53
	  :END:
		- ```bash
		  docker run -it --rm \
		      --network=host -p 14540:14540/udp \
		      --ipc=host --pid=host \
		      --env UID=$(id -u) \
		      --env GID=$(id -g) \
		      -v $(pwd)/records:/ros_workspace/records \
		      px4-ros ros2
		  ```
	- DOING Test full pipeline for robustness for a simple deployment
	  :LOGBOOK:
	  CLOCK: [2024-04-02 Tue 16:31:26]
	  :END:
- TODO Run test batch
	- TODO Obtain a few data sets
	- TODO Actively maintain and improve the rosnodes