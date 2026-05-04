# aws-secure-vpc-project
## Secure AWS VPC Architecture with Private Subnets

<img width="1536" height="1024" alt="architecture-diagram png" src="https://github.com/user-attachments/assets/8283aeb3-ccf1-4a5f-8656-0a8b0420f88e" />

📖 Overview

This project demonstrates the design and implementation of a secure AWS Virtual Private Cloud (VPC) architecture that isolates internal resources while allowing controlled outbound access and centralized monitoring.

The goal is to reflect real-world cloud design patterns used to:

Protect backend systems from direct internet exposure
Enforce least privilege access
Maintain visibility through logging and monitoring

🏗️ Architecture
Core Services Used
Amazon VPC
Amazon EC2
AWS CloudTrail
Amazon CloudWatch
NAT Gateway
Internet Gateway

🎯 Design Goals
Network Isolation
Separate public-facing and internal resources
Controlled Internet Access
Allow outbound traffic from private resources without exposing them
Secure Access Management
Restrict inbound access and enforce least privilege
Monitoring & Visibility
Track activity and maintain logs for auditing

🌐 Network Architecture
VPC
CIDR: 10.0.0.0/16
Public Subnet
CIDR: 10.0.1.0/24
Hosts:
Bastion Host (EC2)
NAT Gateway
Route:
0.0.0.0/0 → Internet Gateway

Private Subnet
CIDR: 10.0.2.0/24
Hosts:
Private EC2 Instance
Route:
0.0.0.0/0 → NAT Gateway

🔐 Security Design
Access Control
Bastion Host:
SSH allowed from trusted IP only
Private EC2:
SSH allowed only from Bastion Host
IAM
EC2 instances use IAM roles
No hardcoded credentials
Least privilege enforced

🔄 Traffic Flow
Inbound
Internet → Internet Gateway → Bastion Host (Public Subnet)

Outbound (Private Instance)
Private EC2 → NAT Gateway → Internet Gateway → Internet

✔ Private resources can access the internet
❌ Private resources cannot be accessed from the internet

📊 Monitoring & Logging
AWS CloudTrail → API activity logging
CloudWatch → Metrics and logs
VPC Flow Logs → Network traffic visibility

🚀 Deployment Steps (High-Level)
Create VPC and subnets
Attach Internet Gateway
Configure route tables
Deploy NAT Gateway
Launch Bastion Host (public subnet)
Launch Private EC2 (private subnet)
Configure security groups
Attach IAM roles
Enable logging (CloudTrail, Flow Logs)

🔧 Future Improvements
Replace SSH with AWS Systems Manager Session Manager
Deploy across multiple Availability Zones
Automate with Terraform or CloudFormation
Integrate GuardDuty and Security Hub
Implement centralized alerting

📎 Related Content

Medium Article: https://medium.com/p/d0bad75df9f0?postPublishedType=initial

LinkedIn Post: https://www.linkedin.com/posts/johnnylouis_aws-cloudengineering-cybersecurity-share-7456888790440255489-5pnq?utm_source=share&utm_medium=member_desktop&rcm=ACoAAAScb6gB1duzxBcU2AV7tzUXSdHGK0RxUlE
