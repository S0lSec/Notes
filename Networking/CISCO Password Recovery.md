### 1. Enter the ROMMON mode
```
Readonly ROMMON initialized

monitor: command "boot" aborted due to user interrupt 
rommon 1 >
```
### 2. Change the configuration register
```
rommon 1 > confreg 0x2142
rommon 2 > reset

 System Bootstrap, Version 15.0(1r)M9, RELEASE SOFTWARE (fc1)
 Technical Support: http://www.cisco.com/techsupport
 Copyright (c) 2010 by cisco Systems, Inc.
 (output omitted)
```
### 3. Copy the startup-config to the running-config
```
Router# copy startup-config running-config
Destination filename [running-config]?

1450 bytes copied in 0.156 secs (9295 bytes/sec)
R1#
```
### 4. Change the password
```
R1# configure terminal
Enter configuration commands, one per line. End with CNTL/Z.
R1(config)#enable secret cisco
```
### 5. Save the running-config as the startup-config
```
R1(config)# config-register 0x2102
R1(config)# end
R1# copy running-config startup-config
Destination filename [startup-config]?
Building configuration...
[OK]
R1#
```
### 6. Reload the device
```
R1# reload
Proceed with reload? [confirm] 

*Mar 1 13:04:53.009: %SYS-5-RELOAD: Reload requested by console. Reload Reason: Reload Command.
```
