- DONE [[Literature review for Data Generation Task]]
- DOING Generate plan of action
  :LOGBOOK:
  CLOCK: [2024-03-20 Wed 16:21:03]
  :END:
	- DONE Figure out how to make a ((65fc12cb-7576-445f-a824-0bce95119dc2))
	  :LOGBOOK:
	  CLOCK: [2024-03-20 Wed 16:35:22]
	  CLOCK: [2024-03-20 Wed 16:35:24]--[2024-03-21 Thu 15:48:01] =>  23:12:37
	  CLOCK: [2024-03-21 Thu 15:48:02]--[2024-03-21 Thu 15:48:02] =>  00:00:00
	  CLOCK: [2024-03-21 Thu 15:48:03]--[2024-03-21 Thu 15:48:04] =>  00:00:01
	  :END:
	- DONE Figure out how to set up ROS in a containerised environment
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
	  :LOGBOOK:
	  CLOCK: [2024-03-22 Fri 16:15:18]--[2024-03-26 Tue 16:15:37] =>  96:00:19
	  :END:
		- **NOTE** that the rate at which data is being recorded is throttled.
	- DOING Formalise a PoA
	  :LOGBOOK:
	  CLOCK: [2024-03-26 Tue 16:16:38]
	  :END:
- TODO Deploy simulation and data collection system in local machine
- TODO Run test batch