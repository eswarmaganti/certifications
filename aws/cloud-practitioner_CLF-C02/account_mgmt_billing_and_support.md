# Account Management, Billing and Support


## AWS Organizations
- Global Service
- Allows to manage multiple AWS accounts
- The main account is the master account
- Cost Benefits
  - Consolidated Billing across all accounts - single payment method
  - Pricing benefits from aggregated usage (volume discount for EC2 and S3)
  - Pooling of Reserved EC2 instances for optimal savings
- API is available to automate AWS account creation
- Restrict account privileges using Service Control Policies (SCP)

### Multi Account Strategy
- Create accounts 
  - *per department*
  - *per cost center*
  - *per dev / test / prod*
  - *Based on regulatory restrictions (using SCP)* 
  - *for better resource isolation* 
  - *to have separate per-account service limits*
  - *isolated account for logins.*
- Multi Account Vs One Account with Multi VPC
- Use tagging standards for billing purposes
- Enable CloudTrail on all accounts, send logs to central S3 account
- Send CloudWatch Logs to central logging account.

### Service Control Policies
- Whitelist or blacklist IAM actions
- Applied at the OU or Account Level
- Does not apply to the Master Account
- SCP is applied to all the users and roles of the account, including Root
- The SCP does not affect service-linked roles
  - service-linked roles enable other AWS services to integrate with AWS organizations and can't be restricted by SCPs
- SCP must have an explicit allow (does not allow anything by default)
- Use cases
  - Restrict access to certain services (for example: can't use EMR)
  - Enforce PCI compliance by explicitly disabling services.

### AWS Organization - Consolidated Billing
- When enabled, provides you with
  - *Combined Usage*: combine the usage across all AWS accounts in the AWS Organization to share the volume pricing, Reserved Instances and Savings Plan discounts
  - *One Bill* - get one bill for all AWS Accounts in the AWS Organizations
- The management account can turn off Reserved Instances discount sharing for any account in the AWS Organization, including itself.
- The reserved instances can be shared between multiple account only in the reserved Availability Zone.

---

## AWS Control Tower
- Easy way to setup and govern a secure and compliant multi-account environment based on best practices
- benefits
  - Automate the setup of your environment in a few clicks
  - Automate ongoing policy management using guardrails
  - Detect policy violations and remediate them
  - Monitor complice through an interactive dashboard
- AWS Control Tower runs on top of AWS Organizations
  - It automatically sets up AWS Organizations to organize accounts and implement SCPs (Service Control Policies)

---

## AWS Resource Access Manager (AWS RAM)
- Share AWS Resources that you own with other AWS accounts
- Share with any account or within your organization
- Avoid resource duplication
- Supported resources include Aurora, VPC Subnets, Transit Gateway, Route53, EC2 Dedicated Hosts, License Manager Configurations

---
## AWS Service Catalog
- Users that are new to AWS have too many options, and may create stacks that are non compliant / in line with the rest of the organization
- Some users just want a quick self-service portal to launch a set of authorized products pre-defined by admins
- include: virtual machines, databases, storage options, etc..
- We can use AWS service catalog to define products which are CloudFormation Templates. A collection of products are called portfolio.
- Users can create resources easily with the products defined in service catalog

---

## Pricing Models in AWS
- AWS has 4 pricing models:
- *Pay as you go*: pay for what you have use, remain agile, responsive, meet scale demands
- *Save when you reserve*: minimum risks, predictably manage budgets, comply with long-terms requirements
  - Reservations are available for EC2 Reserved Instances, DynamoDB Reserved Capacity, ElastiCache Reserved Nodes, RDS Reserved Instance, RedShift Reserved Nodes
- *Pay less by using more*: volume-based discounts
- *Pay less as AWS grows*

### Compute Pricing - EC2
- Only charged for what you use
- Number of instances
- Instance configuration
  - Physical Capacity
  - Region
  - OS and Software
  - Instance Type
  - Instance Size
- ELB running time and amount of data processed
- Detailed monitoring (AWS Cloud watch metrics)
- *On-demand Instances*:
  - minimum of 60s
  - Pay per second (Linux/Windows) or per hour (other)
- *Reserved Instances*: 
  - Up to 75% discount compared to On-Demand on hourly rate
  - 1 or 3 years commitment
  - All upfront, partial upfront, no upfront
- *Spot Instances*:
  - Up to 990% discount compared to On-Demand on hourly rate
  - Bid for unused capacity
- *Dedicated Host&
  - on-Demand
  - Reservation for 1 year or 3 years commitment
- *Savings Plan* as an alternative to save on sustained usage

### Compute Pricing - Lambda & ECS
- *Lambda*:
  - Pay per call
  - Pay per duration
- *ECS*
  - EC2 Launch Type Model: No additional fees, you pay for AWS resources stored and created in your application
- *Fargate*:
  - Fargate Launch Type Model: Pay for vCPU and memory resources allocated to your applications in your containers.

### Storage Pricing - S3
- *Storage Class*: S3 standard, S3 Infrequent Access, S3 One-Zone IA, S3 Intelligent Tiering, S3 Glacier and S3 Glacier Deep Archive
- Number and size of objects: Price can be tiered (based on volume)
- Number and type of requests
- Data transfer OUT of the S3 region
- S3 Transfer Acceleration
- Lifecycle transitions
- Similar Service: *EFS* (pay per use, has infrequent access & lifecycle rules)

### Storage Pricing - EBS 
- Volume type (based on performance)
- Storage volume in GB per month provisioned
- IOPS:
  - General Purpose SSD: included
  - Provisioned IOPS SSD: Provisioned amount of IOPS
  - Magnetic: Number of requests
- Snapshots
  - Added data cost per GB per month
- Data Transfer:
  - Outbound data transfer are tiered for volume discounts
  - inbound is free

### Database Pricing - RDS
- Per hour billing
- Database characteristics
  - Engine
  - Size
  - Memory
- Purchase type:
  - On-demand
  - Reserved (1 or 3 years) with optional upfront
- Backup Storage: There is no additional charge for backup storage upt to 100% of your database storage for a region.
- Additional storage (per GB per month)
- Number of input and output requests per month
- Deployment type (storage and I/O are variable)
  - Single AZ
  - Multiple AZs
- Data transfer:
- Outbound data transfer are tiered for volume discounts
- Inbound is free

### Content Delivery - CloudFront
- Pricing is different across different geographic regions
- Aggregated for each edge location, then applied to your bill
- Data Transfer Out (volume discount)
- Number of HTTP/HTTPS requests

### Networking Costs in AWS per GB
- All the traffic in to your Region / AZ is free
- The communication between EC2 instance in same AZ is free using private IP
- The communication between EC2 instances in same region but different AvailabilityZones are free using private IPs but costs *$0.02* if public/elastic IPs
- The communications between EC2 instances in different regions will costs *$0.02* per GB

### Savings Plan
- Commit a certain $ amount per hour for 1 or 3 years
- Easiest way to setup long-term commitments on AWS
- *EC2 Savings Plan*:
  - Up to 72% discount compared to On-Demand
  - Commit to usage of individual families in a region (e.g. C4 or M5)
  - Regardless of AZ, size, OS or tenancy
  - All upfront, partial, no upfront
- *Compute Savings Plan*:
  - Up to 66% discount compared to On-demand
  - Regardless of Family, Region, size, Os, tenancy, compute options
  - Compute Options: EC2, Fargate, Lambda
- *Machine Learning Savings Plan*: Sage Maker
- Setup from AWS Cost Explorer console

---

## AWS Compute Optimizer
- Reduced costs and improve performance by recommending optimal AWS resources for your workloads
- Helps you chose optimal configurations and right-size your workloads (over/under provisioned)
- Uses Machine Learning to analyze your resources configurations and their utilization using CloudWatch Metrics
- Supported resources
  - EC2 instances
  - EC2 ASG
  - EBS Volumes
  - Lambda functions
- Lower your costs by up to 25%
- Recommendations can be exported to S3

---

## Billing and Costing Tools
- **Estimating Costs in the cloud*:
  - Pricing Calculator
- **Tracking costs in the cloud**
  - Billing Dashboard
  - Cost Allocation Tags
  - Cost and Usage Reports
  - Cost Explorer
- **Monitoring against costs plan**
  - Billing Alarms
  - Budgets

### AWS Pricing Calculator
- Estimate the cost for your solution architecture

### Cost Allocation Tags
- Use cost allocation tags to track your AWS costs on a detailed level
- AWS generated tags
  - Automatically applied to the resource you create
  - Starts with Prefix *aws*
- User-defined tags
  - Defined by the user
  - Starts with Prefix user

### Cost and Usage Reports
- Dive deeper into your AWS costs and usage
- The AWS cost & usage report contains the most comprehensive set of AWS cost and usage data available, including additional metadata about AWS services, pricing, and reservations
- The AWS Cost & Usage Report lists AWS usage for each service category used by an account and its IAM users in hourly or daily line items, as wll as any tags that you have activated for cost allocation purposes.
- Can be integrated with Athena, Redshift or QuickSight 

### Cost Explorer
- Visualize, understand, and manage your AWS costs and usage over time
- Create custom reports that analyze cost and usage data
- Analyze your data at a high level: total costs and usage across all accounts
- Or Monthly, hourly, resource level granularity
- Choose an optimal savings plan
- Forecast usage up to 12 months based on previous usage.


### Billing Alarms in CloudWatch
- Billing data metric is stored in Cloudwatch us-east-1
- Billing data are for overall worldwide AWS costs
- It's for actual cost, not for projected costs
- Intended as simple alarm (not powerful as AWS Budgets)

### AWS Budgets
- Create budget and send alarm when costs exceeds the budget
- 4 types of budgets:
  - *Usage*
  - *Cost*
  - *Reservation*
  - *Savings Plans*
- For Reserved Instances (RI)
  - Track utilization
  - Supports EC2, ElastiCache, RDS, Redshift
- Up to 5 SNS notification per budget
- Can filter by: Service, Linked Account, Tag, Purchase Option, Instance Type, Region, Availability Zone, API Operation, etc... 
- Same options as AWS Cost Explorer

### AWS Cost Anomaly Detection
- Continuously monitor your cost and usage using ML to detect unusual spends
- It learns your unique, historic spend patterns to detect one-time cost spike and/or continuous cost increases
- Monitor AWS services, member accounts, cost allocation tags or cost categories
- Sends you the anomaly detection report with root-cause analysis
- Get notified with individual alerts or daily/weekly summary (using SNS)

---

### AWS Trusted Advisor
- Service gives high level AWS account assessment
- Analyze your AWS accounts and provide recommendation on 6 categories
  - Cost optimization
  - Performance
  - Security
  - Fault Tolerance
  - Service Limits
  - Operational Excellence
- Business & Enterprise support plan
  - Full set of checks
  - Programmatic access using AWS support API
- Security check are enabled by default and is free using Trusted Advisor

### Support plans for AWS
- **Basic support**: *free*
  - *Customer service & communities* - 24*7 access to customer service, documentation, whitepapers, and support forums
  - *AWS Trusted Advisor* - Access to the 7 core Trusted Advisor checks and guidance to provision your resources following best practices to increase performance and improve security
  - *AWS Personal Health Dashboard* - A personalized view of the health of AWS services, and alerts when your resources are impacted.
- **Developer Support Plan**
  - All Basic support Plan +
  - Business hours email access to Cloud support associates
  - unlimited cases / unlimited contacts
  - Case severity/response times
    - General guidance < 24 business hours
    - System Impaired : < 12 business hours
- **Business Support Plan**
  - Intended to be used if you have production workloads
  - Trusted Advisor - Full set of checks + API access
  - 24*7 phone, email and chat access to Cloud Support Engineers
  - Unlimited cases / unlimited contacts
  - Access to Infrastructure Event Management for additional fee
  - Case Severity / response times:
    - General guidance < 24 business hours
    - System impaired: < 12 business hours
    - Production system impaired: < 4 hours
    - Production system down: < 1 hour
- **Enterprise On-Ramp Support Plan**
  - Intended to be used if you have production or business critical workloads
  - All of Business support plan +
  - Access to a pool of Technical Account Managers 
  - Concierge Support Team (for billing and account best practices)
  - Infrastructure Event Management, Well-Architected & Operations Reviews
  - Case severity / response times:
    - Production system impaired: < 4 hours
    - Production system down: < 1 hour
    - Business-critical system down: < 30 mins
- **Enterprise Support Plan**
  - Intended to be used if you have mission critical workloads
  - All of Business Support Plan +
  - Access to a designated Technical Account Manager
  - Concierge Support Team (for billing and account best practices)
  - Infrastructure Event Management, Well-Architected & Operations Reviews
  - Access to AWS Incident Detection and Response (for additional fee)
  - Case severity / response times
    - Production system impaired: < 4 hours
    - Production system down: < 1 hour
    - Business-critical system down: < 15 mins