# Secure Boot - Programming FPGA Image and Flashing Bootloader and Firmware
	- ## Programming FPGA Image
		- ### Requirements
			- [FPExpress](http://tinyurl.com/yzhycfch)
			- FlashPro Programmer V5 or V6
			- Saluki V2 with SysCon Adapter 2 with PolarFire JTAG Connector (ribbon cable as well)
		- ### Process
			- Run FPExpress as superuser
			  
			  ```bash
			  # Assume installation is at default location
			  sudo ./usr/local/microchip/Program_Debug_v2023.1/Program_Debug_Tool/bin/FPExpress
			  ```
			- _Project → New Job Project_
			- _Import FlashPro Express job file → Browse..._
			- Find and select the "MPFS_ICICLE_KIT_BASE_DESIGN.job" file to "zeroize" the FPGA
			- Select a _FlashPro Express job project location_ where the log files will be dumped. **NOTE** must be an empty folder.
			- In dropdown, select 'ZEROIZE_LIKE_NEW'
			- Click "RUN"
			- Conduct above steps again for the following two jobs:
				- "enable_user_key.job"
				- "full_build_uek1.job"
			- Select 'PROGRAM' in dropdown for both
			- #+BEGIN_NOTE
			  This will basically prepare bootloader as well and prepare the Saluki for the keys to unlock it.
			  #+END_NOTE
	- ## Certifying with Keys
		- ### Requirements
			- cert_tool.py
			- default_rdcert.json
			- ed2551_sign.py
			- px4_bin_ed25519_private.pem
		- ### Process
			- `cd` into the folder all the files above. Ensure that the Saluki V2 is connected through USB.
			- Run:
			  
			  ```bash
			  python3 -m pip install cryptography
			  ```
			- Then run:
			  
			  ```bash
			  python3 cert_tool.py px4_bin_ed25519_private.pem
			  ```
			- If successful, then the Saluki V2 will be mounted as USB device with 3 partitions.
	- ## Flashing Firmware (Pre-Built Firmware)
		- ### Requirements
			- ssrc_saluki-v2_custom_keys.px4
			- px_uploader.py
		- ### Process
			- Basically, we can only flash this pre-built firmware since it is compatible with the secure keys.
			- `cd` into the directory with the above two files.
			- Run:
			  
			  ```bash
			  python3 px_uploader.py ssrc_saluki-v2_custom_keys.px4
			  ```
			- If successful, then the Saluki V2 can be worked as a regular Pixhawk.
	- ## Flashing Firmware (Custom Firmware)
		- In this case, we need to build firmware with a new set of keys that can be verified with the keys in the bootloader and the FPGA (refer to [this]([[Secure Boot Validation]])).
		- We apply a patch that signs the keys into the firmware, and then build the px4-firmware.
		- ```bash
		  # Clone using SSH to avoid getting permission errors   
		  git clone --recursive git@github.com:tiiuae/px4-firmware-fc-only.git -b v1.13.3-1.0.0-rc5
		  
		  # Patch has to be applied to introduce the keys
		  cd px4-firmware-fc-only/Tools/saluki-sec-scripts
		  git am 0002-custom-keys-for-saluki-v2.patch
		  
		  # Build with the keys signed
		  cd ../../
		  export SIGNING_ARGS=Tools/saluki-sec-scripts/uae_tii_custom_keys/saluki-v2/px4_bin_ed25519_private.pem
		  ./build.sh ./build saluki-v2_custom_keys
		  ```