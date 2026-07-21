**BACKUP YOUR STUFF**
# VZDumps
- In-platform backup utility
**GUI**
Resource Tree > Object (Node VM) > Backup

**CLI**
Node-level backup​: `vzdump --all --storage <storage_id> --compress zstd​`
VM/CT backup​ `vzdump <vmid> --storage <storage_id> --compress zstd`
# Backup Modes
| **Mode** | **Description**                                                                                                                          |
| -------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| Stop     | - Fully powers off the workload<br>- Provides the most accurate backup, but implies downtime                                             |
| Snapshot | - Live backup option with no downtime<br>- Can be inconsistent<br>- It is NOT a snapshot but a backup                                    |
| Suspend  | - Middle ground between Stop and Snapshot Mode<br>- Mostly used for compatibility issues<br>- Has downtime because it suspends the VM/CT |
# Snapshots
- Gets a picture of the state of the VM/CT at a specific point in time
- Not meant to be used as backups
- Used for testing and development
# Proxmox Backup Server
- Fully-featured open source backup solution created for Proxmox VE
- Most advanced and reliable option to create backups
- Has its own GUI to manage the server
- Has Its own configuration for DNS, NTP, network interfaces and user management
- Can link several PBSs together for redundancy and reliability
- Can set up advanced control features, like traffic shaping and storage limits
- Needs another enterprise subscription
# Configuration Levels
- **Datacenter** - Applies to all the nodes that compose it
- **Node** - Only workloads in the node are backed up
- **Workload** - Most granular level; key for Fault Tolerance features
# Backup Jobs
- Can be set up as frequently as needed
- Needs to be aligned to a business continuity plan to be used efficiently
- Can include all VMs/CTs or a subset
- Must choose type of backup
# Backup Tools
**Pruning**
- Process of removing old backup snapshots according to predefined retention rules
- Helps manage storage by deleting unnecessary backups
- Pruning it typically configured at the storage or backup job level to automate cleanup
**Garbage Collection**
- Process of removing data chunks that are no longer referenced by any backups
- Frees up space by permanently deleting unneeded or orphaned data after pruning has removed old backups
- GC is run periodically to maintain storage efficiency