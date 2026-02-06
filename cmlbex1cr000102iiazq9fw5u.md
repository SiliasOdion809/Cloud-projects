---
title: "Deploying Multiple EC2 Instances with Apache and Nginx Behind an AWS Load Balancer (With Monitoring & Automated Backups)"
seoTitle: "Building a resilient EC2 architecture on AWS"
seoDescription: "Deploy Apache and Nginx on EC2, configure an AWS Load Balancer, enable CloudWatch monitoring, and set up automated backups in this practical DevOps project."
datePublished: Fri Feb 06 2026 21:43:43 GMT+0000 (Coordinated Universal Time)
cuid: cmlbex1cr000102iiazq9fw5u
slug: deploying-multiple-ec2-instances-with-apache-and-nginx-behind-an-aws-load-balancer-with-monitoring-and-automated-backups
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1770413482098/754d2b1d-bdff-4fc5-93d5-1ede0704f756.png
tags: aws, cloud-computing, load-balancing, ec2-instance

---

## Introduction

In this project, I deployed two **Amazon EC2** instances running **Amazon Linux**, installed **Apache** on one instance and **Nginx** on the other, and placed both behind an **AWS Application Load Balancer**.

To make the setup more production-ready, I also configured:

* **Monitoring and alerting using Amazon CloudWatch**
    
* **Automated backups using EC2 snapshots**
    

This project demonstrates core AWS skills such as compute provisioning, traffic distribution, monitoring, and disaster recovery.

---

## Architecture Overview

![https://miro.medium.com/v2/resize%3Afit%3A1400/0%2AGqO1VSDirA9PeH5t.png](https://miro.medium.com/v2/resize%3Afit%3A1400/0%2AGqO1VSDirA9PeH5t.png align="left")

![https://docs.aws.amazon.com/images/autoscaling/ec2/userguide/images/elb-tutorial-architecture-diagram.png](https://docs.aws.amazon.com/images/autoscaling/ec2/userguide/images/elb-tutorial-architecture-diagram.png align="left")

**Architecture Components**

* 2 EC2 Instances (Amazon Linux)
    
* Apache Web Server (Instance 1)
    
* Nginx Web Server (Instance 2)
    
* 1 Application Load Balancer
    
* 1 Target Group
    
* Amazon CloudWatch for monitoring
    
* Automated EC2 snapshots for backups
    

---

## Step 1: Launch Two EC2 Instances

I logged into the AWS Management Console and navigated to **Amazon EC2**.

### Configuration Steps

1. Click **Launch Instance**
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770403937456/c02b6916-d9b3-4787-b88f-853c96db7391.png align="center")
    
2. Select **Amazon Linux**
    
3. Choose instance type (e.g., `t2.micro`)
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770404004725/9dea3b14-c446-4b7d-a917-b7a36b594def.png align="center")
    
4. Create or select a key pair
    
5. Configure a Security Group:
    
    * SSH (22) — My IP
        
    * HTTP (80) — Anywhere
        
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770404040046/20e3669b-bf49-4c56-8361-f846157ae80c.png align="center")
    
6. Launch **two separate EC2 instances**
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770404068349/d6adad62-e784-42c3-adb4-a8fd2dd271b2.png align="center")
    

---

## Step 2: SSH into Both Instances

Using the public IPs, I connected to each instance via SSH.

```plaintext
ssh -i mykey.pem ec2-user@<EC2_PUBLIC_IP>
```

I confirmed successful access on both instances.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770404517137/9c583460-6b21-44f4-81b8-d8e2b132f1de.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770404526291/997765f7-cae1-409f-9290-752ccf310a65.png align="center")

---

## Step 3: Install Apache on the First Instance

On the first EC2 instance, I installed **Apache HTTP Server**.

```plaintext
sudo yum update -y
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
sudo systemctl status httpd
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770404747214/50b4d788-0a54-442c-8283-47c1b6c2cdff.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770404831213/e7ceae59-eeaf-4f22-af81-9bf7656543d7.png align="center")

I customized the web page:

```plaintext
sudo nano /var/www/html/index.html
```

```plaintext
<h1>Apache Server - EC2 Instance 1</h1>
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770405125497/09a721ed-49ea-4a0e-88b5-843c20f45e9f.png align="center")

## Step 4: Install Nginx on the Second Instance

On the second EC2 instance, I installed **Nginx**.

```plaintext
sudo yum update -y
sudo yum install nginx -y
sudo systemctl start nginx
sudo systemctl enable nginx
sudo systemctl status nginx
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770405276353/9210f00d-5c0c-40ec-9962-1001ecb3833d.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770405384299/9a7e24a1-5c74-4e0b-acf9-e14200a782ec.png align="center")

I edited the default Nginx page:

```plaintext
sudo nano /usr/share/nginx/html/index.html
```

```plaintext
<h1>Nginx Server - EC2 Instance 2</h1>
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770406446479/9eddc904-7c0a-477e-a75c-b39560069eef.png align="center")

---

## Step 5: Create a Target Group

I created a Target Group to route traffic to the instances.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770406759104/0222b24a-7678-459b-96bd-3035cfceba06.png align="center")

### Target Group Configuration

* Target type: **Instance**
    
* Protocol: **HTTP**
    
* Port: **80**
    
* Health check path: `/`
    

Both EC2 instances were registered and marked **healthy**.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770406820932/e28f72e5-d028-48c1-9d75-312a69ddb361.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770406997836/b0d5d767-f3c7-4536-967e-c30dcd75b6b7.png align="center")

---

## Step 6: Create an Application Load Balancer

Next, I created an **Application Load Balancer**.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770407459009/635b3aa0-6e85-4b42-b04d-47ff58f1b8d9.png align="center")

### Load Balancer Settings

* Scheme: Internet-facing
    
* Listener: HTTP (80)
    
* Availability Zones: Same as EC2 instances
    
* Forward traffic to the created Target Group
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770407713288/d606622e-ab7f-4df1-a520-f0646e35e940.png align="center")

---

## Step 7: Access the Load Balancer DNS

Once the load balancer became active, I accessed its DNS name in a browser.

```plaintext
http://<load-balancer-dns-name>
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770407875175/2e5d5ee9-d14f-4b15-ad4a-6a59bc5d69c9.png align="center")

Refreshing the page alternated between:

* Apache server response
    
* Nginx server response
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770408062050/8c265d45-cdee-44f6-a8b4-7045f50dd284.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770408071172/bc7e5451-b241-4d61-a896-6e186ebc4ed7.png align="center")

---

## Step 8: Enable Monitoring with Amazon CloudWatch

To monitor performance and availability, I used **Amazon CloudWatch**.

### What I Monitored

* EC2 CPU Utilization
    
* Network In / Network Out
    
* Load Balancer request count
    
* Target group health status
    

### Alarm Configuration

* Created a CloudWatch alarm to trigger when CPU utilization exceeds a threshold
    
* Notifications configured using SNS
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770413720756/e091fddb-6683-41e7-b940-aef632c98a57.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770411905803/5911fc8b-b746-4c21-9b55-1c27be1e2dd6.png align="center")

---

## Step 9: Configure Automated Backups Using EC2 Snapshots

To ensure disaster recovery, I enabled **automated backups** by creating EC2 snapshots.

### Backup Strategy

* Created AMIs or EBS snapshots for both instances
    
* Configured lifecycle rules to:
    
    * Run backups automatically
        
    * Retain snapshots for a defined period
        

This ensures the instances can be restored quickly in case of failure or data loss.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770413373339/95c8bbff-d5a4-4e5d-9961-55f44d6cc9c7.png align="center")

---

## Key Takeaways

* Load balancers distribute traffic efficiently across multiple instances
    
* CloudWatch provides visibility into system performance and health
    
* Automated backups are essential for fault tolerance and recovery
    
* This setup reflects real-world AWS production practices
    

---

## Conclusion

This project showcases how to deploy multiple EC2 instances with different web servers, expose them through an Application Load Balancer, and enhance the setup with monitoring and automated backups. It demonstrates foundational AWS skills required for Cloud and DevOps roles, including scalability, observability, and resilience.