title:: ECU-IoFT: A Dataset for Analysing Cyber-Attacks on Internet of Flying Things
file:: ![ECU-IoFT: A Dataset for Analysing Cyber-Attacks on Internet of Flying Things](../assets/ahmed2022_1710759991443_0.pdf)
file-path:: ../assets/ahmed2022_1710759991443_0.pdf
categories:: #uav-fault-dataset

- # Summary
	- ECU-IoFT (Edith Cowan University) documents three known cyber-attacks targetting Wi-Fi communications and lack of security in an affordable off-the-shelf drone.
		- Denial-of-service (control signals and GPS)
		- Man-in-the-middle attacks
		- Exploited API
	- **IoFT** - Internet of Flying Things
	- No publicly available labeled datasets that reflect cyberattacks on IoFT.
	- Publicly available network traffic datasets are emulated and not real test setup.
	- Creates dataset targeting Ryze Tello Drone
	- Dataset: https://github.com/iMohi/ECU-IoFT
	- **Contribution:**
		- Cyber vulnerability analysis of an off-the-shelf low-cost drone used in educational purpose.
		- Risk associated of using vulnerable drones.
		- Simulation of three cyber attacks on IoFT scenario.
		- Development of benchmark dataset capturing network traffic.
		- Performance analysis of most popular anomaly detection algorithms using developed dataset.
		- Future research directions of IoFT cyber security.
- # Dataset Development
	- > a purpose-made IoFT dataset needs to be created to adequately identify security threats targeted by Low-end consumer IoFT devices, often used within the education sector.
	- Development followed the remote grey box penetration test philosophy
		- Penetration test is considered a grey box when some but not all of the information and internal workings of the target is known.
		- Eg. Knowing the drone being targeted without knowledge of inner workings.
	- Pre-engagement -> Information gathering -> Threat modeling -> Vulnerability analysis -> Exploitation -> Post exploitation -> Reporting
	- **Environment:**
		- Ryze Tello TLW004 running firmware version 01.04.92.01.
		- UAV controlled via Google Pixel 2 - Android 10 (QQ3A.200805.001) - Tello app (1.6.0.0).
		- Attack machine running Kali Virtual Machine build 2021.2 within VMware Workstation Pro 16.1.2.
	- **Attacks:**
		- Wi-Fi Deauthentication Attack.
		- WPA2-PSL Wi-Fi Cracking Attack.
		- Tello API Exploit.
- # Evaluation
	- It is drone type dependent, so collection and testing with other drones is also required.