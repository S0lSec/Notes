# Design for Azure SQL databases
**SQL virtual machines**
Best for migrations and applications requiring OS-level access
**Managed instances**
Best for most life-and-shift migrations to the cloud
* Single instance
* Instance pool (Multiple instances)
**SQL Databases**
Best for modern cloud applications
* Single database
* Elastic pool
# Database Pricing models
**DTU**
* Simple
* preconfigured
**vCore**
* Flexible
* Control
* Transparent
* Independent scaling of compute, storage and I/O resources
**Serverless**
* Intermittent, unpredictable usage
* Automatically scales based on workload demand
# Azure SQL Database Service Tiers
## General Purpose/Standard tier
* Designed for common workload
* Budget oriented balanced compute and storage
* Uses nodes with spare capacity to spin up new SQL Server instances
* Uses LRS and RA-GRS
## Business Critical/Premium tier
* Designed for OLTP application
* High transaction rate and low I/O latency
* Offers the highest resilience to failures by using several isolated replicas
* Deploys an Always On availability group using multiple synchronously updated replicas
* Uses Local SSD storage and RA-GRS
## Hyperscale tier
* Designed for very large OLTP databases
* Able to autoscale storage and scale compute
* Captures instantaneous backups
* Restores in minutes
* Scale up or down in real time
# Design security for data
## Protect your database
**Network Security**
* VNet
* Firewall rules, NSG
* Private link
**Identify and access**
* Authentication options:
  * Entra ID
  * SQL Auth
  * Windows Auth
* Azure RBAC
* Roles and permissions
* Row level security
**Data protection**
* Encryption-in-use (Always encrypted)
* ^ -at-rest (TDE)
* ^ -in-flight (TLS)
* Customer-managed keys
* Dynamic data masking
**Security management**
* Advanced threat protection
* SQL audit
* Audit integration with log analytics and event hubs
* Vulnerability assessment
* Data discovery and classification
* Microsoft Defender for Cloud
## Authenticate to an Azure SQL database
SQL database supports two types of authentication:
* **SQL authentication:** Credentials are stored in the database
* **Microsoft Entra authentication:** Credentials are stored in Microsoft Entra ID
# Design for Azure SQL Edge
**Relational database engine for IoT and IoT Edge deployments
Containerized Linux app that runs on a process based on ARM64 or x64**
Use SQL Edge when you need to:​
* Capture continuous data streams in real time​
* Integrate the data in a comprehensive organizational data solution​
* Synchronization and connectivity to back-end systems​
* Overcome slow or intermittent broadband connections
# Design for Azure Cosmos DB
**Fully managed NoSQL database service for modern app development**
## When to use:
* Web and mobile applications that store and query user generated content like Tweets or blog posts​
* Retail and marketing industry that store catalog data and event sourcing in order proccing pipelines ​
* Gaming that requires single-millisecond latencies for reads and writes and can handle massive spikes in request rates​
* IoT use cases can load data into Azure Cosmos DB for adhoc querying. New data and changes to existing data can be read on change feed. Then all data or just changes to data in Azure Cosmos DB can be used as reference data as part of real-time analytics.​

