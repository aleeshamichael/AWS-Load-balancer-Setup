# AWS-Load-balancer-Setup
# AWS Load Balancer and Target Group Configuration

## Overview
This repository contains step-by-step instructions for setting up a Load Balancer and Target Group in AWS. The setup includes creating a VPC, configuring subnets, launching EC2 instances, and installing an Apache web server.

## Steps to Configure Load Balancer and Target Group

### 1. Create a VPC
- Set up a VPC.
- Attach an Internet Gateway to the VPC.

### 2. Configure Subnets
- Create two public subnets in Availability Zones 2a and 2b.
- Create a private subnet in Availability Zone 2a.

### 3. Set Up Route Tables
- Associate the Internet Gateway with public subnets.
- Create a NAT Gateway using a public subnet.
- Create a route table for the private subnet and associate it with the NAT Gateway.

### 4. Configure Security Group
- Allow inbound SSH and HTTP access.

### 5. Launch EC2 Instances
- Launch an instance in the public subnet (AZ 2a).
- Launch another instance in the private subnet (AZ 2a).
- Use the public instance to access the private instance.

### 6. Install Apache Web Server on Private Instance
```bash
sudo su
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
cd /var/www/html
vi index.html
```
Add the following content:
```html
<h1>Welcome</h1>
```
Save and exit:
```bash
ESC then :wq
```

### 7. Configure Target Group
- Create a target group and add the private instance in AZ 2a.

### 8. Set Up Load Balancer
- Configure a Load Balancer using Availability Zones 2a and 2b.

### 9. Access the Web Page
- Copy the Load Balancer's DNS name.
- Open it in a browser to view the index page.

## Repository Contents
- **README.md** - This guide.
- **Steps to configure Load Balancer and Target Group in AWS.docx** - Detailed steps with screenshots.
- **install_apache.sh** - Script to install Apache on a private instance.

## Installation Script
Save the following as `install_apache.sh`:
```bash
#!/bin/bash
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
echo "<h1>Welcome</h1>" | sudo tee /var/www/html/index.html
```

## License
MIT License.
