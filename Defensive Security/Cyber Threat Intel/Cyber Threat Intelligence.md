Threat intelligence provides the context that helps an analyst decide which alerts represent danger.

CTI seeks to answer three essential questions:
1. Who or what is on the other end of this alert?
2. What was their behavior in the past
3. How does my org respond and what should I do about it right now?
# Raw Data -> Usable Intelligence
1. **Data** - An unprocessed observable
2. **Information** - Data plus factual annotation
3. **Intelligence** - Analyzed information that provides answers
# Lifecycle
1. Planning & Direction
2. Collection
3. Processing
4. Analysis
5. Dissemination
6. Feedback
![](CTI%20LifeCycle.canvas)
# Traffic Light Protocol (TLP)
|TLP label|Sharing boundary|Typical SOC L1 behaviour|
|---|---|---|
|**TLP: CLEAR**|No restriction|Post to the internal wiki or platform.|
|**TLP: GREEN**|Share with peer community but not publicly|Upload to MISP/Slack workspace restricted to partner SOCs.|
|**TLP: AMBER**|Organisation-wide, external sharing only with need-to-know clients|Keep within the company CTI platform; reference, do not copy, in tickets.|
|**TLP: RED**|Named recipients only|Store in an encrypted note; do not post to the ticketing system without clearance.|
