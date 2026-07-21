# Mitigate MAC Address Table Attacks
- Limits the number of valid MAC addresses allowed on a port.
- Only allow learned or configured addresses
![[Pasted image 20260511102837.png|551]]
## Enabling Port Security
```
interface f0/1
switchport port-security
!If port is a dynamic port set it to static first
switchport mode access
switchport port-security
```
Troubleshooting: `show port-security interface f0/1`
Set max # of MAC addr: `switchport port-security maximum <value>`
### Add MAC Addresses
Manually: `switchport port-security mac-address <mac-address>`+
Dynamically Sticky: `switchport port-security mac-address sticky`
(Learn addresses and stick them to the running-config)
# Port Security Aging
(Aging timer that automatically removes inactive entries from dynamic tables)
**Types**
- **Absolute** - Secure addresses on the port are deleted after the specified aging time
- **Inactivity** - Secure addresses on the port are deleted on if they are inactive for the specified aging time

Enable or disable static aging for the secure port, or set the aging time/type:
`switchport port-security aging { static | time _time_ | type {absolute | inactivity}`

| **Parameter**   | **Description**                                                                                                                                                        |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| static          | Enable aging for statically configured secure addresses on this port                                                                                                   |
| time *time*     | Specify the aging time for this port. The range is 0 - 1400min. If the time is 0 aging is disabled for this port                                                       |
| type absolute   | Set the absoulte aging time. All the secure addresses on this port age out exactly after the time (in min) specified and are removed from the list                     |
| type inactivity | Set the inactivity aging type. The secure addresses on this port age out only if there is no data traffic from the secure source address for the specified time period |
## Example:
```
S1(config)# interface fa0/1
S1(config-if)# switchport port-security aging time 10
S1(config-if)# switchport port-security aging type inactivity
S1(config-if)# end
S1# show port-security interface fa0/1
Port Security              : Enabled
Port Status                : Secure-up
Violation Mode             : Shutdown
Aging Time                 : 10 mins
Aging Type                 : Inactivity
SecureStatic Address Aging : Disabled
Maximum MAC Addresses      : 2
Total MAC Addresses        : 2
Configured MAC Addresses   : 1
Sticky MAC Addresses       : 1
Last Source Address:Vlan   : a41f.7272.676a:1
Security Violation Count   : 0
S1#
```
# Port Security Violations Modes
| **Mode** | **Description**                                                                                        |
| -------- | ------------------------------------------------------------------------------------------------------ |
| shutdown | Shuts down the port                                                                                    |
| restrict | Drops packets with unknown source address until you remove a sufficient number of secure mac addresses |
| protect  | Drops packets with unknown source address until you remove a sufficient number of secure MAC addresses |
## Comparison
| **Violation Mode** | **Discards Offending Traffic** | **Sends Syslog Msg** | **Increase Violation Counter** | **Shuts Down Port** |
| ------------------ | ------------------------------ | -------------------- | ------------------------------ | ------------------- |
| Protect            | yes                            | no                   | no                             | no                  |
| Restrict           | yes                            | yes                  | yes                            | no                  |
| Shutdown           | yes                            | yes                  | yes                            | yes                 |
## Example
```
S1(config)# interface f0/1
S1(config-if)# switchport port-security violation restrict
S1(config-if)# end
S1#
S1# show port-security interface f0/1
Port Security              : Enabled
Port Status                : Secure-up
Violation Mode             : Restrict
Aging Time                 : 10 mins
Aging Type                 : Inactivity
SecureStatic Address Aging : Disabled
Maximum MAC Addresses      : 2
Total MAC Addresses        : 2
Configured MAC Addresses   : 1
Sticky MAC Addresses       : 1
Last Source Address:Vlan   : a41f.7272.676a:1
Security Violation Count   : 0
S1#
```
# Verify Port Security
`show port-security`
`show port-security insterface f0/1`
# Mitigate VLAN Hopping
1. Disable DTP
2. Disable unused ports
3. Put unused ports in a unused VLAN
4. Manually enable the trunk line on a trunking port
5. Set the native VLAN to anything other than 1
# Mitigate DCHP Starvation Attacks
DHCP spoofing attacks can be mitigated by using DHCP snooping on trusted ports.

DHCP snooping determines whether DHCP messages are from an administratively configured trusted or untrusted source. It then filters messages and rate-limits DHCP traffic from untrusted sources.
## Implementation
1. Enable DHCP snooping by using the `ip dhcp snooping` global configuration command
2. On trusted ports use the `ip dhcp snooping trust` interface configuration command
3. Limit the number of DHCP discover messages that can be received per second on untrusted ports by using the `ip dhcp snooping limit rate` interface configuration command
4. Enable DHCP snooping by VLAN or by a range of VLANs by using the `ip dhcp snooping <vlan>` global configuration command
# Mitigate ARP Attacks
Dynamic ARP inspection (DAI) requires DHCP snooping and helps prevent ARP attacks by:
- Not relaying invalid or gratuitous ARP Requests out to other ports in the same VLAN.
- Intercepting all ARP Requests and Replies on untrusted ports.
- Verifying each intercepted packet for a valid IP-to-MAC binding.
- Dropping and logging ARP Requests coming from invalid sources to prevent ARP poisoning.
- Error-disabling the interface if the configured DAI number of ARP packets is exceeded.

To mitigate the chances of ARP spoofing and ARP poisoning, follow these DAI implementation guidelines:
- Enable DHCP snooping globally.
- Enable DHCP snooping on selected VLANs.
- Enable DAI on selected VLANs.
- Configure trusted interfaces for DHCP snooping and ARP inspection.
## Configuration
```
S1(config)# ip dhcp snooping
S1(config)# ip dhcp snooping vlan 10
S1(config)# ip arp inspection vlan 10
S1(config)# interface fa0/24
S1(config-if)# ip dhcp snooping trust
S1(config-if)# ip arp inspection trust
```

DAI can also be configured to check for both destination or source MAC and IP addresses:
- **Destination MAC** - Checks the destination MAC address in the Ethernet header against the target MAC address in ARP body.
- **Source MAC** - Checks the source MAC address in the Ethernet header against the sender MAC address in the ARP body.
- **IP address** - Checks the ARP body for invalid and unexpected IP addresses including addresses 0.0.0.0, 255.255.255.255, and all IP multicast addresses.
```
S1(config)# ip arp inspection validate ?
dst-mac  Validate destination MAC address
  ip       Validate IP addresses
  src-mac  Validate source MAC address
S1(config)# ip arp inspection validate src-mac
S1(config)# ip arp inspection validate dst-mac
S1(config)# ip arp inspection validate ip
S1(config)# do show run | include validate
ip arp inspection validate ip
S1(config)# ip arp inspection validate src-mac dst-mac ip
S1(config)# do show run | include validate
ip arp inspection validate src-mac dst-mac ip
S1(config)#
```
# Mitigate STP Attacks
Attackers can spoof the root bridge and change the topology of a network.
To mitigate STP attacks use PortFast and Bridge Protocol Data Unit (BPDU) Guard
- **PortFast** - PortFast immediately brings an interface configured as an access port to the forwarding state from a blocking state, bypassing the listening and learning states. Apply to all end-user ports. PortFast should only be configured on ports attached to end devices.
- **BPDU Guard** - BPDU guard immediately error disables a port that receives a BPDU. Like PortFast, BPDU guard should only be configured on interfaces attached to end devices.

If portFast is enables on a port connecting to another switch, there is a risk of creating a spanning-tree loop.

Enable PortFast on interface: `spanning-tree portfast`
Enable PortFast globally: `spanning-tree portfast default`

Verify PortFast enabled: `show spanning-tree summary`
## Configure BPDU Guard
Even though PortFast is enabled the interface will still listen for BPDUs.
**Always enable BPDU Guard on all PortFast-enabled ports**

Enable on interface: `spanning-tree bpduguard enable`
Enable globally: `spanning-tree portfast bpduguard default`