# S.M.A.R.T Reporting
(Self-Monitoring, Analysis, and Reporting Technology)
Used to gather the health and performance of your physical disks.

Datacenter > server > Disks
# Interface Metrics
To get an overview of the overall health of the Proxmox VE cluster
Datacenter > summary

To track local resource utilization
Datacenter > server > summary
# Common Notification Events
| Event                          | Type              | Severity  | Metadata fields (in addition to type)       |
| ------------------------------ | ----------------- | --------- | ------------------------------------------- |
| System updates available       | `package-updates` | `info`    | `hostname`                                  |
| Cluster node fenced            | `fencing`         | `error`   | `hostname`                                  |
| Storage replication job failed | `replication`     | `error`   | `hostname`, `job-id`                        |
| Backup succeeded               | `vzdump`          | `info`    | `hostname`, `job-id` (only for backup jobs) |
| Backup failed                  | `vzdump`          | `error`   | `hostname`, `job-id` (only for backup jobs) |
| Mail for root                  | `system-mail`     | `unknown` | `hostname`                                  |
# Monitor Feature
Monitor gives the user low level access the VM/CT/node

| **Command**        | **Description**                                          |
| ------------------ | -------------------------------------------------------- |
| `stop`             | Pauses the VM/CT, keeping it in the state it was stop at |
| `cont`             | Restart KVM emulator (continues)                         |
| `system_powerdown` | Forces a shutdown via KVM module                         |
| `sendkey`          | Sends key into VM/CT (`sendkey ctrl-alt-f6`)             |
| `screendump`       | Captures screenw                                         |
