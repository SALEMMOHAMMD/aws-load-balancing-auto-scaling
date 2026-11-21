# aws-load-balancing-auto-scaling
AWS Lab 6 - Load Balancing and Auto Scaling
# AWS Lab 6 – Load Balancing and Auto Scaling

## 1. Project Overview

In this lab, I implemented a scalable and highly available web application infrastructure using Amazon Web Services (AWS).

The main goal was to configure an Application Load Balancer to distribute incoming traffic across multiple EC2 instances and implement EC2 Auto Scaling to automatically adjust the number of instances based on application demand.

## 2. AWS Services Used

- **Amazon EC2:** Provides the compute instances that host the web application.
- **Amazon Machine Image (AMI):** Used to create an image of the existing web server.
- **Application Load Balancer (ALB):** Distributes incoming HTTP traffic across multiple instances.
- **EC2 Auto Scaling:** Automatically manages the number of running EC2 instances.
- **Amazon CloudWatch:** Monitors CPU utilization and scaling alarms.
- **Amazon VPC:** Provides the networking environment.
- **Target Groups:** Manage the EC2 instances receiving traffic from the load balancer.

## 3. Project Implementation

### Step 1 – Create an AMI

Created an Amazon Machine Image (AMI) from the existing Web Server 1 instance.

This AMI was used as the base image for launching identical EC2 instances through Auto Scaling.

### Step 2 – Configure Target Group

Created a Target Group named `LabGroup` to register and monitor EC2 instances.

The target group is responsible for routing traffic from the Application Load Balancer to healthy instances.

### Step 3 – Create Application Load Balancer

Created an internet-facing Application Load Balancer named `LabELB`.

Configuration:
- Load Balancer Type: Application Load Balancer
- Scheme: Internet-facing
- Listener: HTTP (Port 80)
- Availability Zones: Two Public Subnets
- Target Group: LabGroup
- Security Group: Web Security Group

### Step 4 – Create Launch Template

Created a Launch Template named `LabConfig`.

Configuration:
- AMI: Web Server AMI
- Instance Type: t2.micro
- Key Pair: vockey
- Security Group: Web Security Group
- Detailed CloudWatch Monitoring: Enabled

### Step 5 – Configure Auto Scaling Group

Created an Auto Scaling Group named `Lab Auto Scaling Group`.

Scaling configuration:

| Configuration | Value |
|---|---|
| Desired Capacity | 2 |
| Minimum Capacity | 2 |
| Maximum Capacity | 6 |
| Scaling Policy | Target Tracking |
| Metric Type | Average CPU Utilization |
| Target Value | 60% |

The Auto Scaling Group uses two Private Subnets and is attached to the `LabGroup` Target Group.

### Step 6 – Verify Load Balancing

Verified that the Auto Scaling Group launched two EC2 instances.

Checked the Target Group to confirm that both instances were registered and their health status became healthy.

Accessed the web application using the Application Load Balancer DNS name to verify that traffic was successfully routed to the application.

### Step 7 – Test Auto Scaling

Used the application's Load Test feature to generate additional CPU load.

Monitored CPU utilization through Amazon CloudWatch and observed the scaling alarms.

The Auto Scaling configuration was designed to launch additional EC2 instances when application demand increased, up to the configured maximum capacity of six instances.

## 4. Project Screenshots

### 4.1 Web Application

The web application accessed through the Application Load Balancer DNS name.

![Web Application](1-Web-App.png)

### 4.2 Auto Scaling

Screenshot showing the Auto Scaling configuration and EC2 scaling environment.

![Auto Scaling](2-Auto-Scaling.png)

### 4.3 AWS Architecture

The architecture diagram illustrates the infrastructure components, including the Load Balancer, Target Group, EC2 instances, and Auto Scaling configuration.

![AWS Architecture](3-Architecture.png)

## 5. Key Skills Gained

- Creating and managing Amazon Machine Images (AMI).
- Configuring Application Load Balancers.
- Working with Target Groups and Health Checks.
- Creating EC2 Launch Templates.
- Configuring Auto Scaling Groups and Scaling Policies.
- Monitoring CPU utilization using CloudWatch.
- Understanding High Availability and Scalability.
- Distributing application traffic across multiple EC2 instances.

## 6. Conclusion

Successfully completed an AWS hands-on lab focused on Load Balancing and Auto Scaling.

This project provided practical experience in building scalable cloud infrastructure, distributing incoming traffic, monitoring application performance, and managing EC2 capacity based on demand.

**Technologies:** AWS | EC2 | AMI | Application Load Balancer | Auto Scaling | CloudWatch | VPC
