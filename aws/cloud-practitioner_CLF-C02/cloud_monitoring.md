# CLoud Monitoring

## Cloud Watch
Amazon CloudWatch is a comprehensive monitoring and observability service for AWS resources and applications. It collects monitoring data in the form of logs, metrics and events, allowing users to visualize system health, set alarms, and automatically react to changes in performance. Key features include real-time monitoring of EC2, Lambda and custom application metrics

### Metrics
Metrics are fundamental concept in CloudWatch. A metric represents a time-ordered set of data points that are published to CloudWatch. Think of a metric as a variable to monitor, and the data points as representing the values og that variable over time.

For Example, the CPU usage of a particular EC2 instance is one metric provided by Amazon EC2. The data points themselves can come from any application or business activity from which you collect data.

- By Default, many AWS services provide metrics at no charge for resources such as EC2, RDS, EBS volumes etc,. You can also enable detailed monitoring for some resources, such as Amazon EC2 instances, or publish your own application metrics.
-  For custom metrics, you can add data points in any order and at any rate you choose. You can retrieve statistics about those data points as an ordered set of time-series data
- Metrics are uniquely defined by name, a namespace, and zero or more dimensions.  
- Each data point in a metric has a timestamp, and a unit if measure. You can retrieve statistics from cloudWatch for any metric.

## Alarms
- You can use an alarm to automatically initiate actions on your behalf. An alarm watches a single metric over a specified time period, and performs one or more specified actions, based on the value of metric relative to a threshold over time.
- The action is a notification sent to an Amazon SNS topic or an AutoScaling Policy. You can also add alarms to dashboards.
- Alarms invoke actions for sustained state changes only. CloudWatch alarms do not invoke actions simply because they are in particular state. The state must have changed and been maintained for a specified number of periods.
- When creating an alarm, select an alarm monitoring period that is greater than or equal to the metrics resolution. For example, basic monitoring for Amazon EC2 provides metrics for your instances every 5 minutes.

## CloudWatch Logs
- CloudWatch Logs can collect log from:
  - ElasticBeanstalk: collection of logs from application
  - ECS: collection from containers
  - AWS Lambda: collection from function logs
  - CloudTrail based on filter
  - CloudWatch log agent: on EC2 machines or on-premises servers
  - Route53: Log DNS queries
- Enable real-time monitoring of logs
- Adjustable CloudWatch Logs retention

### CloudWatch Logs for EC2
- By default, no logs from your EC2 instance will go to CloudWatch
- You need to run a CloudWatch agent on EC2 to push the log files you want
- Make sure IAM permissions are correct
- The CloudWatch log agent can be setup on-premises too.

## EventBridge (CloudWatch Events)
- Schedule: Cron jobs
- Event Pattern: Event rules to react to a service doing something
- Trigger Lambda function, send SQS/SNS messages...
- Default Event Bus inside AWS
- Partner Event Bus - from AWS partners like DataDog etc
- Custom Event Bus - custom events from applications
- Schema Registry: model event schema
- You can archive events sent to an event bus (indefinitely or set period)
- Ability to reply archived events


## AWS CloudTrail
- Provides governance, compliance and audit for your AWS account.
- CloudTrail is enabled by default
- Get an history of events / API calls made within your AWS account by
  - Console
  - SDK
  - CLI
  - AWS Services
- Can put logs from CloudTrail into CloudWatch Logs or S3
- A trail can be applied to all regions (default) or a single region
- If a resource id deleted in AWS, investigate AWS first
- CloudTrail retains management events in its "EventHistory" for 90 days by default.

---

## AWS X-Ray
- Debugging in Production, the good old way:
  - Test locally
  - Add log statements everywhere
  - Re-deploy in production
- Log formats differ across applications and log analysis is hard
- Debugging: one big monolith "easy", distributed services "hard"
- No common views of your entire architecture
- X-RAY helps with Visual Analysis of our Applications

### Advantages
- Troubleshooting performance (bottlenecks)
- Understand dependencies in a microservice architecture
- Pinpoint service issues
- Review request behavior
- Find errors and exceptions
- Are we meeting time SLA?
- Where I am throttled?
- Identify users that are impacted.

---

## Amazon CodeGuru
- An ML-powered service for automated code reviews and application performance recommendations
- Provides two functionalities
  - CodeGuru Reviewer: automated code reviews for static code analysis (development)
  - CodeGuru Profiler: visibility/recommendations about application performance during runtime (production)

---

## AWS Health Dashboard - Service History
- Shows all regions, all services health
- Shows historical information for each day
- Has an RSS feed you can subscribe to
- Previously called AWS service Health Dashboard

## AWS Health Dashboard - Your Account
- Aws Personal Health Dashboard (PHD)
- AWS account health dashboard provides alerts and recommendation guidance when AWS is experiencing events that may impact you
- The dashboard displays relevant and timely information to help you manage events in progress and provides proactive notification to help you plan for scheduled activities.
- Can aggregate the data for entire AWS Organizations