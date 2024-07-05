# Requirements
	- Rugged Laptop - Dell Latitude 7330 Rugged Extreme with correct BIOS setting.
	- Comms Module 1.5
	- USB for etching Ghaf installation media
	- IX-Industrial Ethernet Cable (Comms Module -> Rugged Laptop)
	- XT30-Power Male Cable (Powering Comms Module)
	- Micro USB -> USB A/C Cable (for Raspberry Pi)
	- Router with Connection to the Internet (Read ((66879ca1-0e9a-43dd-8b0c-df4fed084332)) first!)
	- Laptop with TPM2.0 Security Chip (for Provisioning Server)
	- Ethernet Switch (optional, unless the Provisioning Laptop has Wireless Hotspot Capability)
	- 2x Ethernet Cables (optional, unless Provisioning Laptop has Wireless Hotspot Capability)
- # Setting Up Provisioning Network/Server
	- ## Generating Keys and Certificates
	- ## Configuring Provisioning Network/Server
- # Setting up Comms Module 1.5
	- ## Flashing `.img`
	- ## Configuring Network
- # Setting up Wireless Mesh Network
  id:: 66879ca1-0e9a-43dd-8b0c-df4fed084332
	- A wireless network with internet connection is mandatory for setting up the PMC.
	- All drones and PMC will be in this network, which will be the Mesh Network.
	- #+BEGIN_IMPORTANT
	  It is mandatory that the wireless network have the following IP format:
	  `192.168.X.X`
	  
	  Optimally, it will not have any other devices apart from just the swarm components and PMC connected to it to avoid IP clashes.
	  
	  If this cannot be facilitated (possibly because of local networking issues), it is best to obtain a router with sim and manually set up the gateway.
	  #+END_IMPORTANT
	-
- # Installing Ghaf
	- ## Create Installation Media
	- ## Flash Ghaf to PMC
	- ## Installation Process
	- ## Provisioning
		- ### via Wireless
		- ### via Switch
- # Registration and Pulling Containers
	- ## Expected Result
		- Upon reboot and connecting the Comms Module 1.5, the Rugged Laptop should automatically connect to the internet.
		- This can be verified with `ping 8.8.8.8` (if this doesn't work, then skip directly to ((66879d7f-5ecc-46c4-95d8-c2840950c717))).
		- Further verification can be done by:
			- ```bash
			  ssh 192.168.101.11 # docker vm
			  # username: ghaf
			  # password: ghaf
			  ```
			- ```bash
			  # from within docker vm
			  ls /var/lib/fogdata
			  # output should contain:
			  # certs/
			  # hostname
			  # ip-address
			  # docker-compose.yml (FROM REGISTRATION)
			  # PAT.pat (FROM REGISTRATION)
			  ```
		- If all the files and folders are present, then restart the container downloading process:
			- ```bash
			  # from within docker vm
			  journalctl -f -u fmo-dci.service
			  ```
	- ## What if there isn't Automatic Internet Connection?
	  id:: 66879d7f-5ecc-46c4-95d8-c2840950c717
		- ### Diagnosing Issue
			- `ssh` into the `netvm` of the PMC:
				- ```bash
				  ssh 192.168.101.1
				  ```
			- Connect the Micro USB cable to the Debug port of the Comms Module and attach a shell to it from the connected computer:
				- ```bash
				  picocom /dev/ttyUSB0 -b 115200
				  # username: root
				  # password: root
				  ```
			- Run `ifconfig` in the Comms Module and in the `netvm` of PMC.
			- As of now, I have observed two possible instances for this problem.
			- **Diagnosis 1:** Check if the Comms Module is connected to PMC
				- Run `ping <br-lan ip>` from Comms Module.
				- If successful, then they are connected.
				- If not, then there is probably an issue with the physical connection -> Change cable or ensure it is plugged in fully.
			- **Diagnosis 2:** Check if there is internet connection in Comms Module
				- This is most common issue.
				- Run `ping 8.8.8.8` from Comms Module.
				- If successful, then there is internet on Comms Module, but it is not being bridged into the `br-lan` port. Skip to ((66878af8-5348-4a99-bbac-2530feebedcc)).
				- If unsuccessful, then there isn't a Wi-Fi internet connection. Continue onwards.
		- ### Steps to connect to WIFI (from Comms Module)
			- We need to instantiate a wireless connection.
			- For this, obtain the ESSID and Password for the Wireless Mesh network with internet connection.
			- In the Comms Module run:
				- ```bash
				  nano /etc/wpa_supplicant.conf
				  # Edit or add the following lines:
				  # network {
				  #   ssid="SRTA"
				  #   psk="<password>"
				  # }
				  ```
				- ```bash
				  wpa_supplicant -i wlan0 -c /etc/wpa_supplicant.conf -B
				  ```
				- ```bash
				  udhcpc -i wlan0
				  ```
				- ```bash
				  route add default gw 192.168.X.1 wlan0
				  # This is the internet gateway. Replace X with appropriate 
				  # obtained from Router IP/Gateway
				  ```
			- Run `ping 8.8.8.8` from Comms Module. It should now be working
		- ### Forwarding Connection -> `give_internet.sh`
		  id:: 66878af8-5348-4a99-bbac-2530feebedcc
			- The gist of the connection is that the Internet connection from the `wlan0` port is brided to the `br-lan` port, which makes it available in the PMC.
			- But, for whatever reason, this isn't happening. We created a crude solution that can recreate this.
			- Run the following in the Comms Module:
				- ```bash
				  # Enable IP masquerading for traffic from br-lan to wlan0
				  iptables -t nat -A POSTROUTING -o wlan0 -j MASQUERADE
				  
				  # Allow forwarding of established and related connections
				  iptables -A FORWARD -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT
				  
				  # Allow forwarding from br-lan to wlan0
				  iptables -A FORWARD -i br-lan -o wlan0 -j ACCEPT
				  
				  # Allow forwarding from wlan0 to br-lan
				  iptables -A FORWARD -i wlan0 -o br-lan -j ACCEPT
				  ```
				- This can be automated with a `give_internet.sh`.
			- With this, you should be able to `ping 8.8.8.8` from PMC and receive internet connection.
			- Run `journalctl -f -u fmo-dci.service` from docker vm to reinitialise container downloads.