# Major Elements of a SOC
![[Pasted image 20260801173132.png]]
## People
- Tier 1 Alert Analyst
- Tier 2 Incident Responder
- Tier 3 Threat Hunter
- SOC Manager
![[Pasted image 20260801173248.png]]
## Process
- Ticket system is frequently used to assign alerts to a queue for an analyst to investigate
- Since sometimes false alarms occur a Cybersecurity Analyst might be tasked with verifying alerts
- If the alert is a true positive then it can be forwarded to investigators or other security personnel
- If the ticket cannot be resolved the analyst will forward the ticket to a Tier 2 Incident Responder for deeper investigation and remediation
![[Pasted image 20260801173607.png]]
## Technologies
### SIEM
**Security Information and Event Management system**
Used to collect data, which is then filtered and classified to detect threats.

- Makes sense of all data gathered by firewalls, network appliances, IDS, etc
- Used for collecting and filtering data, detecting and classifying threats and analysing and investigating threats
- May also manage resources to implement preventive measures and address future threats

SOC technologies include one or more of the following:
- Event collection, correlation and analysis
- Security monitoring
- Security control
- Log management
- Vulnerability
- Vulnerability tracking
- Threat intelligence
![[Pasted image 20260801174135.png]]
### SOAR
**Security Orchestration, Automation and Response**
SOAR platforms aggregate, correlate and analyse alerts, as well as integrates threat intelligence and automating incident investigation and response workflows based on playbooks developed by the security team.

- SIEM and SOAR are often paired together as they have capabilities that complement each other.
![[Pasted image 20260801174358.png]]

SOAR security platforms:
- Gather alarm data from each component of the system
- Provide tools that enable cases to be researched, assessed and investigated
- Emphasize integration as a means of automating complex incident response workflows that enable more rapid response and adaptive defense strategies
- Include pre-defined playbooks that enable automatic response to specific threats. Playbooks can be initiated automatically based on predefined rules or may be triggered by security personnel
# SOC Metrics
- **Dwell Time** - Avg time before threat actors are detected in a network
- **Mean Time to Detect (MTTD)** - Avg time for SOC personnel to identify incident
- **Mean Time to Respond (MTTR)** - Avg time to stop and remediate incident
- **Mean Time to Contain (MTTC)** - Time to stop incident from causing more harm
- **Time to Control** - Time Required to stop spread of malware