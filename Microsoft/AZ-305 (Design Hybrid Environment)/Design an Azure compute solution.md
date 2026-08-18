# Choose an Azure compute service
## Decision Flowchart
![[Pasted image 20260418131553.png]]
## Azure compute services
- **Azure Virtual Machines** - Its VMs...
- **Azure Batch** - Managed service to run large-scale parallel and high-performance computing applications
- **Azure App Service** - Host web apps, mobile app backends, RESTful APIs or automated business processes
- **Azure Functions** - Run code in the cloud without worrying about the infrastructure
- **Azure Logic Apps** - Cloud-based platform to create and run automated workflows (similar to capabilities in Azure Functions)
- **Azure Container Instances (ACI)** - Run containers similar to docker
- **Azure Container Apps (ACA)** - Run containerized applications on a fully managed serverless without managing Kubernetes infrastructure
## Things to consider
- Architecture and infrastructure reqeuirements
- Support for new workload scenarios
- Required hosting options, including platform, infrastructure and functions
- Support for migrations
## Workloads and Architecture
When planning for new instances of Azure services and new workloads consider:
- **Control** - Determine if you require full control over software and applications
- **Workloads** - Consider the workloads you need to support
- **Architecture** - What architecture best supports your infrastructure
## Migrations
Consider migration capabilities
- **Cloud optimized** - Migrate to the cloud and refactor applications to access cloud-native features
- **Lift and shift** - Consider compute services that don't require application redesigns or code changed
- **Containerized** - Does your compute service need to support containerized applications or commercial of the shelf apps
## Hosting
![[Pasted image 20260418132744.png]]
# Design for Azure Virtual Machines solutions
Two main scenarios where Virtual Machines can be an ideal compute solutions:
 - Building new workloads
 - Migrating data by using the lift and shift pattern
 ![[Pasted image 20260418133111.png]]
## Considerations
- Network
- VMs name and location
- Size
- Pricing models and Azure Storage options
- OS
# Design for Azure Batch solutions
- Is similar to VMs and can be used to build new workloads and migrate data
- Works sell with applications that run independently (parallel workloads)
- Effective for applications that need to communicate with each other
- Enables large-scale parallel and high-performance computing batch jobs
![[Pasted image 20260418133445.png]]
## Considerations
- **Pools** - Don't create a new pool for each jobs
- **Nodes** - Individual nodes aren't guaranteed to always be available
- **Jobs** - Uniquely name your jobs so you can accurately monitor and log the activity
# Design for Azure App Service solutions
- All your apps share common benefits
- PaaS environment
- Supports development in multiple languages and frameworks
- Offers built-in load balancing and traffic management at global scale with high availability
- Provides built-in authentication and authorization capabilities
![[Pasted image 20260418134034.png]]
## Continuous deployment
- App Service enables continuous deployment
- Whenever possible use deployment slots for new production build
![[Pasted image 20260418134325.png]]
## Considerations
- Web Apps
- API apps
- WebJobs
- Continuous deployment
- Authentication and Authorization
- Multiple plans to reduce costs
# Design for Azure Container Instance solutions
![[Pasted image 20260418134555.png]]
## Container groups
- A container group is a collection of containers that get scheduled on the same host machine. The containers in a group share a lifecycle, resources, local network and storage volumes
- Useful for when you want to divide a single functional task into several container images
## Considerations
- Use a private registry
- Ensure image integrity throughout the lifecycle
- Monitor container resource activity
# Design for Azure Kubernetes Service solutions
- Platform for automating deployment, scaling and the management of containerized workloads
- Includes the following features:
	- Automated updates
	- Self-healing
	- Easy scaling
![[Pasted image 20260419221738.png]]
**Pricing Tiers**
- Free
- Standard
- Premium
## Considerations
|Feature|Consideration|Solution|
|---|---|---|
|**Identity and security management**|_Do you already use existing Azure resources and make use of Microsoft Entra ID?_|You can configure an Azure Kubernetes Service cluster to integrate with Microsoft Entra ID and reuse existing identities and group membership.|
|**Integrated logging and monitoring**|_Are you using Azure Monitor?_|Azure Monitor provides performance visibility of the cluster.|
|**Automatic cluster node and pod scaling**|_Do you need to scale up or down a large containerization environment?_|AKS supports two auto cluster scaling options. The _horizontal pod autoscaler_ watches the resource demand of pods and increases pods to meet demand. The _cluster autoscaler_ component watches for pods that can't be scheduled because of node constraints. It automatically scales cluster nodes to deploy scheduled pods.|
|**Cluster node upgrades**|_Do you want to reduce the number of cluster management tasks?_|AKS manages Kubernetes software upgrades and the process of cordoning off nodes and draining them.|
|**Storage volume support**|_Does your application require persisted storage?_|AKS supports both static and dynamic storage volumes. Pods can attach and reattach to these storage volumes as they're created or rescheduled on different nodes.|
|**Virtual network support**|_Do you need pod-to-pod network communication or access to on-premises networks from your AKS cluster?_|An AKS cluster can be deployed into an existing virtual network with ease.|
|**Application routing and ingress**|_Do you need to make your deployed applications publicly available?_|AKS supports application routing through the application routing add-on. AKS is transitioning to the Kubernetes Gateway API as the long-term standard for ingress.|
|**Docker image support**|_Do you already use Docker images for your containers?_|By default, AKS supports the Docker file image format.|
|**Private container registry**|_Do you need a private container registry?_|AKS integrates with Azure Container Registry (ACR). You aren't limited to ACR though, you can use other container repositories, public, or private.|
# Design for Azure Functions solutions
![[Pasted image 20260419222112.png]]- Serverless application platform
- Used when you want to run a small piece of code in the cloud
- Only charged for resources you use
- Lets you handle specific definable actions triggered by an event
![[Pasted image 20260419222229.png]]
## Considerations
- Long running functions
- Durable functions
- Performance and scaling
- Defensive functions
- Not sharing storage accounts
# Design for Azure Logic Apps solutions
![[Pasted image 20260419222356.png]]
- Serverless compute solution for creating and running automated workflows
- Schedule and send email notifications using Microsoft 365 when a specific event happens
## Logic Apps vs Functions
![[Pasted image 20260419222509.png]]

| Compare          | Azure Functions                                                                                                                                                          | Azure Logic Apps                                                                                                                                                                                                                                                                                                                                                      |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Development**  | Code-first                                                                                                                                                               | Design-first                                                                                                                                                                                                                                                                                                                                                          |
| **Method**       | Write code and use the durable functions extension                                                                                                                       | Create orchestrations with a GUI or by editing configuration files                                                                                                                                                                                                                                                                                                    |
| **Connectivity** | - [Large selection of built-in binding types](https://learn.microsoft.com/en-us/azure/azure-functions/functions-triggers-bindings)  <br>- Write code for custom bindings | - [Large collection of connectors](https://learn.microsoft.com/en-us/azure/connectors/apis-list)  <br>- [Enterprise Integration Pack for B2B scenarios](https://learn.microsoft.com/en-us/azure/logic-apps/logic-apps-enterprise-integration-overview)  <br>- [Build custom connectors](https://learn.microsoft.com/en-us/azure/logic-apps/custom-connector-overview) |
| **Monitoring**   | Azure Application Insights                                                                                                                                               | Azure portal, Azure Monitor Logs (Log Analytics)                                                                                                                                                                                                                                                                                                                      |
## Considerations
- Integration
- Performance
- Conditional expressions
- Connectors
- Mixing compute solutions
- Other options
- Logic Apps hosting models
![[Pasted image 20260419222637.png]]