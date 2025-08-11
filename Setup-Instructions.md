# Setup Instructions

## Prerequisites
- An AWS account with IAM permissions to manage VPCs, subnets, EC2, IGW, NAT, and security groups
- AWS CLI or AWS Console access

## Deployment Steps

1. **Create VPC & Subnets**
   - VPC with a CIDR block (e.g. 172.16.0.0/16)
   - Public Subnet (e.g. 172.16.1.0/24)
   - Private Subnet (e.g. 172.16.2.0/24)

2. **Internet Gateway**
   - Attach IGW to the VPC
   - Update public subnet route table: `0.0.0.0/0` → IGW

3. **NAT Gateway & Elastic IP**
   - Allocate Elastic IP
   - Deploy NAT Gateway in the public subnet
   - Update private subnet route table: `0.0.0.0/0` → NAT Gateway

4. **Bastion Host Deployment**
   - Launch an EC2 instance in the public subnet
   - Configure security group to allow SSH from your IP only

5. **Private EC2 Instance**
   - Launch EC2 in the private subnet
   - Assign security group that allows SSH from the Bastion Host

6. **SSH Access Flow**
   - SSH into Bastion Host from your local machine
   - From there, SSH into the private instance (e.g. `ssh -A ec2-user@private-instance`)

## Optional Enhancements
- Enable Session Manager for Bastion (AWS Systems Manager)
- Add CloudWatch monitoring and automated backups
- Use Terraform or CloudFormation for infrastructure as code
