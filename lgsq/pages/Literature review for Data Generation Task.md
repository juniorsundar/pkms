- #+BEGIN_NOTE
  Is there a shortage in this field?
  Are there any existing solutions to this shortage?
  How are datasets usually framed in this context?
  #+END_NOTE
- **One example**: [Dania's Dataset](https://www.kaggle.com/datasets/daniaherzalla/tii-ssrc-23)
- **Reviewed Literature**:
  id:: 65f8249b-d3d4-4730-a115-bf181589f923
	- Pertinent:
		- DONE [[UAV sensor failures dataset: Biomisa arducopter sensory critique (BASiC)]]
		- DONE [[ALFA: A Dataset for UAV Fault and Anomaly Detection]]
		  :LOGBOOK:
		  CLOCK: [2024-03-15 Fri 16:03:17]
		  CLOCK: [2024-03-15 Fri 21:31:58]--[2024-03-18 Mon 14:00:50] =>  64:28:52
		  :END:
		- DONE [[Novelty-based Intrusion Detection of Sensor Attacks on Unmanned Aerial Vehicles]]
		  :LOGBOOK:
		  CLOCK: [2024-03-18 Mon 15:05:11]
		  CLOCK: [2024-03-18 Mon 15:06:21]--[2024-03-19 Tue 10:37:51] =>  19:31:30
		  :END:
		- DONE [[Acquisition and Processing of UAV Fault Data Based on Time Line Modeling Method]]
		  :LOGBOOK:
		  CLOCK: [2024-03-19 Tue 12:30:38]--[2024-03-19 Tue 14:30:25] =>  01:59:47
		  :END:
		- DONE [[ECU-IoFT: A Dataset for Analysing Cyber-Attacks on Internet of Flying Things]]
		  :LOGBOOK:
		  CLOCK: [2024-03-19 Tue 11:20:36]--[2024-03-19 Tue 12:21:23] =>  01:00:47
		  CLOCK: [2024-03-19 Tue 12:21:24]--[2024-03-19 Tue 12:21:33] =>  00:00:09
		  :END:
	- Irrelevant:
		- DONE [[Research on Drone Fault Detection Based on Failure Mode Databases]]
		- DONE [On-board Deep-learning-based Unmanned Aerial Vehicle Fault Cause Detection and Identification](https://sci-hub.st/10.1109/icra40945.2020.9197071)
	- To-Read:
- **Review**:
  id:: 65fa87e2-c130-402d-8cae-80c05aeca9c9
	- Most datasets favour SITL or simulated data when it comes to behaviour under fault. Two were found that used real flight data, but one was for fixed-winged UAVs and the other was for intrusion detection use cases.
	- The extent of fault cases are also limited in all available datasets. Faults are either binary (engine on/off, sensor on/off, etc.) or spoofing the GPS. Most papers assume that the GPS is the prime target for most attacks, and the one most susceptible to faults.
	- Datasets are provided in ULOG format (logs dumped in the autopilot after every mission) or in `.csv`, or both. Some papers also provide rosbags and `.mat` files.
	- There is also a raw and processed dataset:
		- The raw dataset either leaves all columns as is, or drops some columns deemed irrelevant.
		- The processed dataset renames keys to make it descriptive and further refines the data set by: dropping additional columns deemed irrelevant; interpolating data.
		- Metadata is also important when providing
	- Data is labelled:
		- Some papers have an overarching indication of if a data set includes fault (is malicious, etc.)
		- Some papers take it further and mark timestamps where fault is injected and what type of fault it is.
	- PX4 or ArduPilot are the commonly used firmwares for the autopilot.
	- All reviewed datasets keep number of active faults at a time to one (1).
	- Data generation occurs in a constant mission/trajectory (a fixed set of missions or trajectories).
- **Considerations:**
  id:: 65fa8fd6-4ac5-4e73-8d0e-e94ae4d78757
	- Autopilots tend to have failsafes in place in case of certain types of fault scenarios. Should this be deactivated?
		- [1]([[UAV sensor failures dataset: Biomisa arducopter sensory critique (BASiC)]]) does not deactivate failsafes.
		- [2]([[ALFA: A Dataset for UAV Fault and Anomaly Detection]]) has a human-in-the-loop-ish setup wherein the human takes over during failure. So essentially the failsafe is disabled.
		- [3]([[Acquisition and Processing of UAV Fault Data Based on Time Line Modeling Method]]) seems to have deactivated the failsafes.
	- Should the data collection adhere to the methodology used in these public datasets? (Preference of using ULOG files to dump raw data).
		- Will make simulation automation much easier as there won't be a need to synchronise bag collection and dumping. Can filter out data using timestamps of mission start/end, fault start/end, or other landmark points.
		- Currently, data is being pre-processed as it is being collected. With this method, the processing can be delayed until all data is collected.
	- How to establish a "control" in data collection? Design of experiment.
		- Is it necessary?
		- Is there a benefit to having complete randomisation?