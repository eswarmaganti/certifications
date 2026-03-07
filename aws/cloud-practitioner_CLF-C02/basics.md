## What is cloud computing
- Cloud computing is the **on-demand** delivery of IT resources such as servers, storage, databases, and software 
- Through a cloud services platform with **pay-as-you-go** pricing
- You can provision exactly the right type and size of computing resources you need
- You can access as many resources as you need, almost instantly
- The cloud provider owns and maintains the network-connected hardware required for these application services, while you provision and use what you need via web interface.

## The Deployment Models of the Cloud
### Private Cloud
- Cloud Services used by a single organization, not exposed to the pubic
- Complete control
- Security for sensitive applications
- Meet specific business needs
- EX: rackspace

### Public Cloud
- Cloud resources owned and operated by a third-party cloud service provider delivered over the internet.
- Six Advantages of cloud computing
- EX: AWS, Azure, GCP

### Hybrid
- Keep some servers on premises and extend some capabilities to the Cloud

## Five Characteristics of Cloud Computing
- On-demand self service
  - Users can provision resources and use them without human interaction from the service provider
- Broad Network Access:
  - Resources available over the network, and can be accessed by diverse client platforms
- Multi-tenancy and resource pooling
  - Multiple customers can share the same infrastructure and applications with security and privacy
  - Multiple customers are services from the same physical resources
- Rapid elasticity and scalability
  - Automatically and quickly acquire and dispose resources when needed
  - Quickly and easily scale based on demand
- Measured Service
  - Usage is measured, users pay correctly for what they have used 

## Six Advantages of Cloud Computing
- Trade capital expense for operational expense
  - Pay on-demand: don't own infrastructure
  - Reduced Total Cost of ownership & Operational Expense
- Benefits from massive economies of scale
  - Prices are reduced as AWS is more efficient due to large scale
- Stop guessing capacity
  - scale based on actual measured usage
- Increased speed and agility
- Stop spending money running and maintaining DC's
- Go global in minutes: leverage the AWS global infrastructure

## Types of Cloud Computing
- IaaS
  - Provide building blocks for cloud IT
  - provides networking, computers, data storage space
  - Highest level of flexibility
  - Easy parallel with traditional on-premises IT
- PaaS
  - Removes the need for your organization to manage the underlying Infrastructure
  - Focus on the deployment and management of your applications
- SaaS
  - completed product is run and managed by the service provider


## Pricing of the Cloud
AWS has 3 pricing fundamentals, follows the pay-as-you-go pricing model
- Compute
  - pay for compute time
- Storage
  - Pay for data stored in the Cloud
- Data transfer OUT of the cloud
  - Data IN is free


## AWS Global infrastructure
- AWS Regions
- AWS Availability Zones
- AWS Data Centers
- AWS Edge Locations / POS

### AWS Regions
- AWS has Regions all around the world
- Names can be us-east-1, eu-west-3, ..
- A region is a cluster of data centers
- Most AWS services are region-scoped

### How to choose AWS Region
- *Compliance* with data governance and legal requirements: data never leaves a region without your explicit permission
- *Proximity*: to customers: reduced latency
- *Available Services* within a Region: new services and new features aren't available in every region.
- *Pricing*: pricing varies region to region and is transparent in the service pricing page.

### AWS Availability Zones
- Each region has many availability zones (usually 3, min is 3, max is 6). Example:
  - ap-southeast-2a
  - ap-southeast-2b
  - ap-southeast-2c
- Each AZ is one or more discrete data centers with redundant power, networking and connectivity
- They're separate from each other, so that they're isolated from disasters