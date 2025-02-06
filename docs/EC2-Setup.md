# Setting Up an EC2 Instance for WordPress Hosting 🚀

This guide outlines the steps to launch an EC2 instance for hosting your WordPress application. 🖥️

---

## Step 1: Choose an Amazon Machine Image (AMI) 🖼️
- Log in to the AWS Management Console as VPCAdminUser.
- Under Name and Tags, enter a name like WordPress WebServer
- Select **Amazon Linux 2 AMI (HVM), SSD Volume Type** (Free Tier eligible). ✔️

## Step 2: Choose an Instance Type ⚙️
- Choose **t2.micro** (Free Tier eligible). 🏷️

## Step 3: Create or Select Key Pair 🔑
- Choose **Create a new key pair** or use an existing one.
- Name it `your-key`.
- **Download the .pem file** and store it safely. 💾

## Step 4: Configure Instance Details ⚙️
- **VPC**: Select **WordPressVPC** (the VPC created earlier).
- **Subnet**: Choose **Public Subnet 1**.
- **Auto-assign Public IP**: **Enable**. 🌐

## Step 5: Configure Security Group 🔒
- Select **WordPress SG** (created during VPC setup).
- Ensure the following **Inbound Rules**:
  - **SSH (22)** → `Your IP only` 🔐
  - **HTTP (80)** → `0.0.0.0/0` 🌍
  - **HTTPS (443)** → `0.0.0.0/0` 🔒

## Step 6: Configure Storage 💾
- **Root volume**: 8GB (default, General Purpose SSD - gp2). 📦
- **Delete on Termination**: Enabled.
- No additional storage is needed for now. 🚫

## Step 7: Connect to the EC2 Instance 🔌
- Launch Instance
Once the instance is running, SSH into it:

```bash
chmod 400 your-key.pem
ssh -i your-key.pem ec2-user@your-public-ip
