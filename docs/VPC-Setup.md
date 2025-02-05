# Setting Up VPC for Scalable WordPress Resume on AWS 🌐

## Step 1: Create the VPC 🏗️
- **Name tag:** `WordPressVPC`
- **IPv4 CIDR block:** `10.0.0.0/16`
- **IPv6 CIDR block:** No IPv6 CIDR block ❌
- **Tenancy:** Default 🏠
- **Number of Availability Zones (AZs):** 2 🌍🌍

---

## Step 2: Create Subnets 🛠️  
### Open the Subnets Page 📋  
- Create subnets for each **Availability Zone (AZ)**  
- **Two subnets** in each Availability Zone:  
  - **Public Subnet** 🌍: For resources like Load Balancers & Web Servers with public internet access.  
  - **Private Subnet** 🔒: For databases that should not have direct internet access.  

### Configure Subnet Settings ⚙️  
#### For Availability Zone 1 (`us-west-2a`):
- **Public Subnet 1:** `10.0.1.0/24`
- **Private Subnet 1:** `10.0.2.0/24`

#### For Availability Zone 2 (`us-west-2b`):
- **Public Subnet 2:** `10.0.3.0/24`
- **Private Subnet 2:** `10.0.4.0/24`

---

## Step 3: Create an Internet Gateway (IGW) 🌉
- **Name tag:** `WordPressIGW`
- **VPC:** Attach to `WordPressVPC`  

---

## Step 4: Update Route Tables 🚦  
### Public Route Table 🌍  
1. **Name tag:** `Public route table`  Attach to `WordPressVPC`.  
2. **Edit Routes** ➝ Add a route:  
   - **Destination:** `0.0.0.0/0`  
   - **Target:** Internet Gateway (`WordPressIGW`)  

### Private Route Tables 🔒  
- **Private Route Table 1:** ❌ No direct internet access.  
- **Private Route Table 2:** ❌ No direct internet access.  
- If **NAT Gateway** or **VPC Peering** is needed for private internet access, configure routes later.  

---

## Step 5: Security Group and NACL Configuration 🔐  
### Create a Security Group  
- **Security Group Name:** `WordPress SG`  
- **VPC:** `WordPressVPC`  

#### Inbound Rules ✅  
| Protocol | Port | Source |
|----------|------|--------|
| HTTP     | 80   | `0.0.0.0/0` 🌍 (Web Access) |
| HTTPS    | 443  | `0.0.0.0/0` 🔒 (Secure Web Access) |
| SSH      | 22   | Your IP Address (For Remote Admin) |

### Network Access Control Lists (NACLs) 🛡️  
- Optionally configure **NACLs** for additional security.  
- Default NACL settings are sufficient for most cases.  

---

## Step 6: Testing the VPC Setup 🧪  
✅ **Launch an EC2 instance** in your public subnet.  
✅ **Verify internet connectivity** by pinging an external site.  
✅ **Ensure SSH access** from your local machine (if port 22 is open).  
🚀 **If everything works, the VPC setup is complete!** 🎉  
