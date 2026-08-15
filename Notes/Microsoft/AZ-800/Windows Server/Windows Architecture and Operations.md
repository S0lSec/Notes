# Hardware Abstraction Layer
Windows computers use many different types of hardware. When the OS is installed it must be isolated from differences in hardware.

The basic Windows architecture is shown here:
![[Pasted image 20260801181437.png]]

- **Hardware Abstraction Layer (HAL)**: Software that handles communication between the hardware and the kernel.
- **Kernel**: Core of the OS, having control over the entire computer. Handles all I/O requests, memory and peripherals
# User Mode and Kernel Mode
There are two different mode in which a CPU operated when Windows is installed: **User mode** and **Kernel Mode**
![[Pasted image 20260801181813.png]]

| **User Mode**                            | **Kernel Mode**                      |
| ---------------------------------------- | ------------------------------------ |
| Applications                             | OS Code                              |
| Has no effect on kernel operations       | Has complete control over the device |
| Has no direct access to memory locations | Crashes can stop the computer        |
| Crashes are recoverable                  | Can directly access memory           |
# Windows File Systems
File System - How information is stored on storage media
- exFAT
	- Simple
	- Supported by many
	- Limited
	- Replaced by FAT16 and FAT32
- HFS+
	- Used on MAC OS
	- Not supported by WIndows
- EXT
	- Used by Linux
	- Not supported by Windows, but Windows can read from it
- NTFS
	- Most common
	- MAC OS needs special driver to write
# Alternate Data Streams
- NTFS stores files as a series of attributes
- The data which the file contains is stored in the attribute $DATA, which is known as a data stream
- You can connect Alternate Data Streams (ADSs) to the file, which is sometimes used to store additional info
# Windows Boot Process
A boot process is the process that occurs between turning on a device and OS being fully loaded.
Windows boot process looks like this:
![[Pasted image 20260801185119.png]]
## Firmware
- **Basic Input-Output System (BIOS)**: Difficult to support all new features requested by users these days
- **Unified Extensible Firmware Interface (UEFI)**: Designed to replace BIOS and support new features
# Windows Registry
Windows stores all of the information about hardware, applications, users and system settings in a large database known as the registry.

The registry is a hierarchical database where the highest level is known as a hive, below that there are keys, followed by subkeys.

| **Registry Hive**          | **Description**                                                          |
| -------------------------- | ------------------------------------------------------------------------ |
| HKEY_CURRENT_USER (HKCU)   | Holds information concerning the currently logged in user                |
| HKEY_USERS (HKCU)          | Holds information concerning all the user accounts on the host           |
| HKEY_CLASSES_ROOT (HKCR)   | Holds information about object linking and embedding (OLE) registrations |
| HKEY_LOCAL_MACHINE (HKLM)  | Holds system-related information                                         |
| HKEY_CURRENT_CONFIG (HKCC) | Holds information about the current hardware profile                     |