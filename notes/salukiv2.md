



# Setting up the Saluki V3



## Nvidia Jetson Orin NX Wake Up Guide



### Software Toolkit Setup


Download the Driver Package and Sample Root Filesystem from this [link](https://developer.nvidia.com/embedded/jetson-linux-archive).
- `Jetson_Linux_R35.3.1_aarch64.tbz2`
- `Tegra_Linux_Sample-Root-Filesystem_R35.3.1_aarch64.tbz2`

Create a directory to work in and move the downloaded files to that
directory. Then, change into this working directory.

Install the dependencies:
```bash
sudo apt-get update && sudo apt install qemu-user-static -y
```

Untar the file and assemble the root file system:
```bash
tar xf Jetson_Linux_R35.3.1_aarch64.tbz2 --verbose

sudo tar xpf Tegra_Linux_Sample-Root-Filesystem_R35.3.1_aarch64.tbz2 -C Linux_for_Tegra/rootfs/ --verbose
cd Linux_for_Tegra/
sudo ./apply_binaries.sh

# This may cause an error because it requires python.
# Most modern systems have phased out python for python3.
# Simply rerun it after replacing the python with python3.
sudo ./tools/l4t_flash_prerequisites.sh
```


### Modify MB2 BTC File


Modify the file:
```bash
nano Linux_for_Tegra/bootloader/t186ref/BCT/tegra234-mb2-bct-misc-p3767-0000.dts
```

Change: `cvb_eeprom_read_size = <0x100>` --> `cvb_eeprom_read_size = <0x0>`


### Flashing Jetson Orin NX


Boot the Orin NX into recovery mode:
1. Power off the device
2. Switch the NV Rec dip switch (the lower switch at the side) to the UP
   Position
3. Connect the PC to the NV USB1 (Middle USB-C) port
4. Power on the device

Ensure that the device is in recovery (APX) mode by running the following
command in the PC:
```bash
lsusb | grep NVIDIA
```

This should show that NVIDIA is in one of the connected devices.

The Jetson Orin NX can now be flashed with the following command:
```bash
sudo ./tools/kernel_flash/l4t_initrd_flash.sh \
-- external-device nvme0n1p1 \
-c tools/kernel_flash/flash_l4t_external.xml -p "-c bootloader/t186ref/cfg/flash_t234_qspi.xml" \
--showlogs --network usb0 jetson-orin-nano-devkit internal
```


### Post-flashing


Once flashing is successful, optionally, you can set up a user account and log in.

To check the serial number of the module without HW disassembly, run:
```bash
cat /sys/firmware/devicetree/base/serial-number
```


## FOG Setup Guide



### Requirements


Ensure that the system this is being run on has docker installed. If that is
not ready, then take some time to install it.

A USB disk drive of at least 32 GB is required.

Having Tailscale installed would also be be helpful.


### Install `fog-hyper`


`fog-hyper` is the hypervisor component of the FOG system that runs VMs on
the drone. It also contains the installation media creation tool. The
`fog-hyper` binary should be available already to proceed.

```bash
chmod +x fog_linux-amd64

# Start installation
sudo ./fog_linux-amd64 debug setup

# secrets.ejson decryption key:
#
# Enter the following as decruption key:
## 0b940d474406309f3f56df9b84f0f6a2b8d1616d2d097fdd337d25a60bc427ce
```

Once `fog` is runnable from anywhere, the initial binary can be deleted `rm
fog_linux-amd64`.

Verify installation with `fog --version`, and a current dated version
should be outputted.


### Create Installation Media


Connect a USB drive and run `lsblk` to identify its mount point at `/dev/`.

Update the `fog-hyper` installation with:

```bash
sudo fog update v11.0.0-rc3
```

To create installation media, first identify which iteration of the
firmware will be installed:

```bash
sudo fog installer create-media --profile=nvidia-nx --site=uae /dev/ID --confirm
```


### Install FOG Software in the drone


**Note:** You will need a provisioning server for this step. Check with the
appropriate people for that.

Plug the installation USB stick to the drone in either the left-most or
central USB-C slot (this has to be done through a dock most likely).

When powering on the Nvidia now, there should be a screen with two icons on
top: a terminal, and an installer icon. Run the installer.

> username: ghaf
> password: |ghaf|

Run the command: `/home/ghaf/fog-stage1-wrapper.sh`

**Note:** In the tick box selection, select the first two, leave third
blank. For the type of FOG installation, only `cm-scan` is possible with
the devkit.

This will start the installation process. Follow the instructions as they
show up on the screen. Once it is done, power off and unplug the USB drive.


## Polarfire Flight Controller Setup


This is more or less similar to [setting up the Saluki V2](#srtasaluki-v2md).

Make sure that the PF MM switch is in the UP Position (it is the switch
above [the one here](#flashing-jetson-orin-nx)).

First zeroise with the V2 `MPFS_ICICLE_KIT_BASE_DESIGN.job`.

Second program with the V3 `MPFS_ICICLE_KIT_BASE_DESIGN.job`.

Third flash the bootloader `ssrc_saluki-v3_bootloader-1.1-23-g8e44177.elf`:
```bash
export SC_INSTALL_DIR=~/Microchip/SoftConsole-v2022.2-RISC-V-747

sudo SC_INSTALL_DIR=~/Microchip/SoftConsole-v2022.2-RISC-V-747 FPGENPROG=/usr/local/microchip/Program_Debug_v2023.1/Program_Debug_Tool/bin64/fpgenprog java -jar $SC_INSTALL_DIR/extras/mpfs/mpfsBootmodeProgrammer.jar --bootmode 1 --die MPFS250T ssrc_saluki-v3_bootloader-1.1-23-g8e44177.elf
```

Next certify with the RnD test keys:
```bash
python3 saluki-sec-scripts/cert_tool.py -s -k saluki-sec-scripts/test_keys/saluki-v3/ed25519_test_key.pem
```

And finally flash the firmware:
```bash
python3 ./tools/px_uploader.py ssrc_saluki-v3_default-1.14.0-308-g9f4fbbdc61.px4
```


___

[< return](#srtaindexmd) -  [index](#indexmd)

