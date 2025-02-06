# Setting Up an EC2 Instance for WordPress Hosting 🚀

This guide outlines the steps to launch an EC2 instance for hosting your WordPress application. 🖥️

---

## Step 1: Choose an Amazon Machine Image (AMI) 🖼️
- Log in to the AWS Management Console as VPCAdminUser.
- Under Name and Tags, enter a name like `WordPress WebServer`
- Select `Amazon Linux 2 AMI (HVM), SSD Volume Type` (Free Tier eligible). ✔️

## Step 2: Choose an Instance Type ⚙️
- Choose `t2.micro` (Free Tier eligible). 🏷️

## Step 3: Create or Select Key Pair 🔑
- Choose **Create a new key pair** or use an existing one.
- Name it `your-key`.
- **Download the .pem file** and store it safely. 💾

## Step 4: Configure Instance Details ⚙️
- **VPC**: Select `WordPressVPC` (the VPC created earlier).
- **Subnet**: Choose `Public Subnet 1`
- **Auto-assign Public IP**: `Enable` 🌐

## Step 5: Configure Security Group 🔒
- Select `WordPress SG` (created during VPC setup).
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

- locate to your-key.pem
```bash
chmod 400 your-key.pem
ssh -i your-key.pem ec2-user@your-public-ip
```

## Step 8: Set Up LAMP Stack on Amazon Linux 🔧

steps to set up a **LAMP Stack** (Linux, Apache, MariaDB, PHP) on an **Amazon Linux** instance. 

### 8.1. **Update the system** 🖥️
Ensure your system is up to date:
```bash
sudo yum update -y
```
### 8.2. Install Apache (httpd) 🌐
Install Apache web server:
```bash
sudo yum install -y httpd
```
### 8.3. Start Apache 🔥
Start the Apache web server:
```bash
sudo systemctl start httpd
```
### 8.4. Enable Apache to start on boot 🔄
Enable Apache to start automatically on boot:
```bash
sudo systemctl enable httpd
```
### 8.5. Check Apache status ✅
Verify Apache is running:
```bash
sudo systemctl status httpd
```
### 8.6. Install MariaDB 🗄️
Install MariaDB (MySQL-compatible database server):
```bash
sudo yum install -y mariadb-server
```
### 8.7. Start MariaDB 💾
Start the MariaDB service:
```bash
sudo systemctl start mariadb
```
### 8.8. Enable MariaDB to start on boot 🔄
Enable MariaDB to start automatically on boot:
```bash
sudo systemctl enable mariadb
```
### 8.9. Secure MariaDB Installation 🔒
Run the security script to set the root password, remove anonymous users, disable remote root login, and remove the test database:
```bash
sudo mysql_secure_installation
```
### 8.10. Check MariaDB status ✅
Verify MariaDB is running:
```bash
sudo systemctl status mariadb
```
### 8.11. Enable PHP 8.1 💻
Enable PHP 8.1 using Amazon Linux Extras:
```bash
sudo amazon-linux-extras enable php8.1
```
### 8.12. Install PHP and required extensions ⚙️
Install PHP along with necessary modules (for MySQL, Curl, GD, etc.):
```bash
sudo yum install -y php php-cli php-mysqlnd php-curl php-gd php-mbstring php-xml php-zip unzip
```
### 8.13. Restart Apache 🔄
Restart Apache to load PHP:
```bash
sudo systemctl restart httpd
```
### 8.14. Download phpMyAdmin (optional) 📦
Navigate to the Apache web directory and download the latest version of phpMyAdmin:
```bash
cd /var/www/html
sudo wget https://www.phpmyadmin.net/downloads/phpMyAdmin-latest-all-languages.tar.gz
```
### 8.15. Extract phpMyAdmin 🗂️
Extract the downloaded archive:
```bash
sudo tar xvf phpMyAdmin-latest-all-languages.tar.gz
```
### 8.16. Rename phpMyAdmin folder ✏️
Rename the extracted folder for better access:
```bash
sudo mv phpMyAdmin-* phpmyadmin
```
### 8.17. Set proper ownership 🔑
Ensure the Apache user has ownership of the phpMyAdmin directory:
```bash
sudo chown -R apache:apache /var/www/html/phpmyadmin
```
### 8.18. Restart Apache 🔄
Restart Apache again to apply changes:
```bash
sudo systemctl restart httpd
```
### 8.19. Create a PHP test file 📝
Create a phpinfo.php file to verify PHP is working:
```bash
echo "<?php phpinfo(); ?>" | sudo tee /var/www/html/info.php
```
### 8.20. Test PHP and phpMyAdmin 🌍
Open your browser and navigate to:
```pgsql
http://your-server-ip/info.php
```
You should see the PHP information page.

Also, navigate to:
```
http://your-server-ip/phpmyadmin
```
To access phpMyAdmin.

### 8.21. Enable Apache and MariaDB on boot
Ensure Apache and MariaDB start automatically on reboot:
```bash
sudo systemctl enable httpd
sudo systemctl enable mariadb
```
