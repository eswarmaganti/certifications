## What is CloudFormation
- CloudFormation is a declarative way of outlining your AWS Infrastructure, for any resources
- For example, with a CloudFormation template, you say:
  - I want a security group
  - I want two EC2 instances using this security group
  - I want an S3 bucket
- Then CloudFormation creates those for you, in the right order with the exact configuration that you specify

### Benefits
- Infrastructure as Code
  - No resources are manually created, which is excellent for control
  - Changes to the infrastructure are reviewed through code
- Cost
  - Each resource within the stack is tagged with an identifier so you can easily see how much a stack costs you
  - You can estimate the costs of your resources using the CloudFormation template
  - Saving strategy: In Dev, you could automate deletion of templates at 5PM and recreate at 8AM, safely
- Productivity
  - Ability to destroy and re-create an infrastructure on the cloud on the fly
  - Automated generation of Diagram for your templates
  - Declarative programming
- Don't re-invent the wheel
  - Leverage existing templates on the web
  - Leverage the documentation
- Supports all AWS resources
  - You can use "custom resources" for resources that are not supported

---

## AWS CDK (Cloud Development Kit)
- Define your cloud infrastructure using a familiar language
  - JS/Python/Java and .NET
  - The code is "compiled" into a CloudFormation template (JSON/YAML)
  - You can therefore deploy infrastructure and applications runtime code together
    - Great for Lambda functions
    - Great for Docker containers in ECS/EKS

---

## AWS Elastic Beanstalk
- Elastic Beanstalk is a developer centric view of deploying an application on AWS
- It used all the components like: EC2, ASG, ELB, RDS ...
- But it's all in one view that's easy to make sense of
- We still have full control over the configuration
- Beanstalk = Platform as a Service
- Beanstalk is free but you pay for the underlying instances
- Managed Service
  - Instance configuration / OS is handled by Beanstalk
  - Deployment strategy is configurable but performed by Elastic Beanstalk
  - Capacity provisioning
  - Load Balancing & Auto-Scaling
  - Application health-monitoring & responsiveness
- Just the application code is the responsibility of the developer
- Three architecture models:
  - single instance deployment: good for dev
  - LB + ASG: great for production or pre-prod web applications
  - ASG only: great for non-web apps in production

---

## AWS CodeDeploy
- We want to deploy our application automatically
- Works with EC2 instances
- Works with on-premises servers
- Hybrid service
- Server/Instances must be provisioned and configured ahead of time with the CodeDeploy Agent

## AWS CodeCommit
- a fully managed source control service that hosts secure, scalable git-based repositories, allowing teams to collaborate on code without managing their own infrastructure.
- It integrates with AWS services like IAM, CloudTrain and CodeBuild and supports standard Git Commands, pull requests and encryption at rest.
- Note that as of late 2024, AWS is not accepting new customers for this service

## AWS CodeBuild
- Code building service in the cloud
- Compiles source code, run tests and produce packages that are ready to be deployed
- Benefits
  - Fully Managed, serverless
  - Continuously scalable & highly available
  - Secure
  - Pay-as-you-go pricing - only pay for build time

## AWS CodePipeline
- Orchestrate the different steps to have the code automatically pushed to production
  - Code -> Build -> Test -> Provision -> Deploy
- Benefits
  - Fully managed, compatible with CodeCommit, CodeBuild, CodeDeploy, ElasticBeanstalk, CloudFormation, Github, 3rd party services
  - fast delivery & rapid updates

## AWS CodeArtifact
- Software packages depend on each other to be build and new one are created.
- Storing and retrieving these dependencies is called artifact management
- Traditionally you need to setup your own artifact managemnt system
- CodeArtifact is a secure, scalable, and cost-effective artifact management for software development
- Works with common dependency management tools such as Maven, Gradle, npm, yarn, pip ...
- Developers and CodeBuild can then retrieve dependencies straight from CodeArtifact

---

## AWS Systems Manager (SSM)
- Helps you manage your EC2 and On-Premises systems at scale
- Another Hybrid AWS service
- Get operational insignts aboiut the state of your infrastructure
- Suite of 10+ products
- Most important features are:
  - Patching automation for enhanced compliance.
  - Run commands across an entire fleet of servers
  - Store parameter configuration with SSM parameter store
- Works for Linux, Windows, MacOS and RaspberryPi OS

### How SSM works
- We need to install the SSM agent onto the systems we control
- Installed by default on Amazon Linux AMI & some Ubuntu AMI
- If an instance can't be controlled with SSM, it's probably an issue with the SSM agent
- Thanks to the SSM agent, we can run commands, patch & configure our server's

### SSM Session Manager
- Allows you to start a secure shell on your EC2 and on-premises servers
- No SSH access, bastion hosts or SSH keys needed
- No port 22 needed
- Supports Linux, MacOs and windows
- Send session log data to S3 or CloudWatch Logs

### SSM Parameter Store
- Secure store for configuration and secrets
- API Keys, passwords, configurations...
- Serverless, scalable, durable, easy SDK
- Control access permission using IAM
- version tracking & encryption

