---
title: "Launching an EC2 Instance and Hosting a Web Page Using Apache on AWS"
seoTitle: "Deploying a Web Server on AWS EC2 with Apache"
seoDescription: "A hands-on DevOps guide to deploying an Apache web server on AWS EC2, configuring SSH and HTTP access, and hosting a website."
datePublished: Wed Feb 04 2026 12:38:07 GMT+0000 (Coordinated Universal Time)
cuid: cml80jowb000a02lfbi8abygs
slug: launching-an-ec2-instance-and-hosting-a-web-page-using-apache-on-aws
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1770203028487/74519bef-a485-4b72-8784-3e3f4868fce7.png
tags: ec2, aws, cloud-computing, devops, tech

---

## Introduction

Amazon Elastic Compute Cloud (EC2) is a core AWS service that allows users to run virtual servers in the cloud. These servers can be used to host websites, applications, and other services.

In this blog, I will give a **detailed step-by-step explanation** of how I:

* Launched an EC2 instance on AWS
    
* Configured security groups to allow SSH and HTTP traffic
    
* Connected to the instance from my local machine using SSH
    
* Installed and configured the Apache web server
    
* Edited the default Apache web page to display my name
    
* Accessed the web page using the EC2 public IP address
    
* Safely terminated the EC2 instance after completion
    

---

## Step 1: Logging into AWS and Navigating to EC2

I started by logging into the **AWS Management Console** using my AWS account. From the AWS services menu, I searched for **EC2** and clicked on it to open the EC2 Dashboard.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770203265374/ec8e657b-8228-44ee-9b9f-a50c9d56c12b.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770203272049/afa36778-bd72-4c25-8f91-27267b7aad51.png align="center")

---

## Step 2: Launching a New EC2 Instance

From the EC2 Dashboard, I clicked **Launch Instance**.

### Instance Configuration

* **Name:** I assigned a name to the instance for easy identification.
    
* **Amazon Machine Image (AMI):** I selected an **Ubuntu Server / Amazon Linux AMI**.
    
* **Instance Type:** I chose `t3.micro`, which is eligible for the AWS Free Tier.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770203451435/a2186e48-c5f2-4357-97ba-1d8fc2f7383d.png align="center")

---

## Step 3: Creating or Selecting a Key Pair

To securely connect to the EC2 instance, AWS requires a **key pair**.

* I created a new key pair (or selected an existing one).
    
* I downloaded the private key file (`.pem`) and stored it safely on my local machine.
    

This key is required for SSH access to the instance.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770203654045/a65ed75d-ffe5-4e2c-935d-ac5331fdfa0e.png align="center")

---

## Step 4: Configuring the Security Group

A **security group** acts as a virtual firewall for the EC2 instance.

I configured the inbound rules to allow:

* **SSH (Port 22)** – for remote access from my local machine
    
* **HTTP (Port 80)** – to allow web traffic to the Apache server
    

These rules ensure that I can connect to the instance and that the web page can be accessed from a browser.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770203766818/3cfaa833-3f55-4df1-aa35-139490aafc69.png align="center")

---

## Step 5: Launching the Instance

After reviewing all configurations, I clicked **Launch Instance**. Within a few minutes, the instance entered the **running** state.

I then copied the **public IP address**, which would be used to connect to the server and access the website.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770204203206/1f1b6c11-48e4-4dad-8176-5c125c1a6c3e.png align="center")

---

## Step 6: Connecting to the EC2 Instance Using SSH

On my local machine, I opened the terminal and navigated to the directory containing the private key file.

I used SSH to connect to the instance using the public IP address. Once connected, I gained command-line access to the remote server.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770204486849/837bcf4c-6631-40b1-92d2-762d2459852c.png align="center")

---

## Step 7: Updating the Server and Installing Apache

After connecting to the instance, I updated the system packages to ensure everything was up to date.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770204719811/a9945c6c-96c7-4a45-90bc-95986b028941.png align="center")

Next, I installed **Apache2**, which is a widely used open-source web server.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770205493221/cf04ec59-c5a6-4642-bb42-468c463bed3a.png align="center")

Once installation was complete, I started the Apache service and verified that it was running correctly.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770205502461/dd023a83-7459-47a7-97d9-32dc1eb2cd87.png align="center")

---

## Step 8: Editing the Default Apache Web Page

Apache stores its default web page in the `/var/www/html` directory.

* I navigated to this directory
    
* I opened the `index.html` file
    
* I replaced the default content with a simple message displaying **my name**
    

This customization helped confirm that the server was correctly serving my own content.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770206902468/ee9334cb-a279-4eef-bd13-0e59b28cdaa6.png align="center")

---

## Step 9: Accessing the Web Page via Browser

After configuring Apache, I opened my web browser and entered the **public IP address** of the EC2 instance.

The page loaded successfully and displayed my name, confirming that:

* Apache was running
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770206959256/7935d27d-271f-4747-95bc-56078100a7b6.png align="center")
    
* HTTP traffic was allowed in the security group
    
* The EC2 instance was accessible from the internet
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770207210387/015acf79-5ab2-4d2c-bf4f-bcff7bde870a.png align="center")

---

## Step 10: Terminating the EC2 Instance

After completing the project, I returned to the EC2 Dashboard and selected the instance.

To avoid unnecessary charges, I clicked **Terminate Instance**. This permanently deleted the EC2 instance and released its resources.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770207697116/4afacc1f-25a8-49b0-ac5a-ee05cdda2052.png align="center")

---

## Conclusion

This step-by-step project demonstrated how to deploy a basic web server using AWS EC2 and Apache. It provided hands-on experience with cloud infrastructure, Linux server management, security groups, and web hosting.

This foundational knowledge is essential for more advanced cloud and DevOps projects such as deploying applications, configuring load balancers, and automating infrastructure.