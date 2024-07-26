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
	- DONE Setup drone with BKC 12.1
	  :LOGBOOK:
	  CLOCK: [2024-07-09 Tue 21:12:52]--[2024-07-10 Wed 23:05:06] =>  25:52:14
	  :END:
		- DONE Flash BKC 12.1 to SRTA drone
		  :LOGBOOK:
		  CLOCK: [2024-07-09 Tue 21:12:53]--[2024-07-09 Tue 21:12:53] =>  00:00:00
		  :END:
		- DONE Provision drone and install containers
		  :LOGBOOK:
		  CLOCK: [2024-07-09 Tue 21:12:54]--[2024-07-10 Wed 23:04:44] =>  25:51:50
		  :END:
		- DONE Verify that drone connects to Mesh Network
		  :LOGBOOK:
		  CLOCK: [2024-07-10 Wed 23:04:45]--[2024-07-10 Wed 23:05:05] =>  00:00:20
		  :END:
	- DONE Verify that the PMC, Drone and Mesh Network are functional in tandem
	  :LOGBOOK:
	  CLOCK: [2024-07-10 Wed 23:05:13]--[2024-07-11 Thu 20:35:03] =>  21:29:50
	  :END:
	- DONE Determine if it is possible to have the PMC and Drone functioning without WiFi in Mesh Network
	  :LOGBOOK:
	  CLOCK: [2024-07-15 Mon 20:30:54]--[2024-07-15 Mon 20:30:55] =>  00:00:01
	  CLOCK: [2024-07-15 Mon 20:30:55]--[2024-07-15 Mon 20:30:56] =>  00:00:01
	  :END:
	- DONE Talk to Daniel Smrcka about running PMC + Drone offline
	  id:: 6697f269-3e4a-46f4-9032-15a30ce36e85
	- DONE Flash SRTA-module inclusive release into the drone Saluki v3
	  :LOGBOOK:
	  CLOCK: [2024-07-15 Mon 20:32:02]--[2024-07-26 Fri 13:41:42] =>  257:09:40
	  :END:
	- DONE Run some test flights with the drone
	  :LOGBOOK:
	  CLOCK: [2024-07-24 Wed 14:16:54]--[2024-07-24 Wed 14:16:56] =>  00:00:02
	  :END:
	- DOING Things to Change in [SRTA Release](https://github.com/tiiuae/fog_system/tree/12.1-gpu-srta)
	  :LOGBOOK:
	  CLOCK: [2024-07-26 Fri 13:42:11]
	  :END:
		- DONE Change `path-worker` reference
		  collapsed:: true
		  :LOGBOOK:
		  CLOCK: [2024-07-26 Fri 13:43:20]--[2024-07-26 Fri 13:43:29] =>  00:00:09
		  :END:
			- ```bash
			  fog manifest update-component path-worker --image ghcr.io/tiiuae/tii-path-worker:sha-8bf623b --things-will-break
			  ```
		- DOING Install with `sros=true` but change it to `false` after setup
		  :LOGBOOK:
		  CLOCK: [2024-07-26 Fri 13:43:21]
		  :END:
		- DONE Change `tii-ml-rta-anomaly-detection` container reference --> `sha-c5d75d2`
		  :LOGBOOK:
		  CLOCK: [2024-07-26 Fri 13:43:22]--[2024-07-26 Fri 13:43:28] =>  00:00:06
		  :END:
		- DONE Remove `gpu=all`
		  :LOGBOOK:
		  CLOCK: [2024-07-26 Fri 13:43:23]--[2024-07-26 Fri 13:43:23] =>  00:00:00
		  CLOCK: [2024-07-26 Fri 13:43:24]--[2024-07-26 Fri 13:43:25] =>  00:00:01
		  :END:
	- TODO Test fly drone with the non-GPU anomaly detection release
	- TODO Conduct experiments with weights-attached