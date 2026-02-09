---
title: "How to Create a Windows Operating System Virtual Machine in Microsoft Azure"
datePublished: Sat Nov 02 2024 10:05:54 GMT+0000 (Coordinated Universal Time)
cuid: cm2zzzxvc000609l20uihdxub
slug: how-to-create-a-windows-operating-system-virtual-machine-in-microsoft-azure
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1730393068124/55bb8be3-f1e3-409e-ba89-f5e4a6d35267.jpeg

---

## Introduction

Creating a virtual machine (VM) in Microsoft Azure is a key skill for anyone looking to leverage cloud computing, whether for personal projects, application development, or enterprise solutions. Azure virtual machines offer flexibility, scalability, and access to a variety of resources, making them ideal for running everything from simple applications to complex infrastructure setups. In this guide, we’ll walk through the steps to create a virtual machine in Azure, from setting up essential configurations to accessing your VM. By the end, you’ll have a functional virtual machine ready for development, testing, or deployment. Let’s get started!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1730309419751/7c3e539e-1dcc-4f9b-a28a-7b34bc289c4f.jpeg align="center")

### Step 1: Log into the Azure Portal

* [**Descript**](https://portal.azure.com)**ion**: Begin by logging int[o your Azure](https://portal.azure.com) account via the [Azure Portal](https://portal.azure.com)
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1730390369921/5d22a2a4-3f64-4474-b785-2077027237d9.png align="center")

### Step 2: Access the “Create a Resource” Option

* **Description**: Once logged in, you’ll be on the Azure dashboard. On the left-hand side menu, click on **Create a resource**. This opens a new window where you can choose from a list of resources.
    
* ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1730390388847/3c85f637-5c20-41fd-a665-d9063ba7aa6e.png align="center")
    

### Step 3: Search and Select “Virtual Machine”

* **Description**: In the “Create a resource” window, use the search bar at the top to type **Virtual Machine**. Select **Virtual Machine** from the options that appear.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1730390409274/18c0eb04-307e-41bb-9a36-8c5595a7ed09.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1730390470794/8652c645-c4c3-4ac8-b5a1-7a46df97958e.png align="center")

### Step 4: Configure the Basics of Your Virtual Machine

* **Description**: The first tab you’ll see is the **Basics** tab. Here, you’ll enter essential details for your VM:
    
    * **Subscription**: Choose the subscription you’re using.
        
    * **Resource Group**: Select an existing resource group or create a new one.
        
    * ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1730390602164/a791757a-2cd0-4203-95fa-9e5e09fc82bf.png align="center")
        
    * **Virtual Machine Name**: Enter a name for your VM, like "MyFirstVM."
        
    * **Region**: Select the Azure region where your VM will be hosted.
        
    * **Availability Options**: Choose **Availability zone** or **Availability set** if you need redundancy.
        
    * ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1730390585175/8eef0c47-0a03-4921-8f00-8d20d05cd5ad.png align="center")
        

### Step 5: Choose the Virtual Machine Image and Size

* **Description**: Scroll down to select the **Image** (operating system) for your VM, such as **Windows Server 2019** or **Ubuntu Server 20.04 LTS**. Then, choose the **Size** based on your CPU and memory requirements.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1730390634910/bdad7a3d-986c-490c-a1eb-8848d7ff4d44.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1730391003151/8110de25-c607-4fe2-957b-daf9148b04ef.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1730391025870/d1a4ba33-9424-4cf2-bc08-d8daf2142e9e.png align="center")

### Step 6: Configure Administrator Account

* **Description**: In the same **Basics** tab, set up the admin account details to manage your VM:
    
    * **Authentication Type**: Choose between **Password** or **SSH Public Key**.
        
    * **Username** and **Password/SSH Key**: Provide a username and either a password or SSH key.
        
    * ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1730391050563/03ceb439-e677-4056-b0bf-204070736d68.png align="center")
        

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1730391072024/421dcb28-1236-449b-9433-3dfff0d91455.png align="center")

### Step 7: Configure Disk Options

* **Description**: In the **Disks** tab, select the OS disk type (Standard SSD, Premium SSD, or HDD) based on performance and cost needs. You can also add data disks if required
    
* ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1730391124664/cada0dbc-06a1-488d-8c50-ce0cdebf712e.png align="center")
    

### Step 8: Set Up Networking

* **Description**: Switch to the **Networking** tab to configure network settings for the VM, including the **Virtual Network (VNet)**, **Subnet**, and **Public IP**. You can accept the defaults or customize these settings.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1730391185207/65cc0327-2d8c-4481-ba94-ddb12498b077.png align="center")

### Step 9: Set Up Monitoring (Optional)

* **Description**: On the **Monitoring** tab, you can enable monitoring options such as **Boot diagnostics**, **Guest OS diagnostics**, and **Auto-shutdown** if needed.Step 10: Review and Create the Virtual Machine
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1730541662990/01c32861-a614-4853-bb30-77d076aee8d9.png align="center")

### Step 10: Review and Create the Virtual Machine

* **Description**: After completing all necessary tabs, go to the **Review + Create** tab. Azure will validate the settings, and if everything is correct, you’ll see a green checkmark. Click **Create** to start the VM deployment.
    
* ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1730391279562/112786ee-798f-46a4-a663-b1e5022f8f0c.png align="center")
    

### Step 11: Access and Manage Your Virtual Machine

* **Description**: Once the VM is created, go to your **Virtual Machines** page, select your VM, and use the **Connect** button to log in via RDP (for Windows) or SSH (for Linux).
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1730391359674/4ffba6ea-162e-4b0f-8fed-3dbb566ef80b.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1730391403234/1c956c89-9e4f-44dd-bf55-f1a48e43f6e4.png align="center")

### Step 12: Connect to Your Windows VM

* **Description**: Once deployment is complete, go to the **Virtual Machines** section in your Azure portal. Select your VM and click **Connect**. Follow the instructions for connecting via **Remote Desktop Protocol (RDP)**, using the username and password you set up in Step 6.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1730391576575/760c7946-baec-447b-8ac8-7569ab3a141d.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1730391644265/5f7db235-60ac-4c02-8b18-25d5b0534671.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1730391679380/c6028255-4037-4430-a9e9-e78c2d0ac399.png align="center")

### Step 13 : Double click on the RDP File to Launch VM

**Description**: Double-click on the downloaded RDP file to initiate a remote desktop session with your virtual machine. This action will open the Remote Desktop Protocol (RDP) client, allowing you to securely connect and manage your VM directly from your local device.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1730392656189/d08a1394-daad-4c3a-acbc-35c2b4063b90.png align="center")

### Conclusion

Creating a virtual machine in Microsoft Azure is a simple yet powerful way to get started with cloud computing. Whether you’re testing an app, running isolated development environments, or hosting scalable services, Azure VMs offer the flexibility and power you need.