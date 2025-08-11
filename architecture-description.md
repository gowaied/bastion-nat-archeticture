# Architecture Description

## Overview
This architecture establishes a secure environment where private EC2 instances remain hidden from direct internet access, while still retaining the ability to patch and update via outbound connections.

## Components

- **VPC & Subnets**  
  One VPC contains:
  - Public Subnet: hosts the Bastion Host and NAT Gateway  
  - Private Subnet: hosts application or backend EC2 instance

- **Internet Gateway (IGW)**  
  Enables inbound/outbound internet traffic for resources in the public subnet.

- **Bastion Host**  
  Deployed in the public subnet; receives SSH traffic from an external client to allow secure management of private resources.

- **NAT Gateway**  
  Also located in the public subnet; enables instances in the private subnet to initiate outbound internet traffic (e.g., software updates), while blocking inbound connections.

- **Private EC2 Instance**  
  Resides in a private subnet with no direct access from the internet. All outgoing traffic is routed through the NAT Gateway.

- **Route Tables**  
  - Public Subnet Route Table: directs 0.0.0.0/0 → Internet Gateway  
  - Private Subnet Route Table: routes 0.0.0.0/0 → NAT Gateway

## Security Measures
- Private instances are unreachable directly from the internet.
- Bastion Host acts as a secure jump server and can be further locked down with Security Groups and SSH key restrictions.
