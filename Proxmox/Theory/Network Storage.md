# Networked Storage
(Note: Networked Storage is NAS)
- Allows a system to truly scale by connecting nodes together building clusters
- Enables key functionalities for business continuity purposes, such as node migration and high availability
- Needs higher investment to have the proper infrastructure
- Riskier since more things can become failure points
# Network File System (NFS)
- Allows admins to access shared storage over a network
![[Pasted image 20260514130718.png]]
# Common Internet File System (CIFS)
- Constantly paired with SMB
- (CIFS is an enhanced version of SMB)
- Requires a username + password to connect to
- Heavier on resources than NFS
![[Pasted image 20260514130737.png]]
# Internet Small Computer Systems Interface (iSCSI)
- Very robust (scalability & flexibility)
- Protocol to transfer data to and from a storage device via TCP/IP packets
- Shared disadvantages with NFS/CIFS
# Advanced Network Storage Options
## GlusterFS
- A cluster of shared network storage that ensures high availability between nodes. ​
- Really expensive to maintain the hardware needed.​
- File-level, has all content tags.​
## CephFS
- Built into PVE, uses node storage to create network arrays.​
- Critical to PVE’s HA capabilities; will be covered later.​
- CephFS is built on top of Ceph; paired with RBD.​
- File-level.
## RBD
- CephFS block-level counterpart; they complement each other.​
- Excels at managing heavy images and container files.​
- Links node storage in a single powerful array.​
- Resource-heavy, due to how powerful it can be.
# Advanced Network Storage Key Features
| **Feature/Storage​**   | **GlusterFS​** | **CephFS​** | **RBD​** |
| ------------------ | ---------- | ------- | ---- |
| Thin Provisioning​ | ​          | Yes​    | Yes​ |
| Snapshots​         | ​          | Yes​    | Yes​ |
| Replication​       | Yes​       | Yes​    | Yes​ |
| Compression​       | Yes​       | Yes​    | Yes​ |
| Deduplication​     | ​          | ​       | ​    |
| Dynamic Resizing​  | Yes​       | Yes​    | Yes​ |
| Encryption​        | Yes​       | Yes​    | Yes​ |
