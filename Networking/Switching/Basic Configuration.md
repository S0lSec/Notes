# Initial Setup
1. Hostname
2. Disable DNS lookup
3. Add banner
4. Add password for enable
5. Add password for console
6. Add password for VTY lines
7. Encrypt passwords
8. Write configuration
9. Set Clock
10. Copy configuration
```
enable
configure terminal

hostname S1
no ip domain lookup

enable secret class

line console 0
password cisco
login
exit

line vty 0 15
password cisco
login
exit

service password-encryption
banner motd # Authorized access only! #
exit

wr

clock set 13:21:00 16 April 2026

copy running-config startup-config
```
# Ports
- Full-duplex - Allows communication both ways (send and receive)
- Half-duplex - Allows communication one way (send or receive)
- Can not use both on a single connection.
- Speed must also be configured when configuring port, ensure speeds are the same on both ends.

When connecting devices either straight-through or crossover cables are required. Straight-through are for intermediary to end devices and crossover cables are for intermediary to intermediary.

**Auto-MDIX** removes the need for specific cables letting you use either to connect devices. (Is usually enabled by default, `mdix auto` if need to manually enable, `show controllers ethernet-controller fa0/1 phy | include MDIX` to view status)
## Configuring port
1. configure terminal
2. interface FastEthernet 0/1
3. duplex full
4. speed 100
5. end
# SSH
0. Verify SSH support - `show ip ssh`
1. Configure IP domain - `ip domain name cisco.com`
2. Generate RSA key pairs - `crypto key generate rsa general-keys modulus {size}`
3. Configure user authentication - `username admin secret ccna`
4. Configure VTY lines 
	1. `line vty 0 15`
	2. `transport input ssh`
	3. `login local`
	4. `exit`
5. Enable SSH version 2 - `ip ssh version 2`
