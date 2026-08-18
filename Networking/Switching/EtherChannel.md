- EtherChannel is used to allow redundant links between devices that have been blocked by STP.
- Groups multiple physical Ethernet links together into one single logical link
- Used to provide fault-tolerance, load sharing, increased bandwidth and redundancy between switches, routers and server.
- When an EtherChannle is configured, the resulting virtual interface is called a port channel.
# Limitations
EtherChannel implementation on the catalyst 2960 switch has certain implementation restrictions, including the following:

- Interface types cannot be mixed. For example, Fast Ethernet and Gigabit Ethernet cannot be mixed within a single EtherChannel.  

- Currently each EtherChannel can consist of up to eight compatibly-configured Ethernet ports. EtherChannel provides full-duplex bandwidth up to 800 Mbps (Fast EtherChannel) or 8 Gbps (Gigabit EtherChannel) between one switch and another switch or host.  

- The Cisco Catalyst 2960 Layer 2 switch currently supports up to six EtherChannels. However, as new IOSs are developed and platforms change, some cards and platforms may support increased numbers of ports within an EtherChannel link, as well as support an increased number of Gigabit EtherChannels.  

- The individual EtherChannel group member port configuration must be consistent on both devices. If the physical ports of one side are configured as trunks, the physical ports of the other side must also be configured as trunks within the same native VLAN. Additionally, all ports in each EtherChannel link must be configured as Layer 2 ports.  

- Each EtherChannel has a logical port channel interface, as shown in the figure. A configuration applied to the port channel interface affects all physical interfaces that are assigned to that interface.
# Auto Negotiation Protocols
EtherChannels can be formed through negotiations using one of two protocols:
- Port Aggregation Protocol (PAgP)
- Link Aggregation Control Protocol (LACP)
(Notes: It is possible to configure static or unconditional EtherChannel without the two mentioned protocols)
## Port Aggregation Protocol
- Aids in the automatic creation of EtherChannel links
- When a EtherChannel link is configured PAgP packets are sent between EtherChannel-capable ports to negotiate the forming of a channel
- Checks consistency
- When PAgP identified matched Ethernet links it groups the links into an EtherChannel, which is then added to the spanning tree as a single port
- All ports must have the same speed and duplex setting and VLAN information
**PAgP Modes**
- On - Forces interface to channel without PAgP
- PAgP desirable - Places an interface in an active negotiating state which the interface initiates negotiations with other interfaces
- PAgP auto - Places an interface in a passive negotiating state which the interface responds to the PAgP packets that is receives but does not initiate PAgP negotiation
**EXAMPLE**
Setup:
![[Pasted image 20260407221749.png]]

| S1        | S2             | Channel Establishment |
| --------- | -------------- | --------------------- |
| On        | On             | Yes                   |
| On        | Desirable/Auto | No                    |
| Desirable | Desirable      | Yes                   |
| Desirable | Auto           | Yes                   |
| Auto      | Desirable      | Yes                   |
| Auto      | Auto           | No                    |
## Link Aggregation Control Protocol
- Allows several physical ports to be bundled to form a single logical channel
- Can be used to facilitate EtherChannels in multivendor environments
- Provides the same negotiation benefits as PAgP
**Modes**
- On - Forces interface to channel without LACP (No exchanging packets)
- LACP active - Places a port in an active negotiating state (Initiates)
- LACP passive - Places a port in a passive negotiating state (Does not initiate)
**EXAMPLE**
Setup:
![[Pasted image 20260407222718.png]]

| S1      | S2             | Channel Establishment |
| ------- | -------------- | --------------------- |
| On      | On             | Yes                   |
| On      | Active/Passive | No                    |
| Active  | Active         | Yes                   |
| Active  | Passive        | Yes                   |
| Passive | Active         | Yes                   |
| Passive | Passive        | No                    |
# Configuration
## Guidelines
- **EtherChannel support** - All Ethernet interfaces must support EtherChannel with no requirement that interfaces be physically contiguous.
- **Speed and duplex** - Configure all interfaces in an EtherChannel to operate at the same speed and in the same duplex mode.
- **VLAN match** - All interfaces in the EtherChannel bundle must be assigned to the same VLAN or be configured as a trunk (shown in the figure).
- **Range of VLANs** - An EtherChannel supports the same allowed range of VLANs on all the interfaces in a trunking EtherChannel. If the allowed range of VLANs is not the same, the interfaces do not form an EtherChannel, even when they are set to **auto** or **desirable** mode.

The figure shows a configuration that would allow an EtherChannel to form between S1 and S2.
![[Pasted image 20260407222931.png]]

In the next figure, S1 ports are configured as half duplex. Therefore, an EtherChannel will not form between S1 and S2.
![[Pasted image 20260407222948.png]]
- If these settings must be changed, configure them in port channel interface configuration mode
- Any configuration that is applied to the port channel interface also affects individual interfaces
- Configurations that are applied to the individual interfaces do not affect the port channel interface
- Making configuration changes to an interface that is part of an EtherChannel link may cause interface compatibility issues.
- The port channel can be configured in access mode, trunk mode (most common), or on a routed port
## Example Configuration
![[Pasted image 20260407223134.png]]

**Steps**
1. Specify the interfaces the compose the EtherChannel group using the **interface range *interface*** command.
2. Create the port channel interface with the **channel-group *identifier* mode active** command
3. To change Layer 2 settings on the port channel interface, enter port channel interface configuration mode using the **interface port-channel** command, followed by the interface identifier
```
interface range FE0/1-2
channel-group 1 mode active
exit

interface port-channel 1
switchport mode trunk
switchport trunk allowed vlan 1,2,20
```
(Note: To remove channel-group mode use `no channel-group` on the interface)
# Verify
- Display the general status of the port channel interface - `show interfaces port-channel`
- Display one line of information per port channel - `show etherchannel summary`
- Display information about specific port channel interface - `show etherchannel port-channel`
- Provide information about the role of the interface - `show interface f0/1 etherchannel`

# EtherChannel Configuration Guidelines and Restrictions

EtherChannel has some specific guidelines that must be followed in order to avoid configuration problems.

1)    All Ethernet interfaces support EtherChannel up to a maximum of eight interfaces with no requirement that the interfaces be on the same interface module.

2)    All interfaces within an EtherChannel must operate at the same speed and duplex.

3)    EtherChannel links can function as either single VLAN access ports or as trunk links between switches.

4)    All interfaces in a Layer 2 EtherChannel must be members of the same VLAN or be configured as trunks.

5)    If configured as trunk links, Layer 2 EtherChannel must have the same native VLAN and have the same VLANs allowed on both switches connected to the trunk.

6)    When configuring EtherChannel links, all interfaces should be shutdown prior to beginning the EtherChannel configuration. When configuration is complete, the links can be re-enabled.

7)    After configuring the EtherChannel, verify that all interfaces are in the up/up state.

8)    It is possible to configure an EtherChannel as static, or for it to use either PAgP or LACP to negotiate the EtherChannel connection. The determination of how an EtherChannel is setup is the value of the **channel-group** _number_ **mode** command. Valid values are:

**active** LACP is enabled unconditionally

**passive** LACP is enabled only if another LACP-capable device is connected.

**desirable** PAgP is enabled unconditionally

**auto** PAgP is enabled only if another PAgP-capable device is connected.

**on** EtherChannel is enabled, but without either LACP or PAgP.

9)    LAN ports can form an EtherChannel using PAgP if the modes are compatible. Compatible PAgP modes are:

**desirable => desirable**

**desirable => auto**

If both interfaces are in **auto** mode, an Etherchannel cannot form.

10)  LAN ports can form an EtherChannel using LACP if the modes are compatible. Compatible LACP modes are:

**active => active**

**active => passive**

If both interfaces are in **passive** mode, an EtherChannel cannot form using LACP.

11)  Channel-group numbers are local to the individual switch. Although this activity uses the same Channel-group number on either end of the EtherChannel connection, it is not a requirement. Channel-group 1 (interface po1) on one switch can form an EtherChannel with Channel-group 5 (interface po5) on another switch.