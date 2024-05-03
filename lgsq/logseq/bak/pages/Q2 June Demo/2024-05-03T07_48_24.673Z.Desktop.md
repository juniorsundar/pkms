- DONE Which camera is being used for image segmentation
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
		- It can be recorded using [`nats-bag`](https://github.com/tiiuae/nats-bag)
		- A laptop or GCS that is in the same NATS network can record the data streamed through NATS.
		- ```bash
		  nats-bag [-s nats://localhost:4222] record [filename]
		  ```
	- DONE Is recording happening continuously or is it to be triggered?
		- The gimbal stream needs to be activated by opening the stream through `dronsole` UI or running:
		- ```bash
		  nats pub video.cmd.<device-id> '{"subscriber": "id1", "subscribe":true}'
		  ```
- DONE Confirm if Siyi A8 is supported for Release12
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
	- They don't have enough Saluki V3 to go around, so we will have to affix ours on a drone. Furthermore, we will have to use the x500 Holybro.
	- There isn't a set method to attach the Siyi A8 camera to the drone, so we will have to think up some strategy, maybe by trying double tape or something.
- DOING Verify if this method can be used to record data in the outdoor arena demo -- talk to Jose Segovia
  :LOGBOOK:
  CLOCK: [2024-04-25 Thu 14:04:21]--[2024-04-25 Thu 14:04:42] =>  00:00:21
  :END:
- TODO Get on Solita about getting camera segmentation demo ready
  id:: b314a9ab-785e-42c9-a642-90a146d98179
	- TODO How is the video to be retrieved? Is there some code in place for this?
	- TODO Determine how the plugin for camera segmentation is to be implemented
- TODO Check if video encoding/decoding is happening on the hardware (Siyi A8)
  id:: c67ddd53-eec8-405d-bd77-4ec7a07c120d
- TODO Triggering the RTA modules
  id:: f5c16267-b6ca-4126-be07-13ac7b5dcaed
	- TODO Check first what kind of triggers can be implemented with Solita
	- TODO Check with Mehmet if something like this needs to be implemented in the software and control scheme for the drone