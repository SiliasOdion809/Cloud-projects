---
title: "🚀 Deploying a Secure AWS Architecture with Bastion Host, Private EC2, NAT Gateway & Application Load Balancer (Step-by-Step Guide)"
seoTitle: "Secure AWS Architecture with Bastion Host, NAT Gateway & ALB"
seoDescription: "Learn how to build a secure AWS architecture using Bastion Host, private EC2 instances, NAT Gateway, Ansible automation, and Application Load Balancer."
datePublished: Sat Feb 14 2026 18:16:42 GMT+0000 (Coordinated Universal Time)
cuid: cmlmn1myb000502iednd4b5sj
slug: deploying-a-secure-aws-architecture-with-bastion-host-private-ec2-nat-gateway-and-application-load-balancer-step-by-step-guide
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1771068744009/bb39374e-233e-414f-bc91-a0d45d80c728.png
tags: ec2, aws, load-balancing, bastion-hosts

---

In this detailed guide, I’ll walk you through how I built a **secure production-style AWS architecture** where:

* Private EC2 instances have **no public IP**
    
* They can still **access the internet via NAT Gateway**
    
* SSH access is only possible through a **Bastion Host**
    
* I automated configuration using **Ansible**
    
* I exposed the application securely using an **Application Load Balancer**
    

This setup follows real-world **DevOps and cloud security best practices**.

---

# 🏗 Final Architecture Overview

### Architecture Components

* Custom VPC
    
* Public Subnet (Bastion Host, NAT Gateway, ALB)
    
* Private Subnet (2 Ubuntu EC2 Instances)
    
* Internet Gateway
    
* NAT Gateway
    
* Public & Private Route Tables
    
* Ansible Automation
    
* Application Load Balancer
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1771091215779/22edb932-498e-4082-9a36-96af569259bf.png align="center")
    

---

# ✅ STEP 1: Create a Custom VPC

Instead of using the default VPC, I created a new one for full control.

### Configuration:

* Name: `Custom-Bastion-VPC`
    
* IPv4 CIDR Block: `10.0.0.0/16`
    
* Enable DNS Hostnames: Yes
    
* Enable DNS Resolution: Yes
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1771071312095/4e87b6a8-e9ba-42fa-8551-73c56cd15d04.png align="center")

---

# ✅ STEP 2: Create Public and Private Subnets

Inside the VPC, I created two subnets.

### 🔓 Public Subnet

* Name: `Public-Subnet`
    
* CIDR: `10.0.1.0/24`
    
* Used for:
    
    * Bastion Host
        
    * NAT Gateway
        
    * Application Load Balancer
        

### 🔒 Private Subnet

* Name: `Private-Subnet`
    
* CIDR: `10.0.2.0/24`
    
* Used for:
    
    * 2 Private EC2 Instances
        

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1771071580034/d378ecd9-39cd-4646-b895-94de06224a13.png align="center")

---

# ✅ STEP 3: Create and Attach Internet Gateway

To allow internet access:

1. Create Internet Gateway
    
2. Attach it to `Custom-Bastion-VPC`
    

This enables internet connectivity for public subnet resources.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1771072005191/6c3e2a56-052e-47f3-a8e0-a4d45da59a1f.png align="center")

---

# ✅ STEP 4: Create a NAT Gateway (For Private Internet Access)

Since private instances should not have public IPs, I created a NAT Gateway.

### Steps:

1. Allocate an Elastic IP
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1771072145231/bf64a5a2-3334-41fc-9791-1664cd556788.png align="center")
    
2. Create NAT Gateway
    
3. Place it inside the Public Subnet
    
4. Attach the Elastic IP
    

### Why?

This allows:

* Private instances → Outbound internet access
    
* Internet → Cannot directly access private instances
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1771072280437/eae86557-097b-4cf3-a0e7-5a0cc83e9ce0.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1771072534315/168236fd-af91-496f-a3ce-450f7a27a49b.png align="center")

---

# ✅ STEP 5: Configure Route Tables

## 🌍 Public Route Table

* Route: `0.0.0.0/0 → Internet Gateway`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1771073617783/a5e3086c-84d7-47cf-96a8-7b61555c7c7e.png align="center")
    
* Associate with Public Subnet
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1771073674608/42567f9c-44ec-4686-9178-a68e35d9e08e.png align="center")
    

## 🔐 Private Route Table

* Route: `0.0.0.0/0 → NAT Gateway`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1771073947469/21d2a61e-c7b6-4bf4-a1aa-d0edd0c3ab78.png align="center")
    
* Associate with Private Subnet
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1771074015201/24bc2230-f274-4ce1-acbe-791e70e1c56b.png align="center")
    

Now:

* Public subnet → Internet via IGW
    
* Private subnet → Internet via NAT
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1771074350790/007cac03-65f3-4fa8-bccf-b9dabc4ffdd6.png align="center")
    

---

# ✅ STEP 6: Launch the Bastion Host

Now I launched an Ubuntu EC2 instance in the Public Subnet.

### Configuration:

* AMI: Ubuntu Server
    
* Subnet: Public Subnet
    
* Auto-assign Public IP: Enabled
    
* Security Group:
    
    * Allow SSH (Port 22)
        
    * Source: My Public IP only
        

This ensures only I can SSH into the Bastion.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1771074827686/76c535a2-7673-4895-96b7-23cdfab248b4.png align="center")

---

# ✅ STEP 7: Launch Two Private EC2 Instances

Next, I launched 2 Ubuntu EC2 instances inside the Private Subnet.

### Configuration:

* Subnet: Private Subnet
    
* Auto-assign Public IP: Disabled
    
* Security Group:
    
    * Allow SSH (Port 22)
        
    * Source: Bastion Host Security Group
        
    * Allow HTTP (Port 80) from ALB Security Group
        

This ensures:

* Only Bastion can SSH into them
    
* Only Load Balancer can access port 80
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1771075543959/b831c19e-1e96-4c25-a968-f30c33bd0599.png align="center")

---

# ✅ STEP 8: SSH into Bastion and Access Private Servers

First, SSH into Bastion:

```plaintext
ssh -i key.pem ubuntu@<Bastion-Public-IP>
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1771075851502/c2ddfe74-0db3-41b4-a1b2-67b47a1bef7b.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1771075869394/fd0bc703-1f95-4d89-b67f-cc77e178bf38.png align="center")

Then SSH into private server from Bastion:

```plaintext
ssh -i key.pem ubuntu@10.0.2.10
```

This confirms secure internal-only access.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1771076256677/6c3add90-23ec-40ce-b906-82933a470eee.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1771076256664/834b946e-4529-4371-8976-abb05268cf8c.png align="center")

Second private instance

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1771076527447/4096ad28-e636-471b-926c-e16cb5ebe7a9.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1771076639418/2b10107d-cc07-41a3-92d3-3ca2019acecd.png align="center")

---

# ✅ STEP 9: Install Ansible on Bastion Host

Inside Bastion:

```plaintext
sudo apt update
sudo apt install ansible -y
```

Verify:

```plaintext
ansible --version
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1771077067409/597e3708-9145-450a-bc96-302044cbfe32.png align="center")

---

# ✅ STEP 10: Configure Ansible to Install Nginx

## Create Inventory File

```plaintext
nano inventory.ini
```

```plaintext
[webservers]
web1 ansible_host=10.0.2.199
web2 ansible_host=10.0.2.153

[all:vars]
ansible_user=ubuntu
ansible_ssh_private_key_file=/home/ubuntu/Server-key.pem
ansible_python_interpreter=/usr/bin/python3
```

---

## Create Playbook

```plaintext
nano install-nginx.yml
```

```plaintext
- name: Install and configure web servers
  hosts: webservers
  become: yes

  tasks:
    - name: Update apt cache
      apt:
        update_cache: yes

    - name: Install Nginx
      apt:
        name: nginx
        state: present

    - name: Start and enable Nginx
      service:
        name: nginx
        state: started
        enabled: yes
```

---

## Run Playbook

```plaintext
ansible-playbook -i inventory.ini install-nginx.yml
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1771077998222/990a691d-61d1-4e99-859c-397bc43496bf.png align="center")

---

# ✅ STEP 11: Modify Nginx Default Page

On each private server:

```plaintext
sudo nano /var/www/html/index.nginx-debian.html
```

Change content:

Server 1:

```plaintext
<!DOCTYPE html>
<html>
<head>
    <title>My Cloud Web Page</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background: #f4f6f8;
            text-align: center;
            padding: 50px;
        }
        .card {
            background: white;
            padding: 30px;
            border-radius: 10px;
            width: 60%;
            margin: auto;
            box-shadow: 0 0 15px rgba(0,0,0,0.1);
        }
        h1 { color: #2c3e50; }
        p { font-size: 18px; }
    </style>
</head>
<body>

<div class="card">
    <h1>Hello 👋 I'm NAME</h1>

    <p><strong>Instance Hostname:</strong> HOSTNAME</p>

    <p><strong>Private IP:</strong> HOST_IP</p>

    <h2>About Me</h2>
    <p>
        I am a Cloud Computing student and aspiring DevOps Engineer.
        I enjoy building secure AWS infrastructure, automating deployments,
        and learning modern cloud technologies.
    </p>
</div>

</body>
</html>
```

Server 2:

```plaintext
This is Private Server 2
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1771079702891/51b35da4-8098-40fa-84a9-60411e71e943.png align="center")

---

# ✅ STEP 12: Create Target Group

Now I configured a Target Group:

* Target type: Instances
    
* Protocol: HTTP
    
* Port: 80
    
* Registered both private instances
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1771080957626/2996e074-603d-40de-a942-a0973033a996.png align="center")
    

---

# ✅ STEP 13: Create Application Load Balancer

Configuration:

* Type: Application Load Balancer
    
* Scheme: Internet-facing
    
* Subnets: Public Subnet
    
* Security Group:
    
    * Allow HTTP (Port 80)
        

Attach:

* Previously created Target Group
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1771081687650/a36dc992-503e-4501-8b3c-81fc7df76140.png align="center")

---

# ✅ STEP 14: Access the Application

Copy the ALB DNS name:

```plaintext
http://<ALB-DNS-Name>
```

Result:

* Traffic distributed between both servers
    
* No public IP exposed on private instances
    
* Fully secure architecture
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1771088378271/90b257f5-e590-4044-8df1-b9832fc35fc3.png align="center")
    

---

### 🔐 Why I Used a Bastion Host

The Bastion Host acts as a secure jump server into the private network.

Instead of exposing my private EC2 instances directly to the internet, I:

* Placed them in a private subnet
    
* Disabled public IP assignment
    
* Allowed SSH access only from the Bastion Host
    

The Bastion Host:

* Allows SSH only from my personal IP
    
* Acts as the single controlled entry point
    
* Reduces attack surface
    

This follows the principle of least privilege and improves overall security posture.

---

### 🤖 How Ansible Simplified Deployment

To avoid manually configuring each server, I used Ansible for automation.

Using:

* An inventory file
    
* A playbook
    
* A single execution command
    

I was able to install and configure Nginx on both private servers simultaneously.

Benefits:

* Consistency across servers
    
* Reduced human error
    
* Faster deployment
    
* Easy scalability
    

This demonstrates infrastructure automation, a core DevOps principle.

---

### 🌍 Direct EC2 Access vs Load Balancer Access

There are two ways users can access applications:

#### 🔴 Direct EC2 Access

Users connect directly to a server’s public IP.

Disadvantages:

* Single point of failure
    
* No traffic distribution
    
* Reduced scalability
    
* Increased security risk
    

#### 🟢 Load Balancer Access

Users connect through a single DNS endpoint provided by the Application Load Balancer.

Advantages:

* High availability
    
* Automatic traffic distribution
    
* Fault tolerance
    
* Backend servers remain private
    

Using a Load Balancer makes the architecture production-ready and scalable.

# 🔐 Security Achieved

✔ Private instances have no public IP  
✔ SSH only through Bastion  
✔ Bastion restricted to my IP  
✔ Internet access via NAT only  
✔ Load Balancer securely exposes app  
✔ Infrastructure automated using Ansible

---

# 🏁 Conclusion

In this project, I successfully built a **secure, scalable, and production-style AWS infrastructure** using:

* VPC segmentation
    
* Bastion Host access control
    
* NAT Gateway for private internet access
    
* Ansible automation
    
* Application Load Balancer for high availability
    

This architecture mirrors what is used in real-world enterprise cloud environments and demonstrates strong understanding of **networking, security, and DevOps automation**.