# Introduction
	- _Access [documentation](https://docs.px4.io/main/en/config/safety.html)_
	- Failsafes specify areas and conditions in which it is safe to fly. It also indicates actions to be performed if failsafe is triggered.
	- Most important failsafe settings are configured in QGroundControl Safety Setup page. Others are through parameters.
	- In remote, can use safety switches to immediately stop motors or return vehicle.
- # Failsafe Actions
	- | **Action**   | **Description**                                           |
	  |--------------|-----------------------------------------------------------|
	  | None/Disabled| No action. Failsafe will be ignored.                      |
	  | Warning      | Warning message will be sent.                             |
	  | Hold         | Will enter hold mode, and hover or circle.                |
	  | Return       | Enters return mode. Behavior is configurable.             |
	  | Land         | Will enter land mode.                                     |
	  | Disarm       | Stops motors immediately.                                 |
	  | Termination  | Turns off all controllers and sets PWM to failsafe values. Can be used to deploy a parachute, landing gear, etc.     |
- # Safety Setup
	- ## through QGroundControl
		- _Note: This only includes most important failsafe settings._
		- ### Low Battery
			- Triggered when battery capacity drops below one or more warning levels. You have `Warn` > `Failsafe` > `Emergency` trigger levels in battery percent.
			- Only options are to **Warn**, **Return** or **Land**. Either triggered when battery level falls below failsafe, or can distribute it according to the different trigger levels.
		- ### Manual Control Loss
			- Triggered if connection to RC transmitter or joystick is loss without fallback. In QGC, you can set RC Loss timeout and failsafe action.
		- ### Data Link Loss
			- Triggered if telemetry link to groundstation is lost. Can set a timeout and failsafe action.
		- ### Geofence
			- Triggered when drone breaches virtual perimeter. Can specify max radius and altitude or provide more complex geofences through alternate means. Also includes failsafe action on breach.
		- ### Configure Return Mode
			- This failsafe action can be configured here. Can set land/loiter behaviour after returning.
		- ### Configure Land Mode
			- Can specify descent rate in metres-per-second and also configure if the system should be disarmed (after a provided duration).
	- ## through Parameters or Other Means
		- ### Position (GPS) Loss
			- Triggered if quality of PX4 position estimate falls below acceptable levels (can be cause by GPS loss)
			- When triggered, it will either Hold or enter Land mode depending on nature of available information.
			- Can set the duration before failsafe trigger through parameter server.
		- ### Offboard Loss
			- Triggered if offboard link is lost while under offboard control mode. Refer to ## [Offboard Control Mode](((e35379dd-34a5-4936-9131-40fa68faba26))) to understand what the offboard control signal rate signifies.
		- ### Traffic Avoidance
			- Allows PX4 to respond to transponder data during missions. Can set failsafe actions through parameters.
- # Failure Detector
	- Allows a vehicle to take protective action if it unexpectedly flips or if notified by external failure detection system.
	- Failure detector during flight is deactivated by default. Enable by setting `CBRK_FLIGHTTERM=0`
	- Failure detective is active on all vehicle types and modes, except for those expected to do flips.
	- ## Attitude Trigger
		- Can be configured to trigger if vehicle attitude exceeds predefined pitch and roll for longer than specific time period.
		- During takeoff, it invokes disarm if vehicle flips. Always active on
		  takeoff irrespective of `CBRK_FLIGHTTERM`
	- ## External Automatic Trigger System (ATS)
		- External ATS must be connected to flight controller port AUX5 (or MAIN5) and configured using the assigned parameters.