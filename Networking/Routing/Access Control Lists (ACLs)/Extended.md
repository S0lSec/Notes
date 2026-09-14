- Numbered ACLs (100-1999 & 2000-2699)
- Named ACLs

Offers more control by using multiple header fields in a single ACE.
Matches via the source + destination IP & source + destination port and the protocol used.

When specifying protocol use **ip** to specify all
# Configuration
## Numbered
**Allow Host**
```
R1(config)# access-list 100 <action> <protocol> <source> <destination>
R1(config)# access-list 100 permit ip host 172.16.10.20 host 192.168.10.10
```

**Allow Subnet**
```
R1(config)# access-list 100 <action> <protocol> <source> <destination> <destination port>
R1(config)# access-list 100 permit tcp 172.16.10.0 0.0.0.255 192.168.10.10 0.0.0.0 eq 80 
```

**Full Example**
```
R1(config)# access-list 100 permit tcp host 172.16.10.20 host 192.168.10.10 eq 80 R1(config)# access-list 100 deny tcp host 172.16.10.10 host 192.168.10.10 eq 80 
R1(config)# access-list 100 permit ip any any 

R1(config)# interface gig 0/1
R1(config-if)# ip access-group 100 in
```
## Named
```
R1(config)# ip access-list extended HTTP_TRAFFIC

! Comment
R1(config-ext-nacl)# remark This ACL Manages HTTP Traffic

! Rules
R1(config-ext-nacl)# permit tcp host 172.16.10.20 host 192.168.10.10 eq 80
R1(config-ext-nacl)# deny tcp host 172.16.10.10 host 192.168.10.10 eq 80
R1(config-ext-nacl)# permit ip any any
R1(config-ext-nacl)# exit

! Attach to interface
R1(config)# interface gig 0/1
R1(config-if)# ip access-group HTTP_TRAFFIC in
```