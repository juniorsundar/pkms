# 12 June 2024
id:: 666934e0-39c9-403c-b79a-6e5ef697de5a
tag:: #MEETING
	- **Attendees**
		- SRTA-AD
	- **Goal**
		- Discuss current project statuses and address any blockers.
		- Align on next steps and action points for ongoing projects.
	- **Agenda**
		- Update on Drone project
		- Jira follow-up
		- Nvidia DGX replacement status
		- Solita vs SRTA AD Demo target discussion
	- **Minutes**
		- Drone: Waiting on RJ45 adaptor
		- Jira followup:
			- predef JIRA template structure
			- same method of adding content to Jira
			- too early to conduct sprints
			- Can use Jira label for filtering if needed
		- Nvidia DGX replacement is stuck because of some geopolitical issues
		- Solita vs SRTA AD Demo target:
			- Solita is going for a Proof of concept with hybrid sim/hardware approach.
			- SRTA AD is going for a hardware proof of concept.
			- Seems to me that both parties are still not in proper sync
	- **Action Points**
		- TODO Write up full update for Week 23 and 24 on Confluence.
- # 5 June 2024
  tag:: #MEETING
  id:: 666975bf-7e03-46d2-8762-f43f7b42d7ce
  collapsed:: true
	- **Attendees**
	  collapsed:: true
		- SRTA-AD
	- **Goal**
	  collapsed:: true
		- Update from the week towards demo
	- **Agenda**
	  collapsed:: true
		- Discuss progress and hold ups on my side
		- Understand the progress form everyone else
	- **Minutes**
	  collapsed:: true
		- GITEX demo
			- OpenSet speaker identification (VAuth)? It seems it isnt needed
			- Transcribing text -> language understanding
		- RTA issues on Saluki V3 as they haven't tested the SRTA modules in the V3.
	- **Action Points**
	  collapsed:: true
		- ((665ff704-5b0e-455b-b730-49c4c89148f6))
		- DONE Find out if PX4 has battery lifecycle estimation
		- DONE Confirm methodology from Sakari to launch the SRTA modules
- # 29 May 2024
  id:: 666975bf-3431-4971-aced-f257086f27a5
  tag:: #MEETING
  collapsed:: true
	- **Attendees**
	  collapsed:: true
		- SRTA-AD
	- **Goals**
	  collapsed:: true
		- Update for demo
	- **Agenda**
	  collapsed:: true
		- Discuss progress on hold-out on physical demonstration.
	- **Minutes**
	  collapsed:: true
		- Moved as JIRA tasks in the SYSTEST team, so it is now in progress.
			- The main points have been clarified with John.
			- ((664f9f87-a976-490c-a59c-d068f1698a15))
		- [GITEX needs to be discussed at a later time](((66581fb0-66ca-4bc7-ae37-8f6e175f6774)))
	- **Action Points**
	  collapsed:: true
		- CANCELLED Test flight mission at 6AM @ [[May 30th, 2024]]
			- The GCS isn't communicating with the drone so cannot control autonomous missions with fog-system
			- QGC still works. Tie this in with --> ((66581d82-205a-4df6-9c16-f90213a69668))
- # 23 May 2024
  id:: 6666b7a8-30cb-4a40-8916-709c82c8a8d6
  tag:: #MEETING
  collapsed:: true
	- **Attendees**
		- SRTA-AD
	- **Goals**
		- Demo updates and timelines
	- **Agenda**
		- Discuss how much work is left for drone flight
		- Point out blockers and problems
	- **Minutes**
		- Drone nearing flight, but no promises.
		- Documentation is sparse and heavily distributed. They make it upon request basically.
		- Have not been able to allocate time for work in the collab project due to bandwidth being utilised for the flight preparation.
		- Some work needs to be done on the data collection stuff.
	- **Action Items**
		- ((665038b5-88dc-4cf8-a496-9feb389f8c85))
		- ((66503288-71ad-481c-bb6d-2300cdffbaba))
- # 15 May 2024
  id:: 6666b7a8-6843-45a8-91fd-afe78ccaca4e
  tag:: #MEETING
  collapsed:: true
	- **Attendees**
		- SRTA-AD
	- **Goals**
		- Demo update and timelines
	- **Agenda**
		- Discuss state of system in preparation for the demo
		- Set demo deadlines
	- **Minutes**
		- People need to go for the International Exhibition of National Security and Resilience conference in ADNEC.
		- Sakari: Building new fog-system and writing to a bootable USb to try and install into Saluki V3.
		- SRTA will be running inside the App VM.
		- Prepare a X500 as backup for far future -- not a priority at the moment.
	- **Action Item**
		- ((664498b2-da80-418c-ac4b-49c004bc01cb))
		- ((664499d6-f73c-49a9-bd7c-6d2ddd36eb87))
		- ((6644991b-cbe7-4882-9761-382fc01aeb4c))
- # 8 May 2024
  id:: 6666b7a7-9d7f-4fa4-8d55-104820d6b34b
  tag:: #MEETING
  collapsed:: true
	- **Attendees**
	  collapsed:: true
		- SRTA-AD
	- **Goals**
	  collapsed:: true
		- Establish goals and requirements for [[Q2 June Demo]]
	- **Agenda**
	  collapsed:: true
		- Update from Sakari on GPU accessibility status
		- Update on data collection and experimentation
	- **Minutes**
	  collapsed:: true
		- Emrah and Ilkka have introduced a hack to get GPU passthrough working.
		- Passed this to Manuel, but some library dependency (libgstreamer) issue is stopping it from reaching release.
		- If we can use T-M690b for flights here over hacking Holybro-X500 it would be better.
		- RTA anomaly detection model from template --> may need to provide assistance to set up the ROS nodes for this.
		- **Safety island:** at time of total failure, have a backup working
			- for "Rabdan" SoC.
			- how to extract data at such cases?
	- **Action Items**
	  collapsed:: true
		- DONE Send data from F4F missions
			- DONE to Shamsa
			- DONE to Samridha
		- ((663b5e94-aac1-4c11-91c3-48f6fdf3a1c0))
		- ((663b5eaf-de76-4d72-8f3f-9bd0c64025f2))
- # 1 May 2024
  id:: 6666b7a7-d168-40cb-b85a-14fb97789bcc
  tag:: #MEETING
  collapsed:: true
	- **Attendees**
	  collapsed:: true
		- SRTA-AD
	- **Goal**
	  collapsed:: true
		- Discuss who is doing a demo
		- Discuss what all are required and what the timeline will be for the demo
	- **Agenda**
	  collapsed:: true
		- Bring up the current bottlenecks for the demo
		- Update on the progress of current tasks
	- **Minutes**
	  collapsed:: true
		- Is the camera driver integration supported?
			- Apparently we have to develop our own drivers for attachments apart from standard installation.
			- Luckily the Siyi A8 is supported.
		- Check if there is packet loss when recording data on FMO?
		- Usually with demos, the flight are first done in Prague F4F before being tested in TII
	- **Action Items**
	  collapsed:: true
		- DONE Send the F4F data to Shamsa
		- ((c67ddd53-eec8-405d-bd77-4ec7a07c120d))
		- ((b314a9ab-785e-42c9-a642-90a146d98179))
		- ((f5c16267-b6ca-4126-be07-13ac7b5dcaed))
- # 25 April 2024
  id:: 6666b7a7-feec-422b-b07c-f15537ffe850
  tag:: #MEETING
  collapsed:: true
	- **Attendees**
	  collapsed:: true
		- SRTA-AD
	- **Goals**
	  collapsed:: true
		- Introduce Iraklis as new PM
		- Update on work
	- **Agenda**
	  collapsed:: true
		- Demo requirements and updates
		- Research collaboration update
	- **Minutes**
	  collapsed:: true
		- How do we show stuff that must be demo'd? --> [Task](DONE Fill up the hardware requirements spreadsheet
		  SCHEDULED: <2024-04-26 Fri 12:00>
		  id:: 662b46fc-94b2-48b8-8db6-61a6172e6705
		  :LOGBOOK:
		  CLOCK: [2024-04-26 Fri 11:11:58]--[2024-04-26 Fri 14:05:10] =>  02:53:12
		  :END:)
		  - Breakdown into steps
		  - Do even if it isn't part of the objectives of this quarter
		  - Hardware details and requirements need to be listed and elaborated upon
		  - Image segmentation demo idea:
		  - ![demo-segmentation.png](../assets/demo-segmentation_1714134642834_0.png)
		  - Flying license will take upto a week to at least start the process
		  - LLM to access outputs from RTA modules to decide on drone manouvre
		  - **Action Items**
		  collapsed:: true
		  - DONE Fill up the hardware requirements spreadsheet
		  SCHEDULED: <2024-04-26 Fri 12:00>
		  id:: 662b46fc-94b2-48b8-8db6-61a6172e6705
		  :LOGBOOK:
		  CLOCK: [2024-04-26 Fri 11:11:58]--[2024-04-26 Fri 14:05:10] =>  02:53:12
		  :END:
		- Send Raw GPS data to Siva