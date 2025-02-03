# 🚀 Automated Deployment of Web Servers with Auto Scaling Group & Load Balancer

## 📌 Introduction
This project demonstrates the **automated deployment** of a scalable web server environment using **AWS Auto Scaling Groups (ASG)** and **Elastic Load Balancer (ELB)**. It ensures **high availability, scalability, and load balancing** for your applications. By following this guide, you'll deploy a robust infrastructure capable of handling variable traffic loads efficiently.

---

## 🛠️ Prerequisites
Before you begin, ensure you have the following:

- ✅ **AWS Account** with access to EC2, Auto Scaling Groups, and Load Balancer services.
- ✅ **AWS CLI** installed and configured on your local machine.
- ✅ **IAM User/Role** with necessary permissions for ASG and Load Balancer.
- ✅ **Basic Knowledge of AWS & Linux** (recommended for troubleshooting).
- ✅ **Git Installed** to clone the repository.

---

## 📥 Clone Repository
To get started, clone this repository and navigate into the project directory:
```sh
# Clone the repository
git clone https://github.com/YogitaBadhe/aws-asg-lb-webhosting.git

# Change to the project directory
cd aws-asg-lb-webhosting.git
```

---

## 📌 Key Features
- **Elastic Load Balancing**: Distributes traffic across multiple instances.
- **Auto Scaling Group**: Dynamically scales EC2 instances based on demand.
- **Automated Web Server Setup**: Deploys a web server with required configurations.
- **Security Best Practices**: Ensures proper security group configurations.

---

## ⚙️ Configuration Details

### 🔒 Security Group Settings
- **Instance-Level Security Group**
  - Allow **HTTP (Port 80)** and **HTTPS (Port 443)** traffic.
- **Load Balancer Security Group**
  - Ensure that it allows HTTP & HTTPS traffic as well.

### 📂 Web Server Configuration
- **Linux Web Server Path:** `/var/www/html/index.html` (Port 80)
- **Windows Web Server Path:** `C:/inetpub/wwwroot/index.html` (Port 80)

---

## 🚀 Deployment Steps
### 🏗️ 1. Create Auto Scaling Group (ASG)
- Define **minimum, maximum, and desired** capacities for the web server instances.

### ⚙️ 2. Create Launch Configuration/Template
- Use an **Amazon Linux AMI** or any **Linux-based AMI**.
- Insert the following **user data script** to configure the web server:
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

### 🖥️ 3. Choose Instance Type
- Decide between **On-Demand** or **Spot Instances** based on cost and availability.

### 📊 4. Define Scaling Parameters
- Configure **desired capacity, maximum capacity, and minimum capacity** for the ASG.

### 🔗 5. Attach Load Balancer to ASG
- Link the **Elastic Load Balancer** to the ASG to distribute incoming traffic.

### ✅ 6. Verify Deployment
- Use **EC2 Management Console** to monitor instance health.

### 🔎 7. Testing Your Deployment
- **Public IP Test**: Get the **public IP** of an instance and open it in a browser.
- **Load Balancer Test**: Ensure the **Load Balancer** is properly routing traffic.

---

## 🧹 Cleanup (Resource Deletion)
To avoid unnecessary costs, remove the created resources after testing:

1. **Delete Auto Scaling Group** (This will terminate associated instances).
2. **Delete Target Group** from the Load Balancer configuration.
3. **Delete Load Balancer** to free up resources.

---

## 🎯 Conclusion
This guide provides a **step-by-step approach** to deploying a **scalable, high-availability** web server infrastructure on AWS using **Auto Scaling Groups** and **Load Balancer**. Happy deploying! 🚀🎉

---
