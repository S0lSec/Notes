# Supported Features
- VPN
- Routing
- Web Application Proxy
	Provide reverse proxy functionality for users who must access their organizations internal web applications.
# VPNs
## Tunneling Protocols
**Point-to-Point Tunneling Protocol (PPTP)**
Encapsulates Point-to-Point Protocol (PPP) packets inside IP packets so they can travel across the internet. Creating a VPN tunneling between a client device and a VPN server.

**Layer 2 Tunneling Protocol with Internet Protocol Security (L2TP/IPSec)**
Combines tunneling and encryption to securely send data across the internet. L2TP creates the tunnel while IPSec provides the encryption and security.
Since L2TP itself does not encrypt data it is almost always used together with IPSec.

**Secure Socket Tunneling Protocol (SSTP)**
Sends VPN traffic through an encrypted HTTPS connection and is mainly used in Windows-based VPN environments.

**Internet Key Exchange version 2 (IKEv2)**
Used to establish and manage secure connections using IPsec.
(Is commonly refered to as IKEv2/IPsec since IKEv2 handles authentication and key exchange while IPsec provides encryption and data protection)
## Authentication Options
**PAP**
Uses plaintext passwords and is the least secure authentication protocol

**CHAP**
A challenge-response authentication protocol that uses the industry-standard MD5 hashing scheme to encrypt the response

**MS-CHAPv2**
same as CHAP

**EAP**
Arbitrary authentication mechanism authenticates a remote access connection

(Note: PKI can be used for remote access)

# Web Application Proxy (WAP)
A reverse proxy service that securely publishes internal web applications to users outside an organizations network.

1. **AD FS preauthentication:** Only authorized users can send data packets to the web application.
2. **Pass-through preauthentication:**
	1. User is connected to the web application through WAP
	2. WAP rebuilds the data packets as they are delivered to the web app
	3. Web app is responsible for authenticating users
3. **AD FS preauthentication benefits:**
	1. SSA
	2. MFA
	3. Multifactor access control