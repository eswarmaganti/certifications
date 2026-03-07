# Identity and Access Management

## IAM: Users & Groups
- IAM = Identity and Access Management, Global Service
- Root account created by default, shouldn't be used or shared
- Users are people within your organization, and can be grouped
- Groups only contain users, not other groups
- Users don't have to belong to a group, and user can belong to multiple groups.

## IAM: Policies
- Users or Groups can be assigned JSON documents called Policies
- These policies define the permissions of the users
- in AWS you apply the least privilege principle: don't give more permissions than a user needs
- Example:
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "s3Full",
      "Effect": "Allow",
      "Action": "s3:*"
      "Resource": "*",
    },
    {
      "Sid":"ec2ReadOnly",
      "Effect": "Allow",
      "Resource": "*",
      "Action": "ec2:Describe*"
    }
  ]
}

```

## IAM: Password Policy
- Strong Passwords = higher security for your account
- IN AWS, you can setup a password policy:
  - set a min character types
    - including uppercase letters
    - lowercase letters
    - numbers
    - non-alphanumeric characters
  - Allow all IAM users to change their own password
  - Require users to change their password after some time
  - Prevent password re-use.

## IAM: Multi Factor Authentication
- Users have access to your account and can possibly change configurations or delete resources in your AWS account
- You want to protect your Root Accounts and IAM users
- MFA = password you know + security device you own

## How can users access AWS?
- To access AWS, you have three options:
  - AWS Management Console (protected by password + MFA)
  - AWS Command Line Interface (CLI): protected by access keys
  - AWS Software Developer Kit (SDK) - for code: protected by access keys
- Access keys are generated through AWS Console
- Users manage their own access keys
- Access keys are secret, just like a password, Don't share them
- Access Key ID ~= username
- Secret Access Key ~= password


## IAM Roles for AWS Services
- Some AWS services will need to perform actions on your behalf
- To do so, we will assign permissions to AWS services with IAM Roles
- Common roles
  - EC2 Instance Roles
  - Lambda Function Roles
  - Roles for CLoudFormation

## IAM Security Tools
- IAM Credentials Report (account-level)
  - a report that lists all your account's users and the status of their various credentials
- IAM Access Advisor (user-level)
  - Access advisor shows the service permissions granted to a user when those services were last accessed
  - You can use this information to revise your policies

## IAM Shared Responsibility Model

- AWS:
  - Infrastructure (Global network security)
  - Configuration and Vulnerability analysis
  - Compliance validation
- Admin:
  - Users, Groups, Roles, Policies management and monitoring
  - Enable MFA on all accounts
  - Rotate all your keys often
  - Use IAM tools to apply appropriate permissions
  - Analyze access patterns & review permissions
