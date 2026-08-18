# Windows Requirements
**EFI Storage**
Extensible Firmware Interface is a system partition used by windows. This is a required system partition when using a UEFI boot OS
**TPM**
Trusted Platform Module (is normally a chip on a motherboard) acts as a cryptographic key used by OS  for data protection, encryption and other security purposes
**VirtIO Drivers**
Windows does not come with drivers for virtualized hardware. These drivers solve this problem
# Creating VM
(Note: This only explains abnormal things)
- Create a tag named *WIndows*
- Check *Start at boot*
- Add additional drive for VirtIO Drivers
- Add EFI & TPM storage
- Create a second disk and set *Bus/Device* to *SATA*
# Installing Windows
(Note: This only explains abnormal things)
- Click on drive and click *Load drivers*
- If you have no internet:
	- Shift+F10 or Monitor and send Shift+F10
	- `OOBE\BYPASSNRO` in cmd
- Go to virtIO drive and install drivers & guest tools
- Enable QEM Guest Agent