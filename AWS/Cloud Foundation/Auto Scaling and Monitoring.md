# Elastic Load Balancing
- Distributes incoming application/network traffic between targets in a single or multiple Availability Zone
- Scales your load balancer as traffic to your application changes over time
## Types of load balancers
![[Pasted image 20260415131058.png]]

## Elastic load balancing
![[Pasted image 20260415131212.png]]

**Use cases:**
- Highly available and fault-tolerant applications
- Containerized applications
- Elasticity and scalability
- VPC
- Hybrid environments
- Invoke Lambda functions over HTTP/s
## Load balancer monitoring
- **Amazon CloudWatch metrics** - Verify the system is performing as expected, alerts if metric goes outside range
- **Access logs** - Captures information about requests send to load balancer
- **AWS CloudTrail logs** - Capture information about API interactions
# CloudWatch
- Monitors resources + applications
- Collects and tracks standard/custom metrics
- Sends notifications to SNS
- Perform EC2 Auto Scaling or EC2 actions
- Define rules to match changes in AWS environment
## Alarms
- **Namespace** – A namespace contains the CloudWatch metric that you want, for example, AWS/EC2.
- **Metric** – A metric is the variable you want to measure, for example, CPU Utilization
- **Statistic** – A statistic can be an average, sum, minimum, maximum, sample count, a predefined percentile, or a custom percentile.
- **Period** – A period is the evaluation period for the alarm. When the alarm is evaluated, each period is aggregated into one data point.
- **Conditions** – When you specify the conditions for a static threshold, you specify whenever the metric is Greater, Greater or Equal, Lower or Equal, or Lower than the threshold value, and you also specify the threshold value.
- **Additional** configuration information – This includes the number of data points within the evaluation period that must be breached to trigger the alarm, and how CloudWatch should treat missing data when it evaluates the alarm.
- **Actions** – You can choose to send a notification to an Amazon SNS topic, or to perform an Amazon EC2 Auto Scaling action or Amazon EC2 action.
# EC2 Auto Scaling
- Auto Scaling group is a collection of EC2 instances that are treated as a logical grouping for the purpose of automatic scaling and management
- (Scale out = Launch instances, Scale in = terminate instances)
![[Pasted image 20260415132350.png]]
![[Pasted image 20260415132449.png]]
## Auto Scaling
- Monitors applications and adjust capacity to maintain steady performance at lowest possible cost