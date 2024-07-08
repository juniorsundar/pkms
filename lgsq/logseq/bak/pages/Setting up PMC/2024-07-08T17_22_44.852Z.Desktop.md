# Steps to connect to WIFI (from Comms Module)
	- ```bash
	  nano /etc/wpa_supplicant.conf
	  # network {
	  #   ssid="SRTA"
	  #   psk="ssrcsrta2024"
	  # }
	  ```
	- ```bash
	  wpa_supplicant -i wlan0 -c /etc/wpa_supplicant.conf -B
	  ```
	- ```bash
	  udhcpc -i wlan0
	  ```
	- ```bash
	  route add default gw 192.168.80.1 wlan0 # This is the internet gateway
	  ```
- # Forwarding Connection -> `give_internet.sh`
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