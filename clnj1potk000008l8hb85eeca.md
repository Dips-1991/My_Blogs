---
title: "Day-38 Task: Getting Started with AWS Basics☁"
datePublished: Mon Oct 09 2023 15:26:15 GMT+0000 (Coordinated Universal Time)
cuid: clnj1potk000008l8hb85eeca
slug: day-38-task-getting-started-with-aws-basics
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1696865110007/ce55ebc8-01c1-4916-b28c-a838675eb9d4.gif
tags: aws, cloud-computing, iammfaaccess-key-idsecret-access-key, tws

---

### 📖 **Introduction**

Well, till now we have discussed about `Git, Linux, Shell Scripting, Docker, Jenkins, and Kubernetes`. It’s time to move to the cloud. Let’s get started with AWS!

### ☁ **Cloud Computing**

Cloud computing is the on-demand availability of computer system resources, especially data storage and computing power, without direct active management by the user. Large clouds often have functions distributed over multiple locations, each of which is a data center.

### **🌐 What is AWS?**

* **Definition**: AWS, or Amazon Web Services, is a comprehensive cloud computing platform provided by Amazon.
    
* **Purpose**: It offers a bunch of services, allowing businesses to host applications, store data, and innovate without the burden of physical infrastructure.
    

### 🏗️ **AWS Global Infrastructure**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696774147137/6655b616-f88a-4baf-b33b-3bcdb9a8772e.png align="center")

* At the moment of writing this blog, The AWS Cloud spans 99 Availability Zones within 31 geographic regions around the world, with announced plans for 15 more Availability Zones and 5 more AWS Regions in Canada, Israel, Malaysia, New Zealand, and Thailand.
    
* Amazon Web Services (AWS) has a global network of 450+ Points of Presence (PoPs), 400+ Edge Locations, and 13 Regional Edge Caches. These PoPs, Edge Locations, and Edge Caches are used to deliver content to end users with lower latency.
    

### 🌎 **What are Regions?**

* A region is a geographical area.
    
* Each region consists of 3 or more availability zones.
    
* Each Amazon Region is designed to be completely isolated from the other Amazon Regions.
    
* Each AWS Region has multiple Availability Zones and data centers.
    

### 🗺️ **What are Availability Zones?**

* Availability Zones are physically separate and isolated from each other.
    
* AZs span one or more data centers and have direct, low-latency, high throughput, and redundant network connections between each other.
    
* Each AZ is designed as an independent failure zone.
    
* An Availability Zone is represented by a region code followed by a letter identifier; for example, `us-east-1a` for the `US East (N. Virginia)` region.
    

### 🌌 **What are Local Zones?**

* AWS Local Zones place compute, storage, database, and other select AWS services closer to end-users.
    
* With AWS Local Zones, you can easily run highly demanding applications that require single-digit millisecond latencies to your end-users.
    
* Each AWS Local Zone location is an extension of an AWS Region where you can run your latency-sensitive applications using AWS services such as Amazon Elastic Compute Cloud, Amazon Virtual Private Cloud, Amazon Elastic Block Store, Amazon File Storage, and Amazon Elastic Load Balancing in geographic proximity to end-users.
    

### 🚉 **Edge Locations and Regional Edge Caches**

* Edge locations are Content Delivery Network (CDN) endpoints for CloudFront.
    
* Currently, there are over 200 edge locations.
    
* Regional Edge Caches sit between your CloudFront Origin servers and the Edge Locations.
    
* A Regional Edge Cache has a larger cache width than each of the individual Edge Locations.
    

### **🛠️ AWS Services: Tools of Transformation**

Let’s dive into the AWS services, each designed to cater to specific needs.

* #### **Compute Services 🖥️**
    
    * **EC2 (Elastic Compute Cloud)**: Provides resizable compute capacity in the cloud, serving as virtual servers for various applications.
        
    * **Lambda**: A serverless compute service, allowing you to run code without provisioning or managing servers
        
    
* #### **Storage Services 🗄️**
    
    * **S3 (Simple Storage Service)**: Scalable object storage, perfect for storing and retrieving any amount of data.
        
    * **EBS (Elastic Block Store)**: Offers high-performance block storage for use with EC2 instances, ideal for databases and applications.
        
    
* #### **Database Services 🎲**
    
    * **RDS (Relational Database Service)**: Managed database service supporting multiple database engines like MySQL, PostgreSQL, and SQL Server.
        
    * **DynamoDB**: A fast and flexible NoSQL database service for applications requiring seamless and quick scalability.
        
    
* #### **Networking Services 🌐**
    
    * **VPC (Virtual Private Cloud)**: A logically isolated section of AWS where you can launch resources in a virtual network.
        
    * **Route 53**: A scalable domain name system (DNS) web service, ensuring seamless and secure routing to end-users.
        
    
* #### **Developer Tools 🛠️**
    
    * **CodeCommit**: Fully managed source control service, ensuring secure and scalable code collaboration.
        
    * **CodePipeline**: Continuous integration and continuous delivery service, automating the software release process for fast and reliable updates.
        
    
* #### **Security and Identity Services 🔐**
    
    * **IAM (Identity and Access Management)**: A robust service for managing user permissions and ensuring secure access control to AWS resources.
        
    * **Cognito**: Identity management service enabling you to add authentication, authorization, and user management to your applications.
        
    

### 🔐**IAM (Identity and Access Management)**

* AWS Identity and Access Management (IAM) is a web service that helps you securely control access to AWS resources.
    
* With IAM, you can centrally manage permissions that control which AWS resources users can access.
    
* You use IAM to control who is authenticated (signed in) and authorized (has permissions) to use resources.
    

### ✍️ Task1:

**Create an IAM user with the username of your own wish and grant EC2 Access. Launch your Linux instance through the IAM user that you created now and install Jenkins and Docker on your machine via a single Shell Script.**

1. **Go To the IAM Dashboard:**
    
    * Search for IAM in the search bar. The IAM dashboard like the below one appears:
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696831704832/d70d2766-9bed-449b-8ee7-30352eb11689.png align="left")
        
2. **Create User:**
    
    * Now go to `Users` In the left corner click on `Create user`.
        
    * Provide the username of the user and Select the required information as shown.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696832078957/595ad1ea-1a16-4098-89cf-dc2e29d7a282.png align="center")
        
    * In `Console password` select the required field as shown below and create your custom password.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696832244072/9cae650b-3ddc-4f2f-8579-66c6219868bb.png align="center")
        
3. **Set the Permissions:**
    
    * Select “`Attach policies directly`” in the Permission Options.
        
    * In the Permission Policies search bar, search for EC2 and select `“AmazonEC2FullAccess”`. And Click on `Next`.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696832468560/f934375c-7d70-4726-9704-151a59392285.png align="center")
        
    * Next, Review the information and click on `Create`.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696832653243/97317f63-bb37-4868-84f3-c49f1892419e.png align="center")
        
4. **Retrieve the password:**
    
    * You can view and download the user’s password below or email the user’s instructions for signing in to the AWS Management Console. This is the only time you can view and download this password.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696832765830/3ff669ed-3b22-4e51-9be5-7675840f12c3.png align="center")
        
    * Make it a point to download the .csv file, if you are not accessing the AWS through an IAM user immediately.
        
    * Click on Return to User’s list. and you can see the user is created.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696832900421/23ae3950-f5ef-4797-9898-7707a2816146.png align="center")
        
5. **Log in to AWS as an IAM user:**
    
    * Sign out and go to the sign-in page of the AWS Management Console.
        
    * Select `IAM user` and Provide the `12 digit Account ID`. and Click on `Next`.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696833272922/2155ec86-951e-4a54-82d4-14e1a917fbc3.png align="center")
        
    * Now sign in as an IAM user using the `username` and `password` that you have created. And Click on `Sign in`.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696833415342/24a10e3a-e484-46fd-ad59-6cf83673a791.png align="center")
        
    * Now, You will be asked to reset the password. Go ahead and change the password using the details you have. Click on `Confirm password change`.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696833539615/b2f57870-d873-496a-98d9-b16d9f80ec13.png align="center")
        
6. **Launch EC2 Instance:**
    
    * Once you logged in as an IAM user go to the `EC2 section` create the EC2 instance and `connect to the EC2 instance`.
        
    * ***Note that you can’t connect to the instance using “***`EC2 Instance Connect”`***as you have not given the user access to ec2:InstanceConnect. So log in using SSH.***
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696833897093/5090dd2a-cb3d-4891-9461-7bd3891512dd.png align="center")
        
7. **Install Docker & Jenkins:**
    
    * Let’s install docker and Jenkins in this instance using a shell script.
        
    * Here is the shell script file for installing `Docker and Jenkins`.
        
        ```abap
        #!/bin/bash
        sudo apt update
        sudo apt install openjdk-11-jre -y
        curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
          /usr/share/keyrings/jenkins-keyring.asc > /dev/null
        echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
          https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
          /etc/apt/sources.list.d/jenkins.list > /dev/null
        sudo apt-get update
        sudo apt-get install jenkins -y
        sudo systemctl enable jenkins
        sudo systemctl start jenkins
        sudo apt-get update
        sudo apt-get install docker.io -y
        sudo systemctl start docker
        ```
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696834678583/bf8d3a53-56e2-4a59-81f4-4601e38085ca.png align="center")
        
    * Now, Execute the Shell Script file
        
    * Before that assign `executable permission` it to the shell script file otherwise, it will throw the permission denied error.
        
    * To provide the executable permission use below the command.
        
        ```apache
        chmod +x <file-name>
        ```
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696834980781/6a737d49-69f6-4d48-b9fb-2ecc310e6e7e.png align="center")
        
    * Once you execute the shell script file it will download and install the Docker and Jenkins for you with a single click.
        
8. **Verify if Jenkins and Docker Installation:**
    
    * To verify whether Docker and Jenkins are installed successfully or not use the command.
        
        ```apache
        sudo systemctl status jenkins
        sudo systemctl status docker
        ```
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696835314233/c5ea1cbe-3225-4faf-acc7-25675a79171f.png align="center")
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696835336204/bf9cba5c-b1ae-417d-bb1c-5948194115ae.png align="center")
        
    * The status of both `Docker` and`Jenkins` is `Active(Running),` which means the installation was successful.
        
    * Allow the `port 8080` in your `EC2 instance security group`.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696835582253/2b46e744-b94b-4b0f-805f-38af784e1ac8.png align="center")
        
    * Now go to your browser, open `<EC2-PublicIP:8080>` and you must be able to see the `Unlock Jenkins` page.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696835680690/d398c8f0-b72d-43af-ac92-7d95601726de.png align="center")
        

### ✍️ Task2:

**In this task, you need to prepare a DevOps team of avengers. Create 3 IAM users of Avengers and assign them to devops groups with IAM policy**

1. **Login as Root User:**
    
    * Log in to AWS Management Console as a root user.
        
2. **Create 3 Users:**
    
    * In `Task-1` we have learned about IAM user creation.
        
    * Create the 3 users with the name "`IronMan`", "`SpiderMan`", "`Thor`".
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696862580246/697da1a3-bae6-41c5-9bcb-e89830ea756d.png align="center")
        
3. **Create User Group:**
    
    * Go to `IAM` &gt; `User Groups` &gt; `Create Group` &gt; User Group Name `“Avengers”`.
        
    * Add created 3 users to the group.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696862979742/98bc6904-30f5-49e4-af77-842d05be415c.png align="center")
        
    * Attach permissions policies &gt; Give this user group access to `S3 Full Access` and `EC2 Full Access` &gt; Click on Create User Group.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696863165769/0f5adc70-72df-4b2a-98b3-9c42316b7ace.png align="center")
        
4. **Check the User Permissions:**
    
    * Now goto `users` click on any one of the user and see the permissions in `Permission` the section.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696863369897/f8df484b-02a1-4d21-9d5e-dc21ba90d947.png align="center")
        
    * What we have achieved here, I had not given any `permissions` to these `users` while creating them. After adding them to the `User Group`, they have got the permissions attached to the policy of the `Avengers` group.
        

### 📝**Summary**

* In this blog, we have learned about **AWS**, **Regions**, **Availability Zones, Local Zones, Edge Locations, and Regional Edge Caches, Some of the overviews of AWS services, AWS Identity and Access Management (IAM).**
    
* We have also performed some hands-on on **IAM user creation** and **installing applications using Shell script.**
    
* We have learned about **User Groups**, **Adding users to the group assigning permissions to the group, and how automatically those permissions are assigned to the added users.**
    

---

> **Thank you🙏🙏... for taking the time to read this blog. I hope you found the information helpful and insightful. So please keep yourself updated with my latest insights and articles on DevOps 🚀 by following me on**
> 
> So, Stay in the loop and stay ahead in the world of DevOps!
> 
> ***Happy Learning !... Keep Learning ! 😊***