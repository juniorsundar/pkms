# Subsections
	- [[PX4 - ROS 2 Integration]]
	- [[PX4 - Simulation]]
	- [[PX4 - uORB]]
	- [[PX4 - Safety Configuration]]
	- [[PX4 - Controls]]
- # Introduction
	- It is a professional autopilot that can be used to power all kinds of vehicles, ranging from drones to ground vehicle and submarines.
	- *Access the documentation [here](https://docs.px4.io/main/en/).*
- # Flight Controller
	- Brains of the unmanned vehicle. PX4 can run on many flight controller boards. Selection of board must suit physical and sensor constraints of the vehicle as well as the type of function the vehicle has.
	- ## Pixhawk Series
		- These are open-hardware flight controllers that run PX4 on the NuttX OS.
		- *Access their website [here](https://pixhawk.org/).*
- # Middleware
	- ## [uORB]([[PX4 - uORB]])
		- It is an asynchronous publish()/subscribe() messaging API used for inter-thread/inter-process communication. It is automatically started early on bootup.
		- In the controller, the desired data is being logged by ULog (PX4's flight logging system). This data is packaged into messages that are transmitted through uORB topics.
		- *Read advanced notes on this [here](https://docs.px4.io/main/en/middleware/uorb.html).*
	- ## μXRCE-DDS (PX4-ROS 2/DDS Bridge)
	  id:: 65f33d3f-30be-412b-996f-0f9e61169323
		- This is the middleware that allows the uORB messages to be published and subscribed on the companion computer as though they were ROS 2 topics.
		- The architecture is defined in the below image:
		- ![image.png](../assets/image_1710440235209_0.png)
		- The client runs on the flight controller, while the agent is on the companion processor. The client reveals the uORB topics active the flight controller to the agent, and the agent decides which of these are to exposed as ROS 2 topics that can then be accessed through nodes running on the local system.
		- *Read advanced notes on this [here](https://docs.px4.io/main/en/middleware/uxrce_dds.html).*
	- ## MAVLink
		- It is a lightweight messaging protocol that is designed to be used in the drone ecosystem. It is designed for efficiently sending messages over unreliable low-bandwidth radio links.
		- PX4 uses MAVLink to communicate with ground stations and apps built with [[MAVSDK]] such as [QGroundControl](((65f339db-c87b-4535-be4f-1840d124d265))) .
- # Development
	- ## Toolchain Installation (Ubuntu)
		- ### Autopilot Installation
		  id:: 65f8249b-a538-46bb-b8eb-8416c2d03f19
			- To install the PX4-Autopilot toolchain for the Ubuntu system, run the following.
			- ```bash
			  # For Ubuntu
			  # Pull the source code
			  # This will automatically retrieve the most recent version of the autopilot
			  git clone https://github.com/PX4/PX4-Autopilot.git --recursive
			  
			  # Running this will install everything
			  bash ./PX4-Autopilot/Tools/setup/ubuntu.sh --no-nuttx
			  
			  # Restart after installation
			    sudo reboot now
			  ```
		- ### μXRCE-DDS Agent Installation
			- The agent needs to be built on the companion processor, with the following steps.
			- ```bash
			  # For Ubuntu
			  # This is the installation for the agent.
			  git clone https://github.com/eProsima/Micro-XRCE-DDS-Agent.git
			  
			  cd Micro-XRCE-DDS-Agent
			  mkdir build
			  cd build
			  cmake ..
			  make
			  sudo make install
			  sudo ldconfig /usr/local/lib/
			  ```
		- ### QGroundControl
		  id:: 65f339db-c87b-4535-be4f-1840d124d265
			- This software provides full flight control and mission planning for any MAVLink enabled drone.
			- To install this, do the following:
			  ```bash
			  # For Ubuntu
			    sudo usermod -a -G dialout $USER
			    sudo apt-get remove modemmanager -y
			    sudo apt install gstreamer1.0-plugins-bad gstreamer1.0-libav gstreamer1.0-gl -y
			    sudo apt install libqt5gui5 -y
			    sudo apt install libfuse2 -y
			  ```
			- Log out and log in to enable user changes.
			- Download the application [here](https://docs.qgroundcontrol.com/master/en/qgc-user-guide/getting_started/download_and_install.html).
			- Install using terminal commands.
			- ```bash
			  # For Ubuntu
			  chmod +x ./QGroundControl.AppImage
			  ./QGroundControl.AppImage  # or double click
			  ```
		- ### [Simulation (SITL)]([[PX4 - Simulation]])
			- Simulation is a quick, easy, and most importantly, safe way to test changes to PX4 code before attempting to fly in the real world. It is also a good way to start flying with PX4 when you haven't yet got a vehicle to experiment with.
			- PX4 supports both [Software In the Loop (SITL)]([[Software in the Loop]]) simulation, where the flight stack runs on computer (either the same computer or another computer on the same network) and [Hardware In the Loop (HITL)]([[Hardware in the Loop]]) simulation using a simulation firmware on a real flight controller board. HITL is only community supported.
		- ### [ROS]([[PX4 - ROS 2 Integration]])
			- Limited only to ROS 2 since ROS 1 is slowly reaching deprecation. Through the [μXRCE-DDS](((65f33d3f-30be-412b-996f-0f9e61169323))) client-agent, it is possible to expose the uORB messages in the flight controller to the ROS 2 framework. This facilitates forward and backwards communication.
	- ## Fault Injection
		- It is possible to inject faults into the flight controller. This methodology is observed in {:$/research/literature-review/coutinho2021:}[literature review]. The strategy can be applied by introducing faults into the source code itself.
		- ### Example: IMU
		  collapsed:: true
			- To introduce a dynamic way to inject and remove faults from this module, we can take advantage of the parameter server in the FC (by launching custom parameters).
			- ```cpp
			  /**
			  * Navigate to ./PX4-Autopilot/src/modules/sensors/vehicle_imu/VehicleIMU.cpp
			  * Add the following snippet of code before the _vehicle_imu_pub.publish(imu) call
			  *
			  **/
			  // Adding faults to the accelerometer
			  param_t accel_fault = param_find("SENS_ACCEL_FAULT");
			  int32_t accel_fault_flag;
			  param_get(accel_fault, &accel_fault_flag);
			  
			  if (accel_fault_flag == 1)
			  {
			      param_t accel_noise = param_find("SENS_ACCEL_NOISE");
			      float_t accel_noise_flag;
			      param_get(accel_noise, &accel_noise_flag);
			  
			      if (abs(accel_noise_flag) > 0)
			      {
			          unsigned seed = std::chrono::system_clock::now().time_since_epoch().count();
			          std::default_random_engine generator (seed);
			  
			          std::normal_distribution<float> distribution (0.0,accel_noise_flag);
			          float dev = distribution(generator);
			          imu.delta_velocity[0] += imu.delta_velocity[0]*dev;
			          imu.delta_velocity[1] += imu.delta_velocity[1]*dev;
			          imu.delta_velocity[2] += imu.delta_velocity[2]*dev;
			      }
			  
			      param_t accel_bias_shift = param_find("SENS_ACCEL_SHIF");
			      float_t accel_bias_shift_flag;
			      param_get(accel_bias_shift, &accel_bias_shift_flag);
			  
			      if (abs(accel_bias_shift_flag) > 0)
			      {
			          imu.delta_velocity[0] += imu.delta_velocity[0]*accel_bias_shift_flag;
			          imu.delta_velocity[1] += imu.delta_velocity[1]*accel_bias_shift_flag;
			          imu.delta_velocity[2] += imu.delta_velocity[2]*accel_bias_shift_flag;
			      }
			  
			      param_t accel_bias_scale = param_find("SENS_ACCEL_SCAL");
			      float_t accel_bias_scale_flag;
			      param_get(accel_bias_scale, &accel_bias_scale_flag);
			  
			      if (abs(accel_bias_scale_flag) > 0)
			      {
			          imu.delta_velocity[0] *= accel_bias_scale_flag;
			          imu.delta_velocity[1] *= accel_bias_scale_flag;
			          imu.delta_velocity[2] *= accel_bias_scale_flag;
			      }
			  
			      param_t accel_drift = param_find("SENS_ACCEL_DRIFT");
			      float_t accel_drift_flag;
			      param_get(accel_drift, &accel_drift_flag);
			  
			      if (abs(accel_drift_flag) > 0)
			      {
			          //! Will have to initialise and declare 'accel_drift_timestep'
			          imu.delta_velocity[0] += 0.01f*accel_drift_flag*accel_drift_timestep/1000000;
			          imu.delta_velocity[1] += 0.01f*accel_drift_flag*accel_drift_timestep/1000000;
			          imu.delta_velocity[2] += 0.01f*accel_drift_flag*accel_drift_timestep/1000000;
			  
			          accel_drift_timestep += 1;
			      }
			  
			      param_t accel_zero = param_find("SENS_ACCEL_ZERO");
			      int32_t accel_zero_flag;
			      param_get(accel_zero, &accel_zero_flag);
			  
			      if (accel_zero_flag == 1)
			      {
			          imu.delta_velocity[0] = 0;
			          imu.delta_velocity[1] = 0;
			          imu.delta_velocity[2] = 0;
			      }
			  }
			  
			  // Adding faults to the gyroscope
			  param_t gyro_fault = param_find("SENS_GYRO_FAULT");
			  int32_t gyro_fault_flag;
			  param_get(gyro_fault, &gyro_fault_flag);
			  
			  if (gyro_fault_flag == 1)
			  {
			      param_t gyro_noise = param_find("SENS_GYRO_NOISE");
			      float_t gyro_noise_flag;
			      param_get(gyro_noise, &gyro_noise_flag);
			  
			      if (abs(gyro_noise_flag) > 0)
			      {
			          unsigned seed = std::chrono::system_clock::now().time_since_epoch().count();
			          std::default_random_engine generator (seed);
			  
			          std::normal_distribution<float> distribution (0.0,gyro_noise_flag);
			          float dev = distribution(generator);
			          imu.delta_angle[0] += imu.delta_angle[0]*dev;
			          imu.delta_angle[1] += imu.delta_angle[0]*dev;
			          imu.delta_angle[2] += imu.delta_angle[0]*dev;
			      }
			  
			      param_t gyro_bias_shift = param_find("SENS_GYRO_SHIF");
			      float_t gyro_bias_shift_flag;
			      param_get(gyro_bias_shift, &gyro_bias_shift_flag);
			  
			      if (abs(gyro_bias_shift_flag) > 0)
			      {
			          imu.delta_angle[0] += imu.delta_angle[0]*gyro_bias_shift_flag;
			          imu.delta_angle[1] += imu.delta_angle[1]*gyro_bias_shift_flag;
			          imu.delta_angle[2] += imu.delta_angle[2]*gyro_bias_shift_flag;
			      }
			  
			      param_t gyro_bias_scale = param_find("SENS_GYRO_SCAL");
			      float_t gyro_bias_scale_flag;
			      param_get(gyro_bias_scale, &gyro_bias_scale_flag);
			  
			      if (abs(gyro_bias_scale_flag) > 0)
			      {
			          imu.delta_angle[0] *= gyro_bias_scale_flag;
			          imu.delta_angle[1] *= gyro_bias_scale_flag;
			          imu.delta_angle[2] *= gyro_bias_scale_flag;
			      }
			  
			      param_t gyro_drift = param_find("SENS_GYRO_DRIFT");
			      float_t gyro_drift_flag;
			      param_get(gyro_drift, &gyro_drift_flag);
			  
			      if (abs(gyro_drift_flag) > 0)
			      {
			          //! Will have to initialise and declare 'gyro_drift_timestep'
			          imu.delta_angle[0] += 0.01f*gyro_drift_flag*gyro_drift_timestep/1000000;
			          imu.delta_angle[1] += 0.01f*gyro_drift_flag*gyro_drift_timestep/1000000;
			          imu.delta_angle[2] += 0.01f*gyro_drift_flag*gyro_drift_timestep/1000000;
			  
			          gyro_drift_timestep += 1;
			      }
			  
			      param_t gyro_zero = param_find("SENS_GYRO_ZERO");
			      int32_t gyro_zero_flag;
			      param_get(gyro_zero, &gyro_zero_flag);
			  
			      if (gyro_zero_flag == 1)
			      {
			          imu.delta_angle[0] = 10000;
			          imu.delta_angle[1] = 10000;
			          imu.delta_angle[2] = 10000;
			      }
			  }
			  ```
		- ### Example: GPS
		  collapsed:: true
			- Some cases are different when working with the SITL or the actual drone. For instance, the GPS fault injection requires affecting the data generated from the simulation side itself.
			- ```cpp
			  /**
			  * Navigate to ./PX4-Autopilot/src/modules/simulation/sensor_gps_sim/SensorGpsSim.cpp
			  * Add the following snippet of code before the _sensor_gps_pub.publish(sensor_gps) call
			  *
			  **/
			  // Adding faults to the gps
			  param_t gps_fault = param_find("SENS_GPS_FAULT");
			  int32_t gps_fault_flag;
			  param_get(gps_fault, &gps_fault_flag);
			  if (gps_fault_flag == 1)
			  
			  {
			      param_t gps_noise = param_find("SENS_GPS_NOISE");
			      float_t gps_noise_flag;
			      param_get(gps_noise, &gps_noise_flag);
			  
			      if (abs(gps_noise_flag) > 0)
			      {
			          unsigned seed = std::chrono::system_clock::now().time_since_epoch().count();
			          std::default_random_engine generator (seed);
			  
			          std::normal_distribution<double> distribution (0.0,static_cast<double>(gps_noise_flag));
			          double dev = distribution(generator);
			          sensor_gps.latitude_deg += sensor_gps.latitude_deg*dev;
			          sensor_gps.longitude_deg += sensor_gps.longitude_deg*dev;
			          sensor_gps.altitude_msl_m += sensor_gps.altitude_msl_m*dev;
			          sensor_gps.altitude_ellipsoid_m += sensor_gps.altitude_ellipsoid_m*dev;
			      }
			  
			      param_t gps_bias_shift = param_find("SENS_GPS_SHIF");
			      float_t gps_bias_shift_flag;
			      param_get(gps_bias_shift, &gps_bias_shift_flag);
			  
			      if (abs(gps_bias_shift_flag) > 0)
			      {
			          sensor_gps.latitude_deg += sensor_gps.latitude_deg*static_cast<double>(gps_bias_shift_flag);
			          sensor_gps.longitude_deg += sensor_gps.longitude_deg*static_cast<double>(gps_bias_shift_flag);
			          sensor_gps.altitude_msl_m += sensor_gps.altitude_msl_m*static_cast<double>(gps_bias_shift_flag);
			          sensor_gps.altitude_ellipsoid_m += sensor_gps.altitude_ellipsoid_m*static_cast<double>(gps_bias_shift_flag);
			      }
			  
			      param_t gps_bias_scale = param_find("SENS_GPS_SCAL");
			      float_t gps_bias_scale_flag;
			      param_get(gps_bias_scale, &gps_bias_scale_flag);
			  
			      if (abs(gps_bias_scale_flag) > 0)
			      {
			          sensor_gps.latitude_deg *= static_cast<double>(gps_bias_scale_flag);
			          sensor_gps.longitude_deg *= static_cast<double>(gps_bias_scale_flag);
			          sensor_gps.altitude_msl_m *= static_cast<double>(gps_bias_scale_flag);
			          sensor_gps.altitude_ellipsoid_m *= static_cast<double>(gps_bias_scale_flag);
			      }
			  
			      param_t gps_drift = param_find("SENS_GPS_DRIFT");
			      float_t gps_drift_flag;
			      param_get(gps_drift, &gps_drift_flag);
			  
			      if (abs(gps_drift_flag) > 0)
			      {
			          sensor_gps.latitude_deg += 0.01*static_cast<double>(gps_drift_flag)*gps_drift_timestep/1000000;
			          sensor_gps.longitude_deg += 0.01*static_cast<double>(gps_drift_flag)*gps_drift_timestep/1000000;
			          sensor_gps.altitude_msl_m += 0.01*static_cast<double>(gps_drift_flag)*gps_drift_timestep/1000000;
			          sensor_gps.altitude_ellipsoid_m += 0.01*static_cast<double>(gps_drift_flag)*gps_drift_timestep/1000000;
			  
			          gps_drift_timestep += 1;
			      }
			  }
			  ```