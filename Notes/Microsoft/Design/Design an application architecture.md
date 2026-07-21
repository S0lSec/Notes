# Describe message and event scenarios
- First decision in design is to plan how the application components communicate
- Most application components communicate by sending messages or events
## Messages
- Contains raw data produced by one component and consumed by another component
- Contains the data itself
- In a message communication, the sending component expects the destination to process the data in a certain way. The integrity of the overall system might depend on both the sender and receiver doing a specific job.
## Events
- Lighter weight than messages
- Often used for broadcast communication
- An event-driven architecture consists of event producers that generate a stream of events, event consumers that listen for these events and event channels that transfer events from producers to consumers
![[Pasted image 20260420082008.png]]
**Characteristics**
- Lightweight notification that indicates something occurred
- Can be sent to multiple or no receivers
- An event publisher has no expectations about actions by a receiving component
- An event is a discrete unit that's unrelated to other events, but an event might be part of a related and ordered series
## Considerations when choosing
- Consider using both
- Consider sender expectations
- Consider guaranteed communication
- Consider ephemeral communication
# Design a messaging solution
Azure offers two message-based solutions:
- Azure Queue Storage
- Azure Service Bus
## Azure Queue Storage
- Uses Azure Storage to store large numbers of messages
- Queues can contain millions of messages
- The number and size of queues is limited only by the capacity of the Azure storage account
- Messages in Queue Storage can be securely accessed from anywhere by using a simple REST-based interface
## Azure Service Bus
- Used to decouple applications and services from each other
- Supports message queues and publish-subscribe topics
- Lets you load-balance work across competing works
- Can be used to safely route and transfer data and control across service application boundaries
- Help coordinate transactional work that requires a high degree of reliability
### Message Queues
- A broker system built on top of a dedicated messaging infrastructure
- Intended for enterprise applications
![[Pasted image 20260420082932.png]]
## Considerations when choosing messaging services
| Messaging solution                                    | Example scenarios                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| ----------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Azure Queue Storage**                               | _You want a simple queue to organize messages_.  <br>  <br>_You need an audit trail of all messages that pass through the queue_.  <br>  <br>_The queue storage exceeds 80 GB_.  <br>  <br>_You'd like to track progress for processing a message inside of the queue_.                                                                                                                                                                                                                                                                             |
| **Azure Service Bus**  <br>_message queues_           | _You require an at-most-once delivery guarantee_.  <br>  <br>_You require at-least-once message processing (PeekLock receive mode)_.  <br>  <br>_You require at-most-once message processing (ReceiveAndDelete receive mode)_.  <br>  <br>_You want to group messages into transactions_.  <br>  <br>_You want to receive messages without polling the queue_.  <br>  <br>_You need to handle messages larger than 64 KB_.  <br>  <br>_The queue storage doesn't exceed 80 GB_.  <br>  <br>_You'd like to publish and consume batches of messages_. |
| **Azure Service Bus**  <br>_publish-subscribe topics_ | _You need multiple receivers to handle each message_.  <br>  <br>_You expect multiple destinations for a single message but need queue-like behavior_.                                                                                                                                                                                                                                                                                                                                                                                              |
# Design an Azure Event Hubs message solution
- Fully managed, big data streaming platform and event ingestion service
- Supports real time data ingestion and micro services batching on the same stream
- Can send and receive events in many different languages
- Events received by Event Hubs are added to the end of its data stream
- Holds each message in its cache and allows it to be read
- Messages remain for other consumers
## Considerations
- Common implementations
- Language and framework integration
- Pricing tier and throughput units
- Pull model benefits
- Message failures
- Data stream access
# Design an event-driven solution
- Enables you to connect to the core application without needing to modify the existing code
- When an event occurs you can respond with specific code
- Aggregates all your events and provides routing from any source to any destination
- Distributes events from sources (like Blob storage accounts)
- Events are distributed to handlers like Azure functions and webhooks
## How it works
![[Pasted image 20260421124738.png]]
1. An event source such as Azure Blob Storage tags events with one or more topics, and sends events to Azure Event Grid.
2.  An event handler such as Azure Functions subscribes to topics they're interested in.
3. Event Grid examines topic tags to decide which events to send to which handlers.
4.  Event Grid forwards relevant events to subscribers.
5. Event Grid reacts when an event happens. However, the actual object that was changed (text file, video, audio, and so on) isn't part of the event data. Instead, Event Grid passes a URL or identifier to reference the changed object.
## Considerations
- Consider using multiple services to fulfill your design requirements
- Consider distinct roles for services
- Consider push vs pull delivery
- Consider linking services
![[Pasted image 20260421124953.png]]

|Azure service|Purpose|Message or Event|Usage scenario|
|---|---|---|---|
|**Azure Event Grid**|Reactive programming|Event distribution (discrete)|_React to status changes_|
|**Azure Event Hubs**|Big data pipeline|Event streaming (series)|_Conduct telemetry and distributed data streaming_|
|**Azure Service Bus**|High-value enterprise messaging|Message|_Fulfill order processing and financial transactions_|

# Design a caching solution
- Temporarily copies frequently accessed data to  fast storage located close to the application
- Can improve response times for client applications by serving data more quickly
- Caching is most effective when a client instance repeatedly reads the same data
## Azure Managed Redis
- Usable by any application within or outside Azure
- Helps improve performance in apps that interface with many database solutions
![[Pasted image 20260421215002.png]]
### Considerations
| Pattern                      | Scenario                                                                                                                                                                                                                                                                                     | Solution                                                                                                                                                                                                                                                                                                                                                                                        |
| ---------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Data cache**               | _Databases are often too large to load directly into a cache_.                                                                                                                                                                                                                               | It's common to use the _cache-aside_ pattern to only load data into the cache as needed. When the system makes changes to the data, the system can also update the cache, which is then distributed to other clients. Additionally, the system can set an expiration on data, or use an eviction policy to trigger data updates into the cache.                                                 |
| **Content cache**            | _Many web pages are generated from templates that use static content such as headers, footers, banners. These static items shouldn't change often_.                                                                                                                                          | Using an in-memory cache provides quick access to static content compared to back-end datastores. This pattern reduces processing time and server load and allows web servers to be more responsive. A content cache can allow you to reduce the number of servers needed to handle loads. Azure Managed Redis provides the _Redis Output Cache Provider_ to support this pattern with ASP.NET. |
| **Session store**            | _A session store is commonly used with shopping carts and other user history data that a web application might associate with user cookies. Storing too much in a cookie can have a negative effect on performance as the cookie size grows and is passed and validated with every request_. | A typical solution uses the cookie as a key to query the data in a database. It's faster to use an in-memory cache like Azure Managed Redis to associate information with a user than interacting with a full relational database.                                                                                                                                                              |
| **Job and message queuing**  | _Some application operations take significant time to complete, which might prevent other unrelated jobs or messages from starting_.                                                                                                                                                         | Applications often add tasks to a queue when the operations associated with the request take time to execute. Longer running operations are queued to be processed in sequence, often by another server. This method of deferring work is called _task queuing_. Azure Managed Redis provides a distributed queue to enable this pattern in your application.                                   |
| **Distributed transactions** | _Applications sometimes require a series of commands against a back-end datastore to execute as a single atomic operation. All commands must succeed, or all commands must be rolled back to the initial state_.                                                                             | Azure Managed Redis supports executing a batch of commands as a single transaction.                                                                                                                                                                                                                                                                                                             |

# Design API integration
- Lets you public, secure, maintain and analyze all your APIs
![[Pasted image 20260421215134.png]]
## Considerations
- Consider number of APIs
- Consider rate of API changes
- Consider API administration load
- Consider standardizing disparate APIs
- Consider service tier selection:
	- Class tiers
	- V2 tiers
	- Consumption tiers
	- Premium v2
- Consider centralized API management
- Consider enhanced API security
# Design an automated app deployment solution
## Azure Resource Manager templates
- Files that define the infrastructure and configuration for your deployment
- Describe each resource in deployment
## Azure Bicep templates
- Bicep ARM template language used to deploy Azure resources
## Azure Automation
- Supports consistent management across your Azure and non-Azure environments
- Gives complete control in 3 services areas:
	- process automation
	- configuration management
	- update management

|Service|Description|
|---|---|
|**Process automation**|Process automation enables you to automate frequent, time-consuming, and error-prone cloud management tasks. This service helps you focus on work that adds business value. By reducing errors and boosting efficiency, it also helps to lower your operational costs. The service allows you to author runbooks graphically in PowerShell or by using Python.|
|**Configuration management**|Configuration management enables access to two features, Change Tracking and Inventory and Azure Automation State Configuration. Azure Automation State Configuration is retiring September 30, 2027 (portal links removed March 31, 2025). **Azure Machine Configuration** (via Azure Policy) is the replacement for new implementations. The service supports change tracking across services, daemons, software, registry, and files in your environment using Azure Monitoring Agent (not Log Analytics). The change tracking helps you diagnose unwanted changes and raise alerts.|
|**Update management**|Update management is now handled by the separate **Azure Update Manager** service (retired from Azure Automation August 31, 2024). Azure Update Manager provides scheduled deployments, maintenance windows, and patch orchestration for Windows and Linux across hybrid environments.|

# Design an app configuration management solution
Configuration management is a modern software-development practice that decouples configuration from code deployment and enables quick changes to feature availability on demand.
## Azure App Configuration
- Provides a service to centrally manage application settings and feature flags
- Fully managed service
- Flexible key representations and mappings
- Has configuration snapshots
### Development Environment
An Azure App Configuration development environment consists of Visual Studio, Visual Studio Code, and the Azure CLI. These components are linked to Microsoft Entra ID, App Configuration, and Azure Key Vault.
![[Pasted image 20260421220024.png]]
### Production
An Azure App Configuration production environment consists of Azure and Microsoft Entra managed identities for Azure resources with related Azure services. These components are linked to Microsoft Entra ID, App Configuration, and Key Vault.
![[Pasted image 20260421220049.png]]