# Design for data storage
To design Azure storage you must first determine what type of data you have.
- **Structured data** includes relational data and has a shared schema
- **Semi-structured** is less organized than structured data and isn't stored in a relational format
- **Unstructured data** is the least organized type of data
# Design for Azure storage accounts
## Determine the best storage account type

| **Account Type​**                      | **Supported services**​                         | **Usage**​                                                                                     |
| -------------------------------------- | ----------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| Standard general-purpose v2 (default)​ | Blobs / Data Lake, Queues, Tables, Azure Files​ | Recommended for most scenarios​                                                                |
| Premium block blobs​                   | Blob storage, Data Lake​                        | High transactions rates, single digit storage latency, or large numbers of small transactions​ |
| Premium file shares​                   | Azure Files​                                    | Enterprise or high-performance scale applications - supports both SMB and NFS file shares​     |
| Premium page blobs​                    | Page blobs only​                                | High performance and low latency storage scenarios​                                            |
# Considerations for storage accounts
- Location
- Replication
- Compliance
- Administrative overhead
- Cost
- Security - Data sensitivity
# Design for data redundancy
![[Pasted image 20260403125535.png]]
# Design for Azure blob storage
## Determine the storage tier
| Tier​             | Storage Duration​ | Usage cases​                                                                                      |
| ----------------- | ----------------- | ------------------------------------------------------------------------------------------------- |
| Premium​          | N/A​              | - High throughout and large numbers of I/O operations per second ​                                |
| Standard Hot​     | N/A​              | - Active and frequent use​<br>    <br>- Data staged for processing​                               |
| Standard Cool​    | > 30 days​        | - Short-term backup​<br>    <br>- Older media infrequently viewed​<br>    <br>- Large data sets ​ |
| Standard Cold​    | > 90 days​        |                                                                                                   |
| Standard Archive​ | > 180 days​       | - Long-term backup​<br>    <br>- Original (raw) data​<br>    <br>- Compliance or archival data​   |
## Consider immutable storage policies
**Determine regulatory compliance, secure document retention and legal hold policies**
- Apply immutable storage policies at the container level​
- Use time-based retention policies for business-critical data​
- Use legal-hold policies for sensitive information to ensure a tamper proof state​
- Policies apply to all objects within the container​
- Audit logs are available​
# Design for Azure files
![[Pasted image 20260403130613.png]]
# Design an Azure disk solution
![[Pasted image 20260403130743.png]]

| Disk type​      | Usage cases​                                                                                                       |
| --------------- | ------------------------------------------------------------------------------------------------------------------ |
| Ultra-disk SSD​ | IO-intensive workloads such as SAP HANA, top tier databases (SQL, Oracle), and other transaction-heavy workloads​  |
| Premium SSD v2​ | Production and performance-sensitive workloads that consistently require low latency and high IOPS and throughput​ |
| Premium SSD​    | Production and performance sensitive workloads​                                                                    |
| Standard SSD​   | Web servers, lightly used enterprise applications and dev/test​                                                    |
| Standard HDD​   | Backup, non-critical, infrequent access​                                                                           |
# Design for storage security
![[Pasted image 20260403131207.png]]
## Considerations for storage security
**Use a layered security model to secure and control access**
![[Pasted image 20260403131302.png]]
- Grant limited access to Azure Storage resources ​
- Enable firewall rules to limit access to access - IP addresses or subnets​
- Use private endpoints and private links for clients​
- Use virtual network service endpoints to provide direct connection​
- Use customer managed encryption keys​
