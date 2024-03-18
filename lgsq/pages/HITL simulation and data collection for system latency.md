- DONE Syncup with Yashrajsinh to hash out requirements of the HITL simulation
	- Drone is running
	  :LOGBOOK:
	  CLOCK: [2024-03-07 Thu 00:01:01]
	  :END:
		- In Hover mode
		- Take one test in Path mode
	- Recording topics (refer to PPT)
		- Timestamped and only pertinent data required
	- Fault activation
		- All 5 sensors
		- $-\infty$ to 0 to $+\infty$
	- Run till failure or set time point
		- Failure defined by crash, sudden landing, out of bounds
		- Out of bounds in 2 levels: unacceptable, and failure (1m, 5m)
	- Dump data for analysis
- DONE Trigger and be able to observe the faults in HITL
  :LOGBOOK:
  CLOCK: [2024-03-07 Thu 00:02:32]
  CLOCK: [2024-03-07 Thu 00:02:34]--[2024-03-14 Thu 15:24:20] =>  183:21:46
  :END:
	- The modules in SITL and HITL are quite different when considering anything apart from the IMU. Directly porting the SITL into HITL did not work, because the GPS, Magnetometer and Barometer are in different source modules.
	- Wasn't able to find these modules. I've tried editing the drivers as well, but it seems that in HITL, the values being published and observed through the ros2 topics aren't reflecting the faults being injected. To expand on this, when addingsome type of fault like setting all values of a particular sensor to zero, only the resulting deviation is observed in the ros2 topics. The values aren't actually getting fully set to zero.
- DONE Set up automated simulation and data collection pipeline
  :LOGBOOK:
  CLOCK: [2024-03-07 Thu 00:03:30]--[2024-03-14 Thu 15:24:39] =>  183:21:09
  :END:
	- **RO2 Node Architecture**
		- Keep the `drone_controller.py` node for param setting and drone launching.
		- Update the `drone_state_monitor.py` node to ensure system remains within
		  limits.
		- ~~Need to edit the `fault_manager.py` such that it triggers a fault after a fixed interval given the sensor that needs to be faulted and the type of fault it needs to experience:~~
			- ~~All zeros~~
			- ~~All max~~
		- Due to the straightforward nature of this process, we can bundle up the fault activation AND the iteration management into `iteration_manager.py`
		- Edit `sensor_recorder_unsync.py` to listen to the below list of topics.
		  This needs to narrowed down a bit:
			- sensor_gyro
			- sensor_accel
			- sensor_mag
			- sensor_baro
			- sensor_gps
			- vehicle_angular_velocity
			- vehicle_acceleration
			- vehicle_attitude
			- vehicle_local_position
			- vehicle_global_position
			- actuator_outputs
			- actuator_controls
	- **Simulation and Data Collection Management**
		- Since it is a one-off deal, there isn't any necessity to set up an   auto-start, kill and relaunch feature. Manual start and kill is sufficient.
		- Write a bash script that, once the simulation in HITL is launched, launches above nodes in correct sequence. It should then:
			- Ready drone
			  logseq.order-list-type:: number
			- Start data recording
			  logseq.order-list-type:: number
			- Trigger fault at fixed time
			  logseq.order-list-type:: number
				- Put a tag in data collection when fault is triggered
			- Stop recording when the drone leaves the boundaries
			  logseq.order-list-type:: number
				- Also apply a tag when the drone switches from *acceptable* to *unacceptable* to *failure*
			- Dump records to `.csv`
			  logseq.order-list-type:: number
			- Reset all applied faults prepare for reset
			  logseq.order-list-type:: number
			- Rinse and repeat for next fault
			  logseq.order-list-type:: number
- DONE Collect data and compile it for analysis
  :LOGBOOK:
  CLOCK: [2024-03-14 Thu 15:24:57]
  CLOCK: [2024-03-14 Thu 15:25:04]--[2024-03-18 Mon 14:19:11] =>  94:54:07
  :END:
	- Wrote a data converter and compiler according to the needs of the final data set. Processing is still needed for this, though that can be done at a later date.
	- Ready to move on to the HITL setup, since things are working well in SITL. Of course, the issue of whether faults injected will become evident in the data is a question. But as per Yashrajsinh, it shouldn't matter as long as the deviations are being captured.
	- **LEFT**:
		- ~~Baro Max~~
		- ~~Baro Min~~
		- ~~Redo Mag Max~~
	- #IMPORTANT When dumping data, check if data integrity is maintained after each dump. Because sometimes not all data is recorded because of some weird edge case.