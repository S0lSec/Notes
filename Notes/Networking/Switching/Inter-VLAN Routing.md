Inter-VLAN routing is the process of forwarding network traffic from one VLAN to another VLAN.

Three inter-VLAN routing options:
- **Legacy Inter-VLAN routing** - This is a legacy solution. It does not scale well.
- **Router-on-a-Stick** - This is an acceptable solution for a small to medium-sized network.
- **Layer 3 switch using switched virtual interfaces (SVIs)** - This is the most scalable solution for medium to large organizations.
# Legacy Inter-VLAN Routing
- Relied on using a router with multiple interfaces
- Each interface was connected to a switch port in different VLANs
- The interfaces served as the default gateways
![[Pasted image 20260406153605.png]]
# Router-on-a-Stick
- Only required one interface
- Interface is configured as an 802.1Q trunk and connected to a trunk port on a Layer 2 switch
- The subinterfaces are configured in software on a router
- Requires subinterface for each VLAN to be routed
![[Pasted image 20260406153731.png]]
## Configuration
1. Configure S1 and the VLANs with trunking
	1. Create and name the VLANs
	2. Create the management interface
	3. Configure access ports
	4. Configure trunking ports
2. Configure S2 (similar as S1, different addressing)
3. Configure Router
	1. Create subinterfaces with addresses and encapsulation
	2. Enable interface with subinterfaces
(Note: Encapsulation command configures the subinterface to respond to 802.1Q 
encapsulated traffic from the specified *vlan-id*)
(Note: Adding *native* add the end of the encapsulation command makes that VLAN the native for that interface)

**EXAMPLE**
![[Pasted image 20260406154142.png]]
```
!S1
!Initial Configuration
enable
configure terminal
hostname S1

! Create and name VLANs
vlan 10
name LAN10
vlan 20
name LAN20
vlan 99
name Management
exit

! Create the management interface
interface vlan 99
ip add 192.168.99.2 255.255.255.0
no shutdown
exit
ip default-gateway 192.168.99.1

!Configure access ports
interface fa0/6
switchport mode access
switchport access vlan 10
no shut
exit

!Configure trunking ports
interface fa0/1
switchport mode trunk
no shut

interface fa0/5
switchport mode trunk
no shut
end
```

```
!S2
!Initial Configuration
enable
configure terminal
hostname S2

! Create and name VLANs
vlan 10
name LAN10
vlan 20
name LAN20
vlan 99
name Management
exit

! Create the management interface
interface vlan 99
ip add 192.168.99.3 255.255.255.0
no shutdown
exit
ip default-gateway 192.168.99.1

!Configure access ports
interface fa0/18
switchport mode access
switchport access vlan 20
no shut
exit

!Configure trunking ports
interface fa0/1
switchport mode trunk
no shut
end
```

```
!R1
!Initial Configuration
enable
configure terminal
hostname R1

!Configure Subinterfaces
interface G0/0/1.10
description Default Gateway for VLAN 10
encapsulation dot1Q 10
ip add 192.168.10.1 255.255.255.0

interface G0/0/1.20
description Default Gateway for VLAN 20
encapsulation dot1Q 20
ip add 192.168.20.1 255.255.255.0

interface G0/0/1.99
description Default Gateway for VLAN 99
encapsulation dot1Q 99
ip add 192.168.99.1 255.255.255.0

interface G0/0/1
description Tunk list to S1
no shut
end
```
## Verification
1. Verify that the subinterfaces are appearing in the routing table of R1. `show ip route`
2. Check if interfaces are up. with the right IP addresses `show ip interface brief`
3. Verify subinterfaces. `show interfaces subinterface-id`
4. Check trunking port. `show interfaces trunk`
# Layer 3 Switch Routing 
- A Switches Virtual Interface (SVI) is configured on a Layer 3 switch
- Although configured on a switch SVI functions the same for a VLAN as a router interface would
![[Pasted image 20260406153930.png]]
## Configuration
1. Create VLANs
2. Create the SVI VLAN interfaces
3. Configure access ports
4. Enable IP routing

**EXMAPLE**
![[Pasted image 20260406160544.png]]
```
!D1
!Create VLANs
vlan 10
name LAN10
vlan 20
name LAN20
exit

!Create SVI VLAN interfaces
interface valn 10
description Default Gateway SVI for 192.168.10.0/24
ip add 192.168.10.1 255.255.255.0
no shut

interface valn 20
description Default Gateway SVI for 192.168.20.0/24
ip add 192.168.20.1 255.255.255.0
no shut

!Configure Access Ports
interface GigabitEthernet1/0/6
description Access port to PC1
switchport mode access
switchport access vlan 10

interface GigabitEthernet1/0/18
description Access port to PCC
switchport mode access
switchport access vlan 20
exit

!Enable IP routing
ip routing
```