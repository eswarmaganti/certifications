
## VPC Endpoint
A VPC Endpoint enables private connectivity between an AWS VPC and supported AWS Services or VPC endpoint services without using an Internet Gateway, NAT Gateway or VPN connection.

Traffic stays entirely within the AWS network, significantly improving security and reducing latency. There are two main types: *Interface Endpoints (powered by PrivateLink)* and *Gateway Endpoint(for S3/DynamoDB)*

### Key Details about VPC Endpoints:
- **Types**:
  - *Interface Endpoint (AWS PrivateLink)*: An Elastic Network Interface (ENI) with a private IP address from your subnet, acting as a target for traffic to supported services like Lambda, Kinesis, or EC2 API.
  - *Gateway Endpoints*: A gateway targeted in your route table for traffic destined for S3 or DynamoDB.
- **Security**: Endpoint policies can be attached to control access, specifying with principals and actions are allowed.
- **Cost**: Gateway endpoints are free; interface endpoints incus hourly and data processing changes.
- **Configuration**: Requires configuring security groups for interface endpoints to allow traffic.