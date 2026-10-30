- Use Layer 3 switches for the core and distributions layers to reduce the need for STP.
- (STP can cause issues if configured improperly disconnecting networks)
- Better to use next-gen firewalls instead of routers
- Have a Layer 2 switch for each major section and use VLANs for segmentation and security

## 1. Access Layer
Enables end devices to connect to the network.
- L2 switches
- Hubs![[Pasted image 20261027123252.png]]

## 2. Distribution Layer
If a network becomes to large it should be divided into multiple local networks. The distribution layer connects these local networks together.
- Routers
- Layer 3 Switches
- VLANs are made in this area and trunks are used to allow the access layer to use these VLANs
![[Pasted image 20261027123244.png]]
## 3. Core Layer
Used to connect multiple distribution layer devices together.
Usually has high speeds (10GB).
Has as much redundant connects as possible.
![[Pasted image 20261027123233.png]]

## 4. Edge Layer
Used to connect the network to external entities such as the ISP.
![[Pasted image 20261027123223.png]]
## 5. Outside DMZ
Used to allow multiple edge routers/firewalls to connect to a single ISP.
Allows for high availability and redundancy.
![[Pasted image 20261027123159.png]]