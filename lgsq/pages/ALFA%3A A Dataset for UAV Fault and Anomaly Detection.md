title:: ALFA: A Dataset for UAV Fault and Anomaly Detection
file:: [keipour2020_1710416688776_0.pdf](../assets/keipour2020_1710416688776_0.pdf)
file-path:: ../assets/keipour2020_1710416688776_0.pdf

- ![ALFA: A Dataset for UAV Fault and Anomaly Detection](../assets/keipour2020_1710416688776_0.pdf)
- # Summary
	- Air Lab Fault and Anomaly (ALFA) Dataset.
	- Fault types in control surfaces of fixed-wing UAV.
	- Use cases:
		- Fault Detection and Isolation.
		- Anomaly Detection.
	- Dataset includes: **Processed data for 47 autonomous flights**
		- 23 sudden full engine failure scenarios.
		- 24 scenarios for seven other types of sudden control surface (actuator) faults.
		- 66 minutes of flight in normal conditions.
		- 13 minutes of post-fault flight time.
	- Additional
		- Many hours of raw data of fully-autonomous, autopilot-assisted and manual flights with tens of fault scenarios.
	- Ground truth of time and type of faults provided for each scenario.
	- Helper tools in several programming languages to handle data (Python, C++ and MATLAB).
	- Metrics proposed to help compare different methods using dataset.
	- This is all **real flight data**.
	- Dataset and Tools: [ALFA: A Dataset for UAV Fault and Anomaly Detection](https://doi.org/10.1184/R1/12707963)
- # Experiment Setup
	- Carbon Z T-28 Model Plane
		- Holybro PX4 2.4.6 autopilot.
		- Pitot Tube.
		- GPS module.
		- Nvidia Jetson TX2 onboard computer.
		- Radio and receiver.
	- Pixhawk autopilot with custom version of Ardupilot/ArduPlane (firmware modified from ArduPlane v3.9.0beta1) by adding new parameters"
		- `DisableEngine` - Complete engine failure.
		- `DisableElevator` - Stuck elevator.
		- `DisableRudder` - Rudder hardover.
		- `DisableAileron` - Stuck Aileron.
	- Parameters programmed to work in autonomous mode only (manual mode is safe for controller to take over if fault occurs).
	- GCS triggers faults, pilot controls movement in safety cases.
	- Onboard Computer: ROS Kinetic Kame on Ubuntu 16.04 (with MAVROS).
	- Data recorded as rosbags.
	- Ground truth about faults published periodically which checks status of custom parameters.
	- To access info about internal commands of autopilot (commanded roll/pitch), firmware and MAVROS are modified to publish the data at high frequency through MAVLink.
- # Data Collection
	- Simple rectangular trajectory (full trajectory not always completed as faults injected in between).
	- **Data Formats**
		- Autonomous flight sequences with failures - Each file contains flight sequence with max 1 fault. In `.csv`, `.mat` and `.bag`.
		- Raw flight sequences - Flights in all modes without any preprocessing. Only `.bag`.
		- Telemetry logs from TX2 - Telemetry data from onboard TX2 computer without preprocessing. No fault ground truth information, useful for unsupervised methods.
		- Dataflash logs from Pixhawk - Straight from Pixhawk autopilot without preprocessing. No Fault ground truth information.
	- **Fault Types**
		- | fault type | # cases | flight time pre-fault (s) | flight time post-fault (s) |
		  |-----------|-----------|-----------|-----------|
		  | engine full power loss | 23 | 2282 | 362 |
		  | rudder stuck left | 1 | 60 | 9 |
		  | rudder stuck right | 2 | 107 | 32 |
		  | elevator stuck at zero | 2 | 181 | 23 |
		  | left aileron stuck at zero | 3 | 228 | 183 |
		  | right aileron stuck at zero | 4 | 442 | 231 |
		  | both aileron stuck at zero | 1 | 66 | 36 |
		  | rudder and aileron at zero | 1 | 116 | 27 |
		  | no fault | 10 | 558 | - |
		  | **total** | 47 | 3935 | 777 |
	- **Data Description**
		- Processed file in `.mat` and `.bag` formats contain all available topics. Each `.csv` file includes only one topic.
		- Topics usually available at 4 Hz or higher.
		- Since they are using MAVROS, the telemetry, sensor, and commander topics are in `/mavros/nav_info/` prefix.
		- Ground truth for each control surface is prefixed: `/failure_states/`
			- `/engines`: true/false
			- `/aileron`: 1 means failure on right side, 2 means failure on left side, 3 means both ailerons failure. Fails by getting stuck at 0 position.
			- `/rudder`: 1 means rudder stuck at 0 position, 2 means stuck to leftmost, 3 means stuck to rightmost.
			- `/elevator`: 1 means elevator stuck in 0 position, 2 means suck all the way down.
		- Ground truths recorded at 5 Hz.
	- **Usage:**
		- No dependency on ROS to read or interpret data as long as the rosbag isn't being read.
		- Some sample code provided to interpret data on user side, and provide statistics.
- # Evaluation Metrics
	- **Maximum detection time** - Delay between time of fault and time of detection.
	- **Average detection time** - Overall time performance of method in detecting faults.
	- **Accuracy** - Ratio $\frac{\text{number of correctly classified sequences}}{\text{total number of sequences}}$
	- **Precision** - Ratio $\frac{\text{sequences with correctly predicted faults}}{\text{total number of detections}}$
	- **Recall** - Ratio $\frac{\text{sequences with correctly predicted faults}}{\text{total number of sequences containing faults}}$
- # Evaluation
	- Sudden control surface failures investigated, but other types of failures are also common in UAVs (sensors, actual errors, etc.)