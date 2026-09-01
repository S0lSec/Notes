# Standard Numbered ACLs
(1-99 & 1300-1999)
- Matches only the source IP of the packet
- Each ACL contains a list of commands
- Each command contains a matching and action logic
- Packets are matches against ACL statements in sequential order. Meaning they allow or deny decision is based on the first matching statement.

- Using a wildcard mask you can allow a range of IP addresses
- A implicit deny is active, but you can implement a implicit allow.

`Access-list 1, if Source IP is 172.16.10.10, then deny`
Match -> `172.16.10.10`
Action -> `deny`
ACL number -> `1`

**Access Control Entry (ACE)** are used to control entry based on an IP address 
e.g. `accesslist 1 deny 172.16.10.10`
e.g. `accesslist 1 permit 172.16.10.10`

```
! Configuration
R1(config)# access-list 1 permit host 172.16.10.20
R1(config)# access-list 1 deny host 172.16.10.10
R1(config)# exit

R1(config)# int g0/1
R1(config-if)# ip access-group 1 out 

! Implicit allow/deny
R1(config)# access-list 1 permit any

! Use wildcard to allow a IP range
R1(config)# access-list 1 deny 17.26.16.0 0.0.0.255
```

# Standard Named ACLs
- Uses names instead of numbers

```
! ip access-list <standard/extended> <name>
R1(config)# ip access-list standard block_pc1
R1(config-std-nacl)# permit 172.16.10.20
R1(config-std-nacl)# deny 172.16.10.10
R1(config-std-nacl)# exit

R1(config)# int g0/01
R1(config-if)# ip access-group block_pc1 out
```

When editing the ACL you must first delete the rule (if added to the end), then create a new rule but provide a location to add the rule. E.g.
```
R2# show access-list
Standard IP access-list BLOCK_PC1
	10 permit host 172.16.10.20
	20 deny host 172.16.10.10
	30 permit any
	40 deny host 172.16.10.100
	
! Editing
R2(config)# ip access-list standard BLOCK_PC1
R2(config-std-nacl)# no 40
R2(config-std-nacl)# 25 deny 172.16.10.100
R2(config-std-nacl)# exit

R2# show access-list
Standard IP access-list BLOCK_PC1
	10 permit host 172.16.10.20
	20 deny host 172.16.10.10
	25 deny host 172.16.10.100
	30 permit any
```
### Block SSH/Telnet
```
R1(config)# ip access-list standard BLOCK_REMOTE_ACCESS
R1(config-std-nacl)# deny 172.16.10.20
R1(config-std-nacl)# permit any
R1(config-std-nacl)# exit

R1(config) line vty 0 15
R1(config-line)# access-class BLOCK_REMOTE_ACCESS in
R1(config-line)# exit
```