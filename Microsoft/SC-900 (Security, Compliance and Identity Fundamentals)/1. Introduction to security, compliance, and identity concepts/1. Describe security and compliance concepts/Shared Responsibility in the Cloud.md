|         | **Customer**                                              | **Azure**                                       |
| ------- | --------------------------------------------------------- | ----------------------------------------------- |
| On-Prem | Everything                                                |                                                 |
| IaaS    | OS, applications, network and data                        | Datacenter network and host machines            |
| SaaS    | Access management                                         | Application stack and underlying infrastructure |
| PaaS    | Application code, configuration, access controls and data | OS and runtime environment                      |
![[Pasted image 20260731142236.png]]
# Cloud Security Advantages
- Benefit from their security and monitoring
- Only have to focus on your responsibilities
- Provider handles patching and physical security
# AI Shared Responsibility Model
An AI-enabled application can be thought of in three layers:
- **AI platform**: The underlying infrastructure, AI model, and platform-level safety controls—including any built-in content filtering, safety systems, or access controls provided by the service.
- **AI application**: The application you build or deploy that connects to the AI platform, including how the app is configured, what data sources or connectors it uses, and what plugins it enables.
- **AI usage**: How people in your organization use the AI system—including the inputs they provide, the acceptable use policies you set, and the oversight you put in place.

![[Pasted image 20260731142441.png]]
## What the provider handles (AI)
- Securing the physical infrastructure and AI model hosting environment
- Providing platform-level safety controls
- Managing the underlying compute infrastructure
## What you handle (AI)
- Protecting your data
- Identity and access management
- Safe configuration
- Mitigating AI-specific risks
- User training and acceptable user policies
