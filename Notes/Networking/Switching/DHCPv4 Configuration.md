# Steps
1. Exclude IPv4 addresses
	- `ip dhcp excluded-address 102.168.10.1 192.168.10.9`
	- `ip dhcp excluded-address 192.168.10.254`
2. Define a DHCPv4 pool name
	- `ip dhcp pool LAN-POOL-1`
3. Configure the DHCPv4 pool
	1. Define the address pool
		- `network 192.168.10.0 255.255.255.0
	2. Define the default router/gateway
		- `default-router 192.168.10.1`
	3. Define a DNS server
		- `dns-server 192.168.11.5`
	4. Define the domain name
		- `domain-name example.com`
	5. Define the duration of lease
		- `lease {days [hours [ minutes]] | infinite}`
	6. Define the NetBIO WINS server
		- `netbios-name-server address`
# Verify
Displays the DHCPv4 commands configured on the router
	`show running-config | section dhcp`
Displays a list of all IPv4 address to MAC address bindings
	`show ip dhcp binding`
Displays count information regarding the number of DHCPv4 messages
	`show ip dhcp server statistics`
# Disable DHCPv4 Server
Disable  - `no service dhcp`
Enable - `service dhcp`