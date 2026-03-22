# AWS Global Infrastructure
AWS Global Infrastructure is the foundational, high secure, and expansive physical backbone of Amazon Web Services, comprising worldwide data centers, networking and software systems.
It enables users to run application with low latency and high availability across Regions, Availability Zones and Edge Locations, forming the largest, most reliable cloud ecosystem.

## AWS Global Applications
AWS global application services enable deploying, accelerating and managing applications across the world with low latency and high availability.
### Key Global application services
- **Amazon CloudFront (CDN)**: Delivers data, videos, and APIs to users globally with low latency using a network of edge locations
- **AWS Global Accelerator**: Improves availability and performance by routing traffic over the AWS private network to the nearest healthy application endpoint
- **Amazon Route 53**: A highly available DNS web service that routes user requests to global infrastructure
- **AWS IAM**: Provides secure, centralized management of user access to AWS resources globally.
- **AWS SHield & WAF**: Protects web applications from DDoS attacks and common web exploits at the edge.

---

## AWS Route 53
Amazon Route 53 is a highly available and scalable cloud domain name system (DNS) web service that translates user-friendly domain names into numeric IP addresses. If effectively connects user requests to infrastructure running in AWS or in-premise, while offering domain registration, health-checking and flexible routing policies.

### Key Concepts
- **Domain Registration**: Purchase and manage domain names directly through AWS
- **Hosted Zones**: A container for record that defines how to route traffic for a domain, similar to traditional DNS zone file
- **Records**: These define how traffic is routed, mapping names to IP addresses (A/AAAA), other domains (CNAME) or AWS resources (Alias)
- **Alias Records**: Specifically for AWS resources (CloudFront, ELB) these act as "smart" records that can map the root domain and update automatically if the resource IP changes.
- **Health Checks**: Monitors the health of your applications. ROute 53 can detect unhealthy endpoints and automatically reroute traffic to healthy resources.
- **Routing Policies**:
  - *Simple*: Basic mapping for single resource
  - *Weighted*: Splits traffic based on assigned percentages
  - *Latency-Based**: Directs users to the regions with the lowest latency.
  - *Failover*: Used for active-passive setups to redirect traffic if the main site fails.
  - *Geo-location/Geo-proximity**: Route traffic based on the user's location.
- **Route 53 Resolver**: Handles the recursive DNS queries for VPCs and allows connecting DNS queries between your virtual network and on-premise network.

---

## AWS CloudFront
Amazon CloudFront is a fast, secure and programmable COntent Delivery Network (CDN) service provided by AWS that accelerates the delivery of static and dynamic web content (like images, videos, APIs) to users globally. By caching content at edge locations - over 216 points of presence - it reduces latency and improves performance.

### Key Features & Benefits
- **Global Performance**: Delivers content from the closest edge location, reducing latency for end-users
- **Security**: Integrated with AWS Shield & AWS for DDoS protection, offering SSL/TLS support and field-level encryption.
- **AWS Integration**: Works seamlessly with Amazon S3, ELastic Load Balancing, ROute 53 and Lambda@Edge
- **Cost-Effective**: Pay-as-you-go pricing with no mandatory upfront contacts, plus 1TB of free data transfer per month
- **Support for Dynamic Content**: Speeds up dynamic content by using optimized network paths to the origin.

### How it works
- Users request content
- CloudFront delivers it from the nearest edge location
  - If not cached, it fetches the content from the "origin", (ex: S3 bucket or HTTP server) and caches it for future requests

### CloudFront Origins
- *S3 bucket*
  - For distributed files and caching them at the edge
  - For uploading files to S3 through CloudFront
  - Secured using Origin Access Control
- *VPC Origin*
  - For applications hosted in VPC private subnets
  - Private application Load Balancer / network Load Balancer / EC2 instance
- *Custom Origin (HTTP)*
  - S3 website
  - Any public HTTP backend you want

---

## AWS Global Accelerator
AWS Global accelerator is a networking service that improves internet users performance for applications by up to 60% using AWSs global network infrastructure. It provides static Anycast IP addresses that route traffic to the nearest healthy endpoints -- such as ALB, NLB or EC2 instances -- across regions.

### Key Benefits
- **Improved Performance**: Uses AWS edge locations to route user traffic onto the private AWS network instantly, reducing internet latency and jitter.
- **Static IP addresses**: Provides two static IP addresses that act as a fixed entry point, eliminating the need to update client applications when backend endpoints change.
- **High Availability**: Continuously monitors endpoint health and reroutes traffic to healthy endpoints within 30 seconds if a failure occurs
- **Global Traffic Management**: Allows traffic failing to manage traffic percentages across Regions for blue.green testing or traffic shifting.
- **Security**: Protects applications by hiding backend endpoints behind the static Anycast IPs, offering built-in AWS Shield protection.

### AWS Global Accelerator VS CloudFront
- They both use the AWS global network and its edge locations around the world
- Both services integrate with AWS Shield for DDoS protection
- CloudFront - Content Delivery Network
  - Improves performance for your cacheable content (such as images and videos)
  - Content is server at the edge
- Global Accelerator:
  - No caching, proxying packets at the edge to applications running in one or more AWS Regions
  - Improves performance for a wide range of applications over TCP or UDP
  - Good for HTTP use cases that require static IP addresses
  - Good for HTTP use cases that required deterministic, fast regional failover.

---

## AWS Outposts
- Hybrid Cloud: businesses that keep an on-premises infrastructure alongside a cloud infrastructure
- Therefore, two ways of dealing with IT systems:
  - One for the AWS Cloud (using AWS console, CLI and APIs)
  - One for their on-premises infrastructure
- *AWS Outposts are "server racks"* that offers the same AWS infrastructure, services, APIs & tools to build your own application on-premises just as in the cloud.
- *AWS will setup and manage "Outposts Racks" within your on-premises infrastructure* and you can start leveraging AWS services on-premises.
- You are responsible for the Outposts Rack physical security.

---

## AWS Wavelength
- Wavelength Zones are infrastructure deployments embedded within the telecommunication providers datacenters at the edge of the 5G networks
- Brings AWS services to the edge of the 5G networks 
- Example: EC2, EBS, VPC,...
- Ultra-low latency application through 5G networks
- Traffic doesn't leave the Communication service provider's network
- High-bandwidth and secure connection to the parent AWS Region
- No additional charges or service agreements
- Use cases: Smart Cities, ML-assisted diagnostics, Connected Vehicles, Interactive Live Video Streams, AR/VR

---

## AWS Local Zones
- Places AWS compute, storage, database, and other selected AWS services closer to end users to run latency-sensitive applications
- Extend your VPC to more locations -- "Extension of an AWS Region"
- Compatible with EC2, RDS, ECS, EBS, ElastiCache, DirectConnect ...
- Example
  - AWS Region: N.Virginia (us-east-1)
  - AWS Local Zones: Boston, Chicago, Dallas ...

