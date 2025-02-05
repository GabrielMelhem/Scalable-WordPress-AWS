# Scalable, Highly Available, and Fault-Tolerant WordPress Application on AWS
This project is part of my AWS Cloud Computing Bootcamp at Neue Fische. The goal is to demonstrate key concepts of cloud architecture, automation, and scalability within Amazon Web Services (AWS).

## Project Overview  
A **WordPress application** is a web-based content management system (CMS) that allows users to create, manage, and publish content easily.  

This project demonstrates how to implement a **Scalable, Highly Available, and Fault-Tolerant WordPress Application** on AWS to ensure:  
✅ Handling of traffic spikes (Scalability)  
✅ Minimal downtime and failover support (High Availability)  
✅ Security, performance optimization, and monitoring  

The architecture is designed using various AWS services, as illustrated in the diagram below. 

## Architecture Diagram 
![Online Resume Diagram](https://github.com/user-attachments/assets/789c6409-be75-4560-9569-62fcfa3ddd65)


## Key Features & AWS Services Used  

### 🚀 **Scalability**  
- **Auto Scaling Group (ASG)** for EC2 instances ensures the system can handle varying traffic loads.  

### 🛡️ **High Availability**  
- **Web servers (EC2) in multiple Availability Zones (AZs)** reduce downtime risks.  
- **Amazon RDS (Relational Database Service) in Multi-AZ mode** provides database failover support.  

### 🔐 **Security**  
- **AWS WAF (Web Application Firewall)** filters malicious traffic.  
- **RDS is hosted in private subnets** to prevent direct external access.  

### ⚡ **Performance Optimization**  
- **Amazon CloudFront** (CDN) speeds up content delivery.  
- **Amazon ElastiCache** (Redis/Memcached) reduces database load.  

### 📊 **Monitoring & Backups**  
- **Amazon CloudWatch** provides logging and monitoring.  
- **Automated RDS backups** ensure data safety.  

### 📂 **Static Content Hosting**  
- **Amazon S3** stores static assets like images, CSS, and JS files.  

### 🔔 **Notification System**  
- **Amazon SNS (Simple Notification Service)** sends admin alerts via email.  

---  

## 📌 **Getting Started**  
(*Steps to deploy this project will be added here soon*)
