# Automated Deployment of Web Servers with Auto Scaling Group and Load Balancer

## Overview
This project demonstrates the deployment of a scalable web server environment using AWS Auto Scaling Groups (ASG) in conjunction with an Elastic Load Balancer (ELB). By following this guide, you will be able to create a highly available and scalable web server infrastructure that automatically adjusts capacity based on demand.

## Prerequisites
Before proceeding with the deployment, ensure you have the following:
- An AWS account with appropriate IAM permissions.
- AWS CLI installed and configured.
- Basic knowledge of AWS services, including EC2, Auto Scaling Groups, and Load Balancers.
- Git installed on your local machine.
- SSH key pair set up in AWS for accessing EC2 instances.

## Clone the Repository
```sh
# Clone the GitHub repository
git clone https://github.com/YogitaBadhe/aws-asg-lb-webhosting.git

# Navigate into the project directory
cd aws-asg-lb-webhosting
```

## Deployment Steps

### 1. Configure Security Groups (SG)
- **Instance-Level SG:** Ensure that the security group associated with EC2 instances allows HTTP (port 80) and HTTPS (port 443) traffic.
- **Load Balancer SG:** Configure the security group for the Load Balancer to permit HTTP (port 80) and HTTPS (port 443) traffic.

### 2. Instance-Level Configuration
- **Package Management:** Install necessary packages and configure paths.
- **Web Server Path and Port:**
  - **Linux:** `/var/www/html/index.html` (Port 80)
  - **Windows:** `C:/inetpub/wwwroot/index.html` (Port 80)

### 3. Create an Auto Scaling Group (ASG)
- Define the parameters for the ASG, including minimum, maximum, and desired capacities.

### 4. Create Launch Configuration/Template
- **AMI Selection:** Use an Amazon Linux AMI or another Linux-based AMI.
- **User Data Script:** Add the following script to initialize the instances:

```bash
#!/bin/bash
yum update -y
yum install httpd -y
systemctl start httpd
systemctl enable httpd
usermod -a -G apache ec2-user
chmod 777 /var/www/html
cd /var/www/html
echo "<h1>Hello from $(hostname -f) webserver</h1>" > /var/www/html/index.html
```

### 5. Choose Instance Type
- **On-Demand or Spot Instances:** Decide between on-demand or spot instances based on cost and availability requirements.

### 6. Define Scaling Parameters
- Configure the **desired capacity**, **maximum capacity**, and **minimum capacity** settings for the ASG.

### 7. Attach Load Balancer to ASG
- Link the **Elastic Load Balancer** to the Auto Scaling Group to distribute incoming traffic evenly.

### 8. Verify Deployment
- **EC2 Management Console:** Monitor instance health and status.
- **Testing:**
  - Obtain the public IP of an instance and verify it serves content via a web browser.
  - Check if the Load Balancer properly routes traffic to healthy instances.

## Cleanup
To remove the deployed resources and avoid unnecessary costs:

### 1. Delete Auto Scaling Group (ASG)
- The associated EC2 instances will be terminated automatically.

### 2. Delete Target Group
- Remove the target group from the Load Balancer configuration.

### 3. Delete Load Balancer
- Remove the Elastic Load Balancer to complete the cleanup process.

## Summary
This project provides a detailed step-by-step guide to deploying a scalable web server infrastructure using AWS services. It ensures high availability and load balancing for your applications, making it suitable for production environments where scalability and reliability are critical.

