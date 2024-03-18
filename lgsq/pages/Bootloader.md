# Definition
	- Also known as a boot manager, it is a small program that loads the operating system kernal of a computer into memory.
	- Boot loaders are essential for starting computers and devices, acting as a bridge between the firmware and the operating system. They can be specific to an operating system or universal, capable of booting multiple OSes.
- # Key Functions
	- **Initialisation** - Upon power-on, the BIOS of UEFI firmware initialises the hardware components and searches for a boot device that has a boot loader.
	- **OS Selection** - On systems with multiple OSs, the boot loader presents a menu that allows the user to select which OS they wish to boot into.
	- **Kernel Loading** - It then loads the kernel into memory. Kernel is the core component of the operating system that manages system resources and hardware interactions.
	- **Transfer of Control** - After loading the kernel, boot loader transfers control to it, allowing the operating system to start and manage the computer's resources.
	- **Configuration and Options** - Boot loaders also allow advanced options for kernel parameters, troubleshooting modes, and system recovery options.