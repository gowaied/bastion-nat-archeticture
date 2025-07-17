# bastion-nat-archeticture

# AWS Bastion Host & NAT Gateway Architecture

This project demonstrates a secure and scalable AWS architecture using:
- A **Bastion Host** for SSH access
- A **NAT Gateway** for private instances to access the internet
- Proper use of **VPC, public/private subnets, routing tables, and security groups**

## 🔧 Technologies Used
- Amazon VPC
- EC2 Instances (Bastion + Private)
- Internet Gateway (IGW)
- NAT Gateway (NGW)
- Route Tables
- Security Groups
- SSH

## 🌐 Network Design
- `Public Subnet`: Bastion Host + NAT Gateway
- `Private Subnet`: Private EC2 Instance (no public IP)
- Bastion used for secure SSH jump to the private instance
- Private instance uses NAT Gateway for outbound internet

## 🚀 How to Deploy
1. Launch VPC with appropriate subnets
2. Create NAT Gateway with Elastic IP in the public subnet
3. Launch Bastion Host with public IP in public subnet
4. Launch Private EC2 instance in private subnet
5. SSH into Bastion, then to private instance
6. Private instance can access internet (e.g., yum, apt, curl)

## 🔐 Security Considerations
- Only allow SSH (port 22) to Bastion from your IP
- Only allow SSH access to private instance **from Bastion’s security group**
- No public IP on private instance

## ✍️ Author
Mohamed Gowaied
