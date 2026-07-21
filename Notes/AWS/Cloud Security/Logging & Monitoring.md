# Importance of logging and monitoring
- Logging provides a record of events
- Logging required for demonstrating compliance with regulations
- Monitoring continuously verifies the security and performance of your resources, applications and data
# Capture and Collect
**CloudTail**
- Assists with compliance
- Records actions taken
- Can view events
- Can be used to view, search, download, archive, analyze and respond to account activity
![[Pasted image 20260520083441.png]]
# AWS Services with built-in logs
- S3
- VPC
- ELB
# Monitor and Report
**CloudWatch**
- Provides view of operational health
- Collects metrics in Cloud and on remises
- Can be used for monitoring and troubleshooting
# CloudTrail vs CloudWatch
| **CloudTrail**                                                                  | **CloudWatch**                                                                           |
| ------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| Continuously monitors and logs user activities                                  | Continuously monitors resources and application performance                              |
| Useful for compliance auditing, security. analysis and troubleshooting          | Useful for detecting anomalous service behavior, setting alarms and discovering insights |
| Helps you determine WHO performed WHAT unauthorized action and WHEN they did it | Alerts you that an issue has occurred due to an unauthorized action                      |
# Best Practices
- Define your organizational requirements
- Configure service and application logging throughout your workload
- Analyze your logs centrally
# Services for logging and monitoring
- AWS Trusted Advisor - Provides recommendations
- Amazon EventBridge - Connect your application with data from other sources
- AWS Security Hub - For security and alerts
- AWS Config - For resources