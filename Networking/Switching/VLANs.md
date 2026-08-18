A VLAN or Virtual Local Area Network is a logical segment of a network, which can be used to help with organization, security and performance.
![[Pasted image 20260406133256.png]]

Each VLAN in a switched network corresponds to an IP network. Therefore VLAN design must take into consideration the implementation of a hierarchical network-addressing scheme.
![[Pasted image 20260406133419.png]]

# Types of VLANs
## Default VLAN
- VLAN 1
- All switchports are on VLAN 1 unless changed
- Insecure
## Data VLAN
- Configured to separate user-generated traffic
- Separate the network into groups of users or devices
- Voice and network management traffic should not be permitted on data VLANs
## Native VLAN
- User traffic from a VLAN must be tagged with its VLAN ID when sent to another switch
- Trunk ports are used between switches to support the transmission of tagged traffic
- Best practice to configure native VLAN as an unused VLAN
- Carries untagged traffic on a trunk line
## Management VLAN
- Data VLAN configured for network management traffic
- (The VLAN with the IP address)
## Voice VLAN
- Used for Voice over IP (VoIP)
- VoIP requires:
	- Assured bandwidth to ensure voice quality
	- Transmission priority over other types of network traffic
	- Ability to be routed around congested areas on the network
	- Delay of less than 150ms across the network'
# Configure
## Create VLAN
1. configure terminal
2. vlan *vlan-id*
3. name *vlan-name*
4. end
## VLAN Port Assignment
1. configure terminal
2. interface *interface-id*
3. switchport mode access
4. switchport access vlan *vlan-id*
5. end
# Trunking
Used to allow VLAN traffic to travel across multiple switches.
Steps to configure trunking on a switch:
1. Connect the switches together
2. Set the connected port to trunking mode
3. Set the native vlan to something other than VLAN 1
4. Specify the allowed VLANs
5. 5. Repeat on other switches
```
configure terminal
interface FastEthernet 0/1
 switchport mode trunk
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,20
 end
```
## Dynamic Trunking Protocol
- Used to setup trunking automatically
- Not secure
- Not often used

Configuration:
1. Create VLANs
2. Set interface on main switch to dynamic desirable
3. Set interfaces on second switch to dynamic auto
