# Tasks
	- DONE [#A] Set up GCS/PMC for drone control
	  id:: 667c02ba-ca15-453c-a243-7e72e9607b6c
	  :LOGBOOK:
	  CLOCK: [2024-06-28 Fri 16:12:07]--[2024-07-04 Thu 21:55:27] =>  149:43:20
	  :END:
		- CANCELLED Setting up GS and Fog
		  :LOGBOOK:
		  CLOCK: [2024-06-28 Fri 16:12:12]
		  CLOCK: [2024-06-28 Fri 16:12:13]
		  :END:
			- DONE Get documentation to set it up
			- DONE Source a second upXtreme device for fog/groundstation role
			- DONE Set up GS role
			  id:: 66807b04-9602-446a-8263-d03791bd6807
			  :LOGBOOK:
			  CLOCK: [2024-07-02 Tue 21:59:22]--[2024-07-02 Tue 21:59:25] =>  00:00:03
			  :END:
			- CANCELLED Set up Fog role
			  :LOGBOOK:
			  CLOCK: [2024-07-02 Tue 21:59:26]
			  :END:
		- DONE [[Setting up PMC]]
		  :LOGBOOK:
		  CLOCK: [2024-06-28 Fri 16:16:12]--[2024-07-04 Thu 21:26:44] =>  149:10:32
		  :END:
			- DONE Obtain rugged laptop
			  collapsed:: true
				- ~~18 weeks lead time...~~ --> 2 days XD
			- DONE Set up provisioning network/server
			  id:: 667ea976-f51d-48b8-a787-aaa69a0a1c2b
			  :LOGBOOK:
			  CLOCK: [2024-07-01 Mon 14:09:41]--[2024-07-01 Mon 14:09:43] =>  00:00:02
			  :END:
			- DONE Set up mesh network
			  id:: 66807b04-7d2d-497c-b9d1-03f253c626dc
			  :LOGBOOK:
			  CLOCK: [2024-07-03 Wed 15:10:20]--[2024-07-04 Thu 21:26:37] =>  30:16:17
			  :END:
				- DONE Assemble Comms Module 1.5
				  id:: 6686d2f2-6a19-44ae-907a-6b8cec282251
				  :LOGBOOK:
				  CLOCK: [2024-07-03 Wed 15:10:17]--[2024-07-03 Wed 15:10:17] =>  00:00:00
				  :END:
				- DONE Configure Comms Module to interface with PMC
				  :LOGBOOK:
				  CLOCK: [2024-07-03 Wed 15:10:19]--[2024-07-04 Thu 21:07:50] =>  29:57:31
				  CLOCK: [2024-07-04 Thu 21:07:50]--[2024-07-04 Thu 21:07:51] =>  00:00:01
				  :END:
			- DONE Register PMC to download containers for a more permanent set-up.
	- DONE Setting up Mesh Network
	  :LOGBOOK:
	  CLOCK: [2024-07-09 Tue 21:12:49]--[2024-07-09 Tue 21:12:50] =>  00:00:01
	  :END:
		- DONE Connect Comms Module 1.5 to Internet Router
		  :LOGBOOK:
		  CLOCK: [2024-07-09 Tue 21:12:44]--[2024-07-09 Tue 21:12:45] =>  00:00:01
		  :END:
		- DONE Verify that the PMC connects to the Mesh Network
		  :LOGBOOK:
		  CLOCK: [2024-07-09 Tue 21:12:47]--[2024-07-09 Tue 21:12:48] =>  00:00:01
		  :END:
	- DOING Setup drone with BKC 12.1
	  :LOGBOOK:
	  CLOCK: [2024-07-09 Tue 21:12:52]
	  :END:
		- DONE Flash BKC 12.1 to SRTA drone
		  :LOGBOOK:
		  CLOCK: [2024-07-09 Tue 21:12:53]--[2024-07-09 Tue 21:12:53] =>  00:00:00
		  :END:
		- DOING Provision drone and install containers
		  :LOGBOOK:
		  CLOCK: [2024-07-09 Tue 21:12:54]
		  :END:
		- TODO Verify that drone connects to Mesh Network
	- TODO Verify that the PMC, Drone and Mesh Network are functional