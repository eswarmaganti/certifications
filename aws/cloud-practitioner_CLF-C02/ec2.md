# Elastic Compute Cloud (EC2)

## EC2 sizing & configuration options
- Operating System (OS): Linux, Windows, MacOS
- How much compute power & cores (CPU)
- How much RAM
- How much storage space
  - Network-attached (EBS & EFS)
  - hardware (EC2 instance store)
- Network card: speed of the card, Public IP address
- Firewall rules: security group
- Bootstrap script (configure at first launch): EC2 user data

## EC2 Instance Types
- You can use different types of EC2 instances that are optimized for different use cases
  - General Purpose
  - Compute Optimized
  - Memory Optimized
  - Accelerated Computing
  - Storage Optimized
  - HPC Optimized
  - Instance Features
  - Measuring Instance Performance
- AWS has the following naming convention
  - `m5.2xlarge`
    - **m**: instance class
    - **5**: Generation
    - **2xlarge**: size within the instance class


### General Purpose
- Great for a diversity of workload such as web servers or code repositories
- Balance between:
  - Compute
  - Storage
  - Networking

### Compute Optimized
- Great for compute-internsive tasks that require high performance
- Use Cases:
  - Batch processing workloads
  - Media transcoding
  - High performance web servers
  - High performance computing (HPC)
  - Scientific modelling & machine learning
  - Dedicated gaming servers

### Memory Optimized
- Fast performance for workloads that process large data sets in memory 
- Use Cases:
  - High performance, relational/non-relational databases
  - Distributed web scale cache stores
  - In-memory databases optimized for BI
  - Applications performing real-time processing of big unstructured data

### Storage optimized
- Great for storage-intensive tasks that require high, sequential read and write access to large data sets on local storage
- Use cases:
  - High frequency online transaction processing systems
  - Relational & NoSQL databases
  - Cache for in-memory databases (Redis)
  - Data warehousing applications
  - Distributed file systems


## Security Groups
- Security Groups are the fundamental of network security in AWS
- They control how traffic is allowed into or out of our EC2 server
- Security groups only contain allow rules.
- Security group rules can reference by IP or by security group
- They regulate
  - Access to Ports
  - Authorized IP ranges - IPv4 and IPv6
  - Control of inbound network
  - Control of outbound network
- By default all inbound traffic is blocked and all outbound traffic is authorized.

## EC2 Instances purchasing options
- On-Demand Instances - short workload, predictable pricing, pay by second
- Reserved (1 & 3 Years)
  - Reserved Instances - long workloads
  - Convertible Reserved Instances - long workloads with flexible instances
- Savings Plan (1 & 3 years) - commitment to an amount of usage, long workload
- Spot Instances - short workloads can lose instances (less reliable)
- Dedicated Hosts - Book an entire physical server, control instance placement
- Dedicated Instances - no other customers will share your hardware
- Capacity Reservations - reserved capacity in a specific AZ for any duration.

### Reserved Instances
- You reserve a specific instance attributes (Instance Type, Region, Tenancy, OS)
- Reservation Period 1 Year or 3 years
- Payment Options - No Upfront, Partial Upfront, All Upfront
- Reserved Instance scope - Regional or Zonal
- Recommended for study-state usage applications 
- You can buy and sell in the Reserved Instance Marketplace
- Convertible Reserved Instances
  - Can change the EC2 instance type, instance family, OS, scope and tenancy

### EC2 Savings Plans
- Get a discount based on long-term usage
- Commit to a certain type of usage ($10/hour for 1 or 3 years)
- Usage beyond EC2 plans is billed at the on-demand price
- Locked to specific instance family & region
- Flexible across
  - Instance size
  - OS
  - Tenancy

### Stop Instances
- Can get a discount of up to 90% compared to On-demand
- Instances that you can "lose" at any point of time if your max price is less than the current spot price
- The Most cost-effective instances in AWS
- Useful for workloads that are resilient to failure
  - Batch Jobs
  - Data Analysis
  - Image processing
  - Any distributed workloads
  - Workloads with a flexible start and end time
- Not suitable for critical jobs or databases

### Dedicated Hosts
- A physical server with EC2 instance capacity fully dedicated to your use.
- Allows you address *compliance requirements* and *use your existing server-bound software licenses* (per-socket, per-core, pe-VM software licenses)
- Purchasing Options:
  - on-demand: pay per second for active Dedicated Host
  - Reserved - 1 or 3 years
- The most expensive option
- Useful for software that have complicated licensing model or companies that have strong regulatory or compliance needs

### Dedicated Instances
- Instances tun on hardware that's dedicated to you
- May share hardware with other instances in same account
- NO control over instance placement (can move hardware after stop/start)

### Capacity Reservations
- Reserved on-demand instances capacity in a specific AZ for any duration
- You always have access to EC2 capacity when you need it.
- No time commitment (create/cancel anytime), no billing discounts
- Combine with Regional Reserved Instances and Savings Plans to benefit from billing discounts
- You're changed at on-demand rate whether you run instances or not
- Suitable for short-term, uninterrupted workloads that needs to be in a specific AZ.


## Shared Responsibility Model for EC2
- AWS
  - Infrastructure (global network security)
  - Isolation on physical hosts
  - replace faulty hardware
  - compliance validation
- User
  - Security Groups rules
  - OS patches and updates
  - Software and utilities installed on the EC2 instance
  - IAM Role assigned to EC2 & IAM user access management
  - Data security on your instance.

---

## AWS Instance Storage

### EBS Volume
- An EBS Volume is a network drive you can attach yo your instances while they run
- It allows your instances to persist data, even after their termination
- They can only be mounted to one instance at a time
- They are bound to specific availability zone
- It's a network drive ( not a physical)
  - It used the network to communicate the instance, which means there might be bit og latency
  - It can be detached from an EC2 instance and attached to another one quickly
- It;s locked to an AZ
  - An EBS volume in us-east-1a cannot be attached to us-east-1b
  - To move a volume across, you first need to snapshot it
- Have a provisioned capacity
  - You get billed for all the provisioned capacity
  - You can increase the capacity of the drive over time 

### EBS snapshots
- Make a backup (snapshot) of your EBS valume at a point in time
- Not necessary to detach volume to do snapshot, but recommended
- Copy snapshots across regions or AZ

- Features
  - EBS snapshot Archive
    - Move a snapshot to an "archive tier" that is 75% cheaper
    - Takes within 24 to 72 hours for restoring
  - Recycle Bin for EBS snapshots
    - Setup rules to retain deleted snapshots so you can recover them after an accidental deletion
    - Specify retention (from 1 day to 1 year)

### AMI (Amazon Machine Image)
- AMI are a customization of an EC2 instance
  - You add your own software, configuration, operating system. monitoring..
  - Faster boot/configuration time because all your software is pre-packages
- AMI are built for a specific region (and can be copied across regions)
- You can launch EC2 instances from:
  - A Public AMI: AWS Provided
  - Your own AMI: you make and maintain them yourself
  - An AWS Marketplace AMI: an AMI someone else made (and potentially sells)

- **AMI Process**
  - Start an EC2 instance and customize it
  - Stop the instance (for data integrity)
  - Build an AMI - this will also create EBS snapshot
  - Launch instance from other AMIs

### EC2 Image Builder
- Used to automate the creation of Virtual Machines or container images
- Automate the creation, maintain, validate and test EC2 AMIs
- Can be run on a schedule (weekly, whenever packages are updated, etc)
- Free Service (Only pay for underlying resources)


### EC2 Instance Store
- EBS volumes are network drives with good but "limited" performance
- If you need a high-performance hardware disk, use EC2 Instance Store
  - Better I/O performance
  - EC2 Instance store lose their storage if they're stopped (ephemeral)
  - Good for buffer / cache / Scratch data / temporary content
  - Risk of data loss if hardware fails
  - Backups and Replication are your responsibility

### EFS - Elastic File System
- Managed NFS (network file system) that can be mounted on 100s of EC2
- EFS works with Linux EC2 instances in multi-AZ
- Highly available, scalable, expensive (3 * gp2), pay per use, no capacity planning

### Shared Responsibility Model for EC2 Storage
- AWS:
  - Infrastructure
  - Replication of dta for EBS volumes & EFS drives
  - Replacing faulty hardware
  - Ensuring their employees cannot access your data
- Customer:
  - Setting up backup / snapshot procedure
  - Setting up data encryption
  - Responsibility of any data on the drives
  - Understanding the risk of using EC2 instance store.

---

## Elastic Load Balancing & Auto Scaling Groups

### High Availability & Scalability for EC2
- Vertical Scaling Increase instance size (= scale up / down)
  - From t2.nano - o.5G of RAM, 1 vCPU
  - To: 1-12tbl.metal - 12.3 TB of RAM, 448 vCPUs
- Horizontal Scaling: Increasing number of instances (= scale in / out)
  - Auto Scaling Group
  - Load Balancer
- High Availability: Run instances for the same application across multip AZ
  - ASG with multi AZ
  - Load Balancer multi AZ

### Scalability vs Elasticity (vs Agility)
- *Scalability*: Ability to accommodate a larger load by making the hardware stronger (scale up), or by adding nodes (scale down)
- *Elasticity*: Once a system is scalable, elasticity means that there will be some "auto-scaling" so that the system can scale based on the load. This is cloud-friendly: pay-per-use, match demand, optimize costs
- *Agility*: New IT resources are only a click away, which means that you reduce the time to make those resources available to your developers from weeks to just minutes.

### Elastic Load Balancing

- *What is load balancing?*
  - Load balancers are servers that forward internet traffic to multiple servers downstream
- *Why use a load balancer?*
  - Spread load across multiple downstream instances
  - Expose a single point of access (DNS) to your application
  - Seamlessly handle failures of downstream instances
  - Do regular health checks to your instances
  - Provide SSL termination (HTTPS) for your websites
  - High availability across zones
- *Why use an Elastic Load Balancer?*:
  - An ELB is a managed load balancer
    - AWS guarantees that it will be working
    - AWS take care of upgrades, maintenance, High Availability
    - AWS provides only a few configuration knobs
  - It costs less to setup your own load balancer but it will be a lot more efforts on your end (maintenance & integrations)
  - 4 kinds of LB's are offered by AWS
    - *Application Load Balancer (HTTP/HTTPS)* - Layer 7
    - *Network Load Balancer (TCP)* - Layer 4
    - *Gateway Load Balancer * - Layer 3
    - *Classic Load Balancer* - Retired

### What is an Auto Scaling Group?
- In real-life, the load on your websites and application can change
- In the cloud, you can create and get rid of servers very quickly
- The goal of an Auto Scaling Group is to
  - Scale Out to match an increased load
  - Scale in to match a decreased load
  - Ensure we have a minimum and maximum number of machines running
  - Automatically register new instances to a load balancer
  - Replace unhealthy instances

### Auto Scaling Groups - Scaling Strategies
- **Manual Scaling**: Update the size of an ASG manually
- **Dynamic Scaling**: Respond to changing demand
  - *Simple / Step Scaling*
    - When a CloudWatch alarm is triggered (example CPU > 70%), then add 2 units
    - When a CloudWatch alarm is triggered (example CPU < 30%), then remove 1 unit
  - *Target Tracking Scaling*:
    - I want the average ASG CPU to stay at around 40%
  - *Scheduled Scaling*
    - Anticipate a scaling based on known usage patterns
    - Example: Increase the min capacity to 10 at 5pm on Fridays
  - *Predictive Scaling*:
    - Uses Machine Learning to predict future traffic ahead of time.
    - Automatically provisions the right number of EC2 instances in advance.
