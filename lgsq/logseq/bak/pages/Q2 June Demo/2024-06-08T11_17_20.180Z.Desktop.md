# Tasks
	- DONE Which camera is being used for image segmentation
	  collapsed:: true
	  :LOGBOOK:
	  CLOCK: [2024-04-25 Thu 13:29:44]--[2024-04-25 Thu 13:29:45] =>  00:00:01
	  CLOCK: [2024-04-25 Thu 13:29:45]--[2024-05-01 Wed 15:15:09] =>  145:45:24
	  :END:
		- [Luxonis OAK-D S2](https://shop.luxonis.com/products/oak-d-s2?variant=42455432233183) - This has been tested with Release12 and proven to work as front-facing.
		- [SIYI A8 Mini](https://shop.siyi.biz/products/siyi-a8-mini) - This is the model being used in Masdar and in F4F Prague for downward facing gimbal.
	- DONE How is the data being recorded?
	  :LOGBOOK:
	  CLOCK: [2024-04-25 Thu 13:29:54]--[2024-04-25 Thu 14:04:41] =>  00:34:47
	  :END:
		- DONE It is known that the data is being dumped in ROSbags somewhere, how to extract this?
		  collapsed:: true
			- It can be recorded using [`nats-bag`](https://github.com/tiiuae/nats-bag)
			- A laptop or GCS that is in the same NATS network can record the data streamed through NATS.
			- ```bash
			  nats-bag [-s nats://localhost:4222] record [filename]
			  ```
		- DONE Is recording happening continuously or is it to be triggered?
		  collapsed:: true
			- The gimbal stream needs to be activated by opening the stream through `dronsole` UI or running:
			- ```bash
			  nats pub video.cmd.<device-id> '{"subscriber": "id1", "subscribe":true}'
			  ```
	- DONE Confirm if Siyi A8 is supported for Release12
	  collapsed:: true
	  :LOGBOOK:
	  CLOCK: [2024-04-26 Fri 13:37:25]
	  :END:
		- It is supported as as confirmed by the people at F4F
	- DONE Create Slack channel with all concerned parties
	  :LOGBOOK:
	  CLOCK: [2024-04-26 Fri 11:11:52]--[2024-04-26 Fri 11:11:52] =>  00:00:00
	  :END:
	- DONE Fill up the hardware requirements spreadsheet
	  SCHEDULED: <2024-04-26 Fri 12:00>
	  :LOGBOOK:
	  CLOCK: [2024-04-26 Fri 11:11:58]--[2024-04-26 Fri 14:05:10] =>  02:53:12
	  :END:
	- DONE Verify the need for grass patches for the image segmentation demonstration
	- DONE Data collection from testing team follow-up --> Awaiting Tintu's go-ahead
	  collapsed:: true
		- They don't have enough Saluki V3 to go around, so we will have to affix ours on a drone. Furthermore, we will have to use the x500 Holybro.
		- There isn't a set method to attach the Siyi A8 camera to the drone, so we will have to think up some strategy, maybe by trying double tape or something.
	- DONE Get on Solita about getting camera segmentation demo ready
	  id:: b314a9ab-785e-42c9-a642-90a146d98179
	  :LOGBOOK:
	  CLOCK: [2024-05-02 Thu 12:00:17]--[2024-05-02 Thu 12:50:55] =>  00:50:38
	  :END:
		- DONE How is the video to be retrieved? Is there some code in place for this?
		  collapsed:: true
		  :LOGBOOK:
		  CLOCK: [2024-05-02 Thu 12:00:16]--[2024-05-02 Thu 12:50:51] =>  00:50:35
		  CLOCK: [2024-05-02 Thu 12:50:51]--[2024-05-02 Thu 12:50:52] =>  00:00:01
		  :END:
			- Video is going to be retrieved from the NATS channel subscriber.
			- There will be implementation in place to do this.
		- DONE Determine how the plugin for camera segmentation is to be implemented
		  collapsed:: true
		  :LOGBOOK:
		  CLOCK: [2024-05-02 Thu 12:00:17]--[2024-05-02 Thu 12:50:52] =>  00:50:35
		  :END:
			- This will not be implemented as a plugin, since the image-segmentation does not change the state of SRTA based on outputs.
			- The safe-landing container is providing coordinates to the SRTA in order to perform the action if the SRTA plugins so decide or its ordered from the FMO.
	- CANCELLED Verify if this method can be used to record data in the outdoor arena demo -- talk to Jose Segovia --> Planned shift to T-motor M690b
	  id:: 66386c1b-cb4c-4ea2-a161-fd8ffedf4d86
	  :LOGBOOK:
	  CLOCK: [2024-04-25 Thu 14:04:21]--[2024-04-25 Thu 14:04:42] =>  00:00:21
	  CLOCK: [2024-05-14 Tue 13:27:01]
	  :END:
	- DONE Triggering the RTA modules
	  id:: f5c16267-b6ca-4126-be07-13ac7b5dcaed
	  :LOGBOOK:
	  CLOCK: [2024-05-02 Thu 13:51:05]--[2024-05-06 Mon 11:39:34] =>  93:48:29
	  :END:
		- DONE Check first what kind of triggers can be implemented with Solita.
		  collapsed:: true
			- There is a placeholder in place inside SRTA and it is awaiting the UI implementation on the UI/FMO side of the things.
		- CANCELLED Check with Mehmet if something like this needs to be implemented in the software and control scheme for the drone
	- DONE Printing the mounts and attach it to the drone
	  :LOGBOOK:
	  CLOCK: [2024-05-02 Thu 12:40:27]--[2024-05-09 Thu 20:13:04] =>  175:32:37
	  :END:
		- DONE Saluki V3 to Drone Mount
		  :LOGBOOK:
		  CLOCK: [2024-05-02 Thu 15:45:33]--[2024-05-07 Tue 09:30:52] =>  113:45:19
		  :END:
		- DONE Siyi A8 and Battery Mount
		  collapsed:: true
		  :LOGBOOK:
		  CLOCK: [2024-05-02 Thu 15:45:36]--[2024-05-09 Thu 20:13:03] =>  172:27:27
		  :END:
			- ![mounting_siyia8.JPG](../assets/mounting_siyia8_1714639504791_0.JPG)
	- CANCELLED Check if video encoding/decoding is happening on the hardware (Siyi A8)
	  id:: c67ddd53-eec8-405d-bd77-4ec7a07c120d
	- DONE Mount Saluki V3 to the ~~Holybro-X500~~ T-Motor M690b Drone and get it airborne
	  id:: 66386c1b-1e6c-4481-b1f3-08b18d2a9fc6
	  :LOGBOOK:
	  CLOCK: [2024-05-09 Thu 20:13:13]--[2024-05-23 Thu 23:57:18] =>  339:44:05
	  :END:
		- DONE Obtain Saluki V3
		- DONE Set up Saluki V3 for flight mission
		  :LOGBOOK:
		  CLOCK: [2024-05-10 Fri 17:58:18]--[2024-05-13 Mon 21:27:34] =>  75:29:16
		  :END:
		- DONE Mount Saluki V3 to ~~Holybro~~ T-Motor M690b Drone
		  :LOGBOOK:
		  CLOCK: [2024-05-13 Mon 21:27:30]--[2024-05-23 Thu 23:57:16] =>  242:29:46
		  :END:
			- DONE Printing parts
			  :LOGBOOK:
			  CLOCK: [2024-05-18 Sat 14:57:44]--[2024-05-18 Sat 14:58:12] =>  00:00:28
			  CLOCK: [2024-05-18 Sat 14:58:13]--[2024-05-22 Wed 21:54:14] =>  102:56:01
			  :END:
			- DONE [Set-up Comms Module v1.5](((66488a15-4e2c-4a74-bc4b-f09e167c608c)))
			  :LOGBOOK:
			  CLOCK: [2024-05-18 Sat 14:57:49]--[2024-05-18 Sat 14:58:14] =>  00:00:25
			  CLOCK: [2024-05-18 Sat 14:58:14]--[2024-05-21 Tue 21:48:50] =>  78:50:36
			  :END:
			- DONE Additional components:
			  collapsed:: true
			  :LOGBOOK:
			  CLOCK: [2024-05-22 Wed 21:52:38]
			  CLOCK: [2024-05-22 Wed 21:52:42]--[2024-05-22 Wed 21:54:16] =>  00:01:34
			  CLOCK: [2024-05-22 Wed 21:54:17]--[2024-05-23 Thu 23:57:14] =>  26:02:57
			  :END:
				- Nvidia power cable
				- RF transmitter/receiver
	- DONE Get drone airborne --> [Transferred to Systems Testing Team](((6656d625-f122-480d-9b57-43c5cdc437c9)))
	  id:: 664f9f87-a976-490c-a59c-d068f1698a15
	  :LOGBOOK:
	  CLOCK: [2024-05-27 Mon 20:17:58]--[2024-06-05 Wed 16:31:06] =>  212:13:08
	  :END:
		- DONE Copy over PID tuning parameters
		  :LOGBOOK:
		  CLOCK: [2024-05-27 Mon 20:17:59]--[2024-05-30 Thu 11:29:34] =>  63:11:35
		  :END:
		- DONE Connect with GCS and fly autonomously
		  :LOGBOOK:
		  CLOCK: [2024-05-30 Thu 11:29:36]--[2024-06-05 Wed 16:30:56] =>  149:01:20
		  :END:
	- TODO Demo prerequisites
		- DOING Note down drone configuration and limitations
		  :LOGBOOK:
		  CLOCK: [2024-06-05 Wed 16:30:43]
		  :END:
		- DONE Understand how to fly drone using FMO
		- DONE Understand how to extract data from drone
		  collapsed:: true
			- Can be done through QGC
		- TODO Prepare anomalous flight use-case (appropriate weights and how to add them)
		- TODO Test single anomalous flight use-case
	- DONE Figure out what the process is to install and setup the ((66605142-3ed1-4364-8797-636648594267))
	  id:: 665ff704-5b0e-455b-b730-49c4c89148f6
	  :LOGBOOK:
	  CLOCK: [2024-06-05 Wed 10:02:55]--[2024-06-05 Wed 16:17:59] =>  06:15:04
	  :END:
	- DOING Soft deadline to get drone working with SRTA module
	  SCHEDULED: <2024-06-13 Thu>
	  :LOGBOOK:
	  CLOCK: [2024-06-05 Wed 22:25:01]
	  :END:
	- DOING Freeze code and model
	  SCHEDULED: <2024-06-30 Sun>
	  id:: 6644991b-cbe7-4882-9761-382fc01aeb4c
	  :LOGBOOK:
	  CLOCK: [2024-05-15 Wed 15:17:19]--[2024-06-04 Tue 21:12:53] =>  485:55:34
	  CLOCK: [2024-06-04 Tue 21:12:53]
	  :END:
	- TODO Demo
	  id:: 664499d6-f73c-49a9-bd7c-6d2ddd36eb87
	  SCHEDULED: <2024-07-01 Mon>
- # Notes
	- Task changes because it was possible to receive a T-Motor M690b assigned for SRTA Team
	  collapsed:: true
		- ((66386c1b-cb4c-4ea2-a161-fd8ffedf4d86))
		- ((66386c1b-1e6c-4481-b1f3-08b18d2a9fc6))
	- Why go for the T-Motor drone over the Holybro?
	  collapsed:: true
		- Final deployment is with T-Motor drone swarms.
		- If it is possible for F4F to repeat and replicate non-normal flight test cases, then it can be replicated in Masdar for testing. This will save chances of drone being wrecked here.
		- If F4F does not have Holybro procured, then lead time to data collection is uncertain.
	- Important points when setting up Comms Module v1.5:
	  id:: 66488a15-4e2c-4a74-bc4b-f09e167c608c
	  collapsed:: true
		- To boot the Raspberry Pi device as USB: [raspberrypi/usbboot](https://github.com/raspberrypi/usbboot)
		- To flash custom image into the Pi, use `sudo rpi-imager`
			- Install with `sudo apt install rpi-imager`
			- `sudo` is important because otherwise the `/dev/sdX` cannot be accessible for writing disk image
		- Check if two communications modules are in the same channel with `iw dev` command. If they are not in the same then there will be a communication issue.
- # Custom Release for SRTA
  id:: 66605142-3ed1-4364-8797-636648594267
	- **Junior from SRTA team**: New fog-system deployment on SalukiV3
	  collapsed:: true
		- Deploying GPU-enabled features, currently on release 12.0.1.
		- Asked about compatibility with existing FPGA, FC versions, etc.
	- **Manuel's Response**: Compatibility confirmed with caveats
	  collapsed:: true
		- Confirmed compatibility but mentioned possible surprises due to the demo branch.
		- Provided link to the specific branch used for testing: [feature/gpu-passthrough](https://github.com/tiiuae/fog_system/commits/feature/gpu-passthrough/)
	- **Junior's Steps for Deployment**: Creating bootable USB and installing fog-system
	  collapsed:: true
		- **Commands**:
		  ```bash
		  sudo fog update feature/gpu-passthrough
		  sudo fog installer create-media --site=uae --profile=nvidia-nx --confirm /dev/sda
		  ```
		- **Process**: Install fog-system on Saluki V3L, connect to internet, and pull required containers.
	- **Manuel's Confirmation**: Steps are correct
	  collapsed:: true
		- Affirmed the steps provided by Junior and confirmed they should suffice.
	- **FC and LMC Clarification**: Use of terms and functionality
	  collapsed:: true
		- Discussed use of FC and clarified LMC as Mission Computer.
		- The LMC has been used in another context (Salukiv2 with Flight Controller and Lite Mission Computer). Now it is just MC.
		- Ensured flying capability with the new fog-system installation.
	- **Junior's Final Query**: Support for potential issues
	  collapsed:: true
		- Asked for contact in case of issues during deployment.
	- **Manuel's Assurance**: Setup should work, provided support guidance
	  collapsed:: true
		- Confirmed that the setup should be functional and offered support.