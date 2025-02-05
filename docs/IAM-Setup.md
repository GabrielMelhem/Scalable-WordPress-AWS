# Setting Up IAM for Scalable WordPress Resume on AWS

## 1. Set Up AWS Account 🛠️
Created an AWS Personal Free Tier account to implement a scalable WordPress online resume application.

## 2. Create IAM User for Administration 👤
- Created an IAM user  and assigned it to an Administrator group with the `AdministratorAccess` policy.
- Enabled **Billing Access** for the user. 💳
- Set up **AWS Budget Limits** to avoid exceeding the free tier. 💰

## 3. Creating IAM Groups for Role-Based Access 🧑‍💻
Created the following IAM groups with appropriate policies:
- **VPC-Admins**: Full access to manage VPC, subnets, and related resources (policies: `AmazonVPCFullAccess`, `AmazonEC2FullAccess`). 🌐
- **Storage-Admins**: Full access to manage S3 buckets, CloudFront, and other storage services (policies: `AmazonS3FullAccess`, `CloudFrontFullAccess`). 📦
- **Monitoring-Admins**: Full access to CloudWatch, CloudTrail, and other monitoring services (policies: `CloudWatchFullAccess`,`CloudWatchFullAccessV2`, `AWSCloudTrail_FullAccess`). 📊

## 4. Create IAM Users and Assign Them to Groups 🧑‍💻🔑
Created the following IAM users:
- `VPCAdminUser`: Assigned to the `VPC-Admins` group. 🖥️
- `StorageAdminUser`: Assigned to the `Storage-Admins` group. 📦
- `MonitoringAdminUser`: Assigned to the `Monitoring-Admins` group. 📊

## 5. Enabling Multi-Factor Authentication (MFA) for Extra Security 🔒
Enabled **MFA** (using virtual MFA apps like Google Authenticator) for all IAM users (`VPCAdminUser`, `StorageAdminUser`, `MonitoringAdminUser`). 🛡️

## 6. Testing Access ✅
- Tested login and permissions for each user to ensure proper access to resources based on group membership. ✅
- Verified MFA functionality for each user. 🔐
