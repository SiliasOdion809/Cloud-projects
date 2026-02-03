---
title: "How I Created an Amazon S3 Bucket, Uploaded an Image, and Made It Publicly Accessible"
datePublished: Tue Feb 03 2026 12:10:06 GMT+0000 (Coordinated Universal Time)
cuid: cml6k3ta6000c02l27avz9f0z
slug: how-i-created-an-amazon-s3-bucket-uploaded-an-image-and-made-it-publicly-accessible
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1770119606506/c503e9bd-8610-47a6-9ff0-c43237ad0dbb.png
tags: aws, cloud-computing, s3

---

---

## Introduction

Amazon Simple Storage Service (Amazon S3) is one of the most popular services provided by Amazon Web Services (AWS). It allows users to store and retrieve files (objects) securely and at any time from anywhere on the internet.

In this blog, I will walk through the steps I followed to:

* Create an S3 bucket on AWS
    
* Upload an image into the bucket
    
* Configure the bucket to allow public access to the image
    

This project helped me understand how cloud storage works and how permissions are managed in AWS.

---

## What is Amazon S3?

Amazon S3 (Simple Storage Service) is an object storage service that offers scalability, security, and high availability. It is commonly used for:

* Storing images and videos
    
* Hosting static websites
    
* Backups and data archiving
    

Each file stored in S3 is called an **object**, and objects are stored inside containers called **buckets**.

---

## Step 1: Logging into the AWS Management Console

To begin, I logged into my AWS account using the AWS Management Console.

**Steps:**

1. Opened my browser and visited [`https://aws.amazon.com`](https://aws.amazon.com)
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770114058939/cca89ed8-f3df-4b8d-a6fc-c414f42775ac.png align="center")
    
2. Signed in using my AWS credentials
    
3. From the AWS Management Console, searched for **S3** and selected it
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770114721647/323b6ee0-9472-4c4c-9bd1-7a76fe29f077.png align="center")

---

## Step 2: Creating an S3 Bucket

After opening the S3 dashboard, I created a new bucket.

**Steps:**

1. Clicked on **Create bucket**
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770114873945/cfc7003e-e146-4920-9f55-e8871b19a64c.png align="center")
    
2. Entered a unique bucket name
    
3. Selected a preferred AWS region
    
4. Left other settings as default
    
5. Clicked **Create bucket**
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770115195446/9e0a982e-42da-480b-ae81-2bd03209f63e.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770115198015/195920e0-f689-48b1-9782-0e9da25e2aa8.png align="center")

---

## Step 3: Uploading an Image to the Bucket

Once the bucket was successfully created, I uploaded an image file into it.

**Steps:**

1. Opened the newly created bucket
    
2. Clicked **Upload**
    
3. Selected an image file from my local system
    
4. Clicked **Upload** to complete the process
    

After uploading, the image appeared inside the bucket as an object.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770115606171/7227fb25-04df-4ac2-a74c-571c01ac81cf.png align="center")

---

## Step 4: Disabling Block Public Access

By default, S3 buckets block public access for security reasons. To make my image publicly accessible, I adjusted the bucket’s public access settings.

**Steps:**

1. Opened the bucket
    
    1. Navigated to the **Permissions** tab
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770115917344/5e57c5fc-b609-4b07-8957-f6fb12743dd5.png align="center")
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770115990339/8a6d6b3e-7980-4d72-869a-70e51747a248.png align="center")
        
2. Clicked **Edit** under *Block public access*
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770116160416/66917d79-89b0-4cad-88d1-c3d8c9ee8e39.png align="center")
    
3. Unchecked **Block all public access**
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770116269253/02c8229c-867c-40b9-af23-493aff51c544.png align="center")
    
4. Saved the changes and confirmed
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770116355296/eca6a558-7019-4d45-a89e-72a8a77d3608.png align="center")
    

---

## Step 5: Making the Image Public Using Bucket Policy

To allow public access to the image, I applied a bucket policy.

**Steps:**

1. Went to the **Permissions** tab
    
2. Selected **Bucket policy**
    
3. Added a policy that allows public read access to objects
    
4. Saved the policy
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770119180985/f247745f-877e-4a51-bd5e-8fd36bc76233.png align="center")
    

This policy allows anyone on the internet to view the image.

---

## Step 6: Accessing the Image Publicly

After configuring the permissions, I copied the **Object URL** of the image and opened it in a browser.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770119279197/e014e3ce-5a82-4545-899d-27fd709ef7dc.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1770119378351/8775320a-d363-484d-b4a8-981d132453bb.png align="center")

The image loaded successfully, confirming that it was publicly accessible.

---

## Conclusion

Through this project, I learned how to:

* Create and manage an S3 bucket
    
* Upload objects to cloud storage
    
* Configure permissions to allow public access
    

This exercise gave me practical experience with AWS S3 and helped me understand how cloud storage and access control work in real-world scenarios. Amazon S3 is a powerful service, and mastering it is an important step in becoming a cloud engineer.