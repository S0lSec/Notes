# Evaluate Migration with the Cloud Adoption Framework
![[Pasted image 20260423121311.png]]
## Considerations
| Effort    | Description                                                                                                                                                                                                                                                                                                                                              |
| --------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| _Assess_  | Assess your workloads to determine costs, modernization, and required deployment tools.                                                                                                                                                                                                                                                                  |
| _Deploy_  | After you assess your workloads, the existing workload functionality is replicated (or improved) in the cloud.                                                                                                                                                                                                                                           |
| _Release_ | After your workloads are deployed (replicated) to the cloud, you can test, optimize, and document your migrated workloads. When you're ready, you can release the workloads to your users. During the _Release_ effort, be sure to hand off the workloads to governance, operations management, and security teams for ongoing support of the workloads. |
![[Pasted image 20260423121409.png]]
# Describe the Azure migration framework
Before migrating a migration plan should be made. This plan should identify workloads to migrate, and the appropriate service or tools to use.
## Stage 1: Assess your-on-premises environment
- Identify your apps, and their related servers, services, and data, that's within scope for migration.
- Start to involve stakeholders, such as the IT department and relevant business groups.
- Create a full inventory and dependency map of your servers, services, and apps that you're planning to migrate.
- Estimate your cost savings by using the Azure Total Cost of Ownership Calculator (TCO).
- Identify appropriate tools and services you can use to perform the four stages.
### Migration strategy patterns
| **Rehost**                                                                                                                                                                                                                                                                                              | **Refactor**                                                                                                                                                                                                        | **Rearchitect**                                                                                                                                                                                                                                                                                                                                | **Rebuild**                                                                                                                                                                                                                                                                                                                            |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| _Move workloads quickly to the cloud_  <br>  <br>_Move a workload without modifying it_  <br>  <br>_For apps designed to take advantage of Azure IaaS scalability after migration_  <br>  <br>_When workloads are important to your business, but you don't need immediate changes to app capabilities_ | _Apply innovative DevOps practices provided by Azure_  <br>  <br>_Implement a DevOps container strategy for workloads_  <br>  <br>_Support portability of your existing code base and available development skills_ | _Your apps need major revisions to incorporate new capabilities_  <br>  <br>_Your apps need major revisions to work effectively on a cloud platform_  <br>  <br>_Use existing application investments_  <br>  <br>_Meet scalability requirements_  <br>  <br>_Apply innovative DevOps practices_  <br>  <br>_Minimize use of virtual machines_ | _Rapid development_  <br>  <br>_Support existing apps with limited functionality and lifespan_  <br>  <br>_Expedite business innovation by using DevOps practices_  <br>  <br>_Rebuild with new cloud-native technologies like Azure Blockchain_  <br>  <br>_Rebuild legacy applications as "no code apps" or "low apps" in the cloud_ |
## Stage 2: Migrate your workloads
- Deploy cloud infrastructure targets
- Migrate workloads
- Decommission on-premises infrastructure
## Stage 3: Optimize your migrated workloads
- Analyze migration costs for your workloads
- Review recommendations for reducing your costs
- Identify options for improving your workload performance
(You can use Microsoft Cost Management to analyze your workload costs.)
## Stage 4: Monitor your workloads
- Can use Azure Monitor to capture health and performance information from your Azure virtual machines.
- Set up alerts based on data sources, such as:
	- Specific metric values like CPU usage
	- Specific text in log files
	- Health metrics
	- Autoscale metrics
# Assess your on-premises workload
## Migration tools and services
| Service or tool                | Stage                | Description                                                                                                                                                                                                               |
| ------------------------------ | -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Azure Migrate**              | _Assess_ & _Migrate_ | Azure Migrate performs assessment and migration to Azure of virtual machines (Hyper-V and VMware), cloud-based virtual machines, physical servers, databases, data, virtual desktop infrastructure, and web applications. |
| **Database Migration Service** | _Assess_ & _Migrate_ | The Azure Database Migration Service performs assessment and migration for several different databases, not just Azure SQL Database.                                                                                      |
| **Data Migration tool**        | _Migrate_            | The Azure Cosmos DB Data Migration tool migrates your existing databases to Azure Cosmos DB.                                                                                                                              |
| **Microsoft Cost Management**  | _Optimize_           | Microsoft Cost Management helps you monitor, optimize, and control your ongoing Azure costs.                                                                                                                              |
| **Advisor**                    | _Monitor_            | Azure Advisor helps optimize your Azure resources for reliability, performance, cost, security, and operational excellence.                                                                                               |
| **Monitor**                    | _Monitor_            | Azure Monitor collects monitoring data from both on-premises and Azure resources that help you analyze data, set up alerts, and identify problems.                                                                        |
| **Microsoft Sentinel**         | _Monitor_            | Microsoft Sentinel provides intelligent security analytics for your applications that enable you to collect, detect, investigate, and respond to incidents.                                                               |
## Things to know about Discovery and Assessment
- Azure has many assessment tools
- To perform an agentless discovery use Azure Migrate Discovery and assessment tools
**The full process for assessing a server can be visualized as follows:**
![[Pasted image 20260423154147.png]]
# Select a migration tool
## Azure Migrate
- **Unified migration platform**: Azure Migrate provides a single portal where you can perform migration to Azure and track the migration status.
- **Assessment and migration tools**: Azure Migrate supplies several assessment and migration tools, including Server Assessment, Server Migration, and other independent software vendor (ISV) tools.
- **Assessment and migration features for different workloads**: Azure Migrate hub supports several different workloads for migration:
    - Servers: On-premises servers are assessed and migrated to Azure virtual machines. Migration is available for both Linux and Windows servers.
    - Databases: On-premises databases are assessed and migrated to Azure SQL Database or to an Azure SQL Managed Instance.
    - Web applications: On-premises web applications are assessed and migrated by using Azure App Service Migration Assistant.
    - Virtual desktops: On-premises virtual desktop infrastructure (VDI) is assessed and migrated to Azure Virtual Desktop.
    - Data: Large volumes of data are migrated to Azure by using Azure Data Box products.
- **Azure Migrate hub tools**: The Azure Migrate hub provides access to many migration tools.
## Azure Resource Mover
- A single location for moving resources.
- Simplicity and speed in moving resources.
- A consistent interface and procedure for moving different types of Azure resources.
- A way to identify dependencies across resources that you want to move.
- Automatic clean-up of resources in the source region.
- The ability to test a move operation before you commit it.
# Migrate your structured data in databases
## Azure Database Migration Service
- Apart of Azure Migrate
- Can migrate databases offline or online
	- **Offline migration**: An offline migration requires shutting down the server at the start of the migration. Use online migration if you can't afford application downtime.
	- **Online migration**: An online migration uses a continuous synchronization of live data, which allows a cut over to the Azure replica database at any time. Online migration minimizes downtime.
## Considerations 
- Do you need an assessment to identify compatibility issues?
- Do you need a SKU recommendation?
- Do you need to migrate database logins and schemas?
- Do you need to automate the process?
- Do you have a specific product scenario?
- Do you need to integrate with other migration tools?
# Select an online storage migration tool for unstructured data
## Azure Storage Mover
- Migrate files and folders to Azure Storage
- Azure Storage Mover works on both NFS shares and SMB shares.
- Can be used for different scenarios such as lift-and-shift
![[Pasted image 20260423160344.png]]
### Considerations
- A single storage mover resource can manage migrations for your source shares
- The storage mover resource itself doesnt process your files/folders
- Storage Mover is hybrid cloud service
## Azure File Sync
- Provides the functionality of an on-premises file share with the benefits of a PaaS cloud service
- Can be used to centralize file shares management
- Can be used to cache Azure file shares on Windows Server computers
### Considerations
| Scenario                                         | Description                                                                                                                                                                                                                                                                                                                                                                                                                |
| ------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| _Replace or supplement on-premises file servers_ | Virtually all companies use file servers. Azure Files can completely replace or supplement traditional on-premises file servers or Network Attached Storage (NAS) devices. With Azure file shares and Microsoft Entra Domain Services authentication, you can migrate data to Azure Files and utilize high availability and scalability while minimizing client changes.                                                   |
| _Lift and shift (rehome)_                        | Azure Files makes it easy to lift-and-shift applications that expect a file share to store application or user data to the cloud.                                                                                                                                                                                                                                                                                          |
| _Backup and disaster recovery_                   | You can use Azure file shares as storage for backups, or for disaster recovery to improve business continuity. You can use Azure file shares to back up your data from existing file servers while preserving configured Windows discretionary access control lists (ACLs). Data stored on Azure file shares is protected from disasters that might affect on-premises locations.                                          |
| _Azure File Sync_                                | With Azure File Sync, Azure file shares can replicate to Windows Server, either on-premises or in the cloud, for performance and distributed caching of data where it's being used. Consider using Azure File Sync when you want to migrate shared folder content to Azure. This method is especially useful as a means for replacing the Distributed File System on your Windows Servers in your on-premises datacenters. |
# Migrate offline data
## Azure Import/Export Service
- You can use the Azure Import/Export service to export data from Azure Blob Storage only.
- You can't export data stored in Azure Files.
- To use the Import/Export service, BitLocker must be enabled on the Windows system.
- You need an active shipping carrier account like FedEx or DHL for shipping drives to an Azure datacenter.
- For exporting, you need a set of disks you can send to an Azure datacenter. The datacenter uses these disks to copy the data from Azure Storage.
### Considerations
- Ideal for large handling amounts of data when the network backbone doesn't have sufficient capacity or reliability to support large-scale transfers
- The import/export service can be helpful in other scenarios including:

|Scenario|Description|
|---|---|
|_Migration_|Use the Import/Export service to migrate large amounts of data from on-premises to Azure, as a one-time task.|
|_Backup_|You can back up your data on-premises in Azure Storage with the Import/Export service.|
|_Recovery_|With the Import/Export service, you can recover large amounts of data you previously stored in Azure Storage.|
|_Distribution_|The Import/Export service helps you distribute data from Azure Storage to customer sites.|
## Azure Data Box
- Provides a quick, reliable and inexpensive method for moving large volumes of data to Azure
- Includes the following components:
	- Data box device
	- Data box service
	- Data box local web-based used interface
### Considerations
- Ideal for transfering 40TB or more
**Situaitons**:

| Scenario                | Description                                                                                                                                                                                                                                                                                                                            |
| ----------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| _One time migration_    | Use Azure Data Box to migrate a large amount of on-premises data to Azure. Move a media library from offline tapes into Azure to create an online media library. Migrate your virtual machine farm, SQL server, and applications to Azure. Move historical data to Azure for in-depth analysis and reporting by using Azure HDInsight. |
| _Initial bulk transfer_ | You can perform an initial bulk transfer with Azure Data Box and follow it with incremental transfers over the network. Move large volumes of historical backup to Azure. After this data is added, you can continue to maintain the archive with incremental data transfers by network to Azure Storage.                              |
| _Periodic uploads_      | Use Azure Data Box to move large volumes of data generated periodically to Azure. Move data generated by sensors from customer connected IoT devices.                                                                                                                                                                                  |
## Compare Azure Import/Export and Azure Data Box
| Compare                                  | Azure Import/Export        | Azure Data Box                                  |
| ---------------------------------------- | -------------------------- | ----------------------------------------------- |
| **Form factor**                          | Internal SATA HDDs or SDDs | Secure, tamper-proof, single hardware appliance |
| **Microsoft manages shipping logistics** | No                         | Yes                                             |
| **Integrates with partner products**     | No                         | Yes                                             |
| **Custom appliance**                     | No                         | Yes                                             |