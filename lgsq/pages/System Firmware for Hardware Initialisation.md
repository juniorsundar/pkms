# Basic Input/Output System (BIOS)
id:: 65f5abe1-3fd0-4d2c-b140-a209e3e73979
	- ## Definition
		- It is a type of firmware used during the booting process (power-on startup) on PCs. The BIOS is a crucial component of computer systems because it performs hardware initialization during the booting process and provides runtime services for operating systems and programs. The BIOS is stored on a ROM chip on the motherboard.
		- BIOS firmware has been replaced in many systems by UEFI (Unified Extensible Firmware Interface)
	- ## Key Functions
		- **Initialization** - When a computer is powered on, the BIOS performs a Power-On Self Test (POST) to check and initialize system hardware components such as the processor, memory, disk drives, and other hardware connected to the motherboard.
		  logseq.order-list-type:: number
		- **Boot Process** - After initializing the hardware, the BIOS identifies and prioritizes available boot devices (like hard drives, CD/DVD drives, or USB drives) according to the system configuration and attempts to boot the system from them.
		  logseq.order-list-type:: number
		- **BIOS Setup** - It provides a setup utility that allows users to configure hardware settings such as system time and date, boot order, and various hardware parameters. This utility is usually accessed by pressing a specific key (like F2, F10, Delete) during the boot process.
		  logseq.order-list-type:: number
		- **Interface for System Services** - BIOS provides a set of low-level interfaces that operating systems and software applications can use to interact with hardware devices, which is especially important during the early stages of the system startup before the operating system has fully loaded.
		  logseq.order-list-type:: number
- # Unified Extensible Firmware Interface (UEFI)
  id:: 65f5acb6-8065-4120-b6ae-2eefb6328255
	- ## Definition
		- UEFI stands for Unified Extensible Firmware Interface. It is a modern specification for motherboard firmware that serves as a replacement for the traditional BIOS (Basic Input/Output System). UEFI offers a number of improvements and new features compared to BIOS, making it more suited to modern computing needs.
	- ## Key Features
		- **Graphical User Interface (GUI)** - Unlike the text-based BIOS setup utility, UEFI firmware often includes a graphical user interface (GUI) that makes it easier for users to configure settings and navigate through menus.
		  logseq.order-list-type:: number
		- **Secure Boot** - Introduces the Secure Boot feature, which helps protect the system against malware by ensuring that only signed, trusted software can boot. This is particularly useful for preventing rootkits and other low-level malware infections.
		  logseq.order-list-type:: number
		- **GPT Support** - Supports GUID Partition Table (GPT)
		  logseq.order-list-type:: number
		- **Faster Boot Times** - Can reduce boot times through its efficient management of the boot process and its ability to load from drivers and EFI (Extensible Firmware Interface) applications directly, without the need for a bootloader.
		  logseq.order-list-type:: number
		- **Network Booting** - Improves on network booting capabilities with support for the UEFI Preboot eXecution Environment (PXE), allowing computers to download and execute an operating system from a server over a network.
		  logseq.order-list-type:: number
		- **Modular Design** - Its architecture is modular, meaning that manufacturers can easily add drivers and applications to the firmware, enhancing hardware compatibility and allowing for more detailed hardware monitoring and configuration.
		  logseq.order-list-type:: number
		- **Backwards Compatibility** - Many UEFI implementations include a compatibility support module (CSM) that allows them to boot operating systems designed for BIOS, ensuring that older operating systems and software can still be used.
		  logseq.order-list-type:: number