---
title: "Day 40  ☁AWS EC2 Automation⚙🚀"
datePublished: Fri Oct 13 2023 19:46:06 GMT+0000 (Coordinated Universal Time)
cuid: clnp0r9i1000309mngydu60vk
slug: day-40-aws-ec2-automation
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1697226151449/83d00219-9d1b-4a53-8e2b-2e24126a014b.jpeg
tags: aws, ec2-instance-types, tws, aws-automation, launchtemplate

---

### ✨**Introduction**

In the previous blog, we learned about User Data and IAM. Let’s learn about Automation in AWS. How to automate EC2 using Launch Templates and Auto Scaling Groups.

### ⚙ **Automation in EC2:**

Amazon EC2 or Amazon Elastic Compute Cloud can give you secure, reliable, high-performance, and cost-effective computing infrastructure to meet demanding business needs.

### 📃 **Launch template in AWS EC2:**

* You can make a launch template with the configuration information you need to start an instance. You can save launch parameters in launch templates so you don't have to type them in every time you start a new instance.
    
* For example, a launch template can have the AMI ID, instance type, and network settings that you usually use to launch instances.
    
* You can tell the Amazon EC2 console to use a certain launch template when you start an instance.
    
* Amazon EC2 Launch Templates are a powerful feature within Amazon Web Services, designed to simplify and standardize the process of launching EC2 instances.
    
* They provide a convenient way to automate the configuration of instances, making it easier to maintain consistency and enhance efficiency across your infrastructure.
    
* A Launch Template is a configuration blueprint that contains settings for launching EC2 instances, such as the AMI, instance type, security groups, and storage configurations.
    

### ✅ **Advantages of Launch Templates**

* **Consistency**: Ensures consistent configurations across instances, reducing the risk of misconfigurations and errors.
    
* **Simplifies Management**: Simplifies the process of launching instances by encapsulating all necessary configurations in a single template.
    
* **Versioning**: Supports versioning, allowing you to manage different iterations of launch configurations over time.
    
* **Flexibility**: Enables parameterization, allowing you to customize specific attributes when launching instances based on the template.
    
* **Integration with Auto Scaling**: Launch Templates seamlessly integrate with Auto Scaling groups, ensuring newly launched instances adhere to defined configurations.
    

### ✏️ **Instance Types**

When you launch an instance, the *instance type* that you specify determines the hardware of the host computer used for your instance.

Instance types are named based on their `family`, `generation`, `additional capabilities`, and `size`.

* The first position of the instance type name indicates the instance family, for example `t`.
    
* The second position indicates the instance generation, for example `2`.
    
* The remaining letters before the period indicate additional capabilities, such as instance store volumes.
    
* After the period (`.`) is the instance size, which is either a number followed by size, such as `nano`,`micro`,`9xlarge`, or `metal` for bare metal instances.
    

### ✍ **AWS Instance Type**

Here are some instance types provided by AWS

1. **<mark>General purpose instances</mark>**
    
    * General purpose instances provide a balance of compute, memory, and networking resources, and can be used for a wide range of workloads.
        
    * These instances are ideally suited for scale-out workloads that are supported by the Arm ecosystem. These instances are well-suited for the `Web servers`, `Containerized microservices`.
        
    * Examples: `t3, m5`
        
2. **<mark>Compute-optimized instances</mark>**
    
    * Compute-optimized instances are ideal for compute-bound applications that benefit from high-performance processors.
        
    * These instances are well suited for the `Batch processing workloads`, `Media transcoding`, `High-performance web servers`, `High-performance computing (HPC)`, `Scientific modeling`, `Dedicated gaming servers and ad serving engines`, `Machine learning inference` and other `compute-intensive applications`.
        
    * Examples: `c5`
        
3. **<mark>Memory optimized instances</mark>**
    
    * Memory optimized instances are designed to deliver fast performance for workloads that process large data sets in memory.
        
    * These instances are well suited for the `High-performance, including relational MySQL and NoSQL, for example MongoDB and Cassandra databases`, `Applications performing real-time processing of big unstructured data, using Hadoop and Spark clusters`.
        
    * Examples: `r5`
        
4. **<mark>Storage optimized instances</mark>**
    
    * Storage optimized instances are designed for workloads that require high, sequential read and write access to very large data sets on local storage.
        
    * They are optimized to deliver tens of thousands of low-latency, random I/O operations per second (IOPS) to applications.
        
    * These instances are well suited for the `Massive parallel processing (MPP) data warehouse`, `MapReduce and Hadoop distributed computing`, `Log or data processing applications`.
        
    * Examples: `i3, d2.`
        
5. **<mark>GPU Instances</mark>**
    
    * GPU instances are equipped with powerful graphics processing units (GPUs) that accelerate applications requiring parallel processing and high-performance computing.
        
    * They are used for machine learning, deep learning, video rendering, and other GPU-intensive workloads.
        
    * Examples: `p3, g4.`
        

### 🙎🏻 **AMI(Amazon Machin Image)**

* An Amazon Machine Image (AMI) is an image that AWS supports and keeps up to date.
    
* It contains the information needed to start an instance. When you launch an instance, you must choose an AMI.
    
* When you need multiple instances with the same configuration, you can launch them from a single AMI.
    
* AMIs are available as Amazon-provided AMIs, AWS Marketplace AMIs, and Custom AMIs.
    
* An AMI includes Root Volume, Instance Configuration, Permissions, Block Device Mappings, and Launch Permissions.
    

### 👨🏼‍💻 **Task: 1**

* Create a launch template with `Amazon Linux 2 AMI` and `t2.micro` instance type with `Jenkins and Docker` setup (You can use the [Day-39 Part-1:☁Amazon EC2 User-Data🤵🏻📑](https://hashnode.com/edit/clnncsrt8000009l99qmk8n4a) )User data script for installing the required tools.
    
* Create 3 Instances using Launch Template, there must be an option that shows the number of instances to be launched, can you find it? :)
    

1. **<mark>Create Launch Template:</mark>**
    
    Go to `AWS management console` &gt; `go to Instance Service` &gt; Under Instance &gt; `Click on Launch Templete` &gt; `Click on Create launch template`.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697214075470/58feb637-2651-4352-8dd5-8b3a5614add5.png align="center")
    
    In the `Launch template name and description` Provide the information as per your need.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697214320557/fedeb152-9813-4c8d-a430-227e712278fd.png align="center")
    
    In the `Application and OS Images (Amazon Machine Image)` select the image that you want.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697214485312/659e967a-2b3e-4800-adc9-368d23444ac3.png align="center")
    
    In the `Instance type` select its free tier eligible but you can select as your need
    
    In the `Key pair (login)` existing if exists or you can create a new key.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697214596857/fe38414d-db1c-487e-9f82-0bb9d4655c41.png align="center")
    
    In the `Network settings` you can select a subnet and security group if exist or you can create a new SG.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697214787005/0cfe350f-1ef8-42f0-a590-bd0df7430e3f.png align="center")
    
    You can provide other information which needed
    
    Now under `Advance Details` at the bottom, there is a `User data section` add the `user data script` there, And `Click on Launch templete`.
    
    ```abap
    #!/bin/bash
    sudo apt-get update -y
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
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697215199287/f3f712d4-32d4-4e4e-9a7e-6946be15a52b.png align="center")
    
    You can see the Launch Template is created.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697215257604/32a10400-be45-4096-a012-5605820a17e6.png align="center")
    
2. **<mark>Create Instance using Launch Template:</mark>**
    
    Since we need 3 instances from the template we created, `select the Launch template` &gt; `go to Action` &gt; `Select Launch instance from launch template`.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697215868411/50e754cb-792b-4362-8c5d-7a65f755e6a4.png align="center")
    
    On the left side, you can see all the instance required information is available as a configuration which we have configured in the launch template.
    
    Now, on the right side in `Summary` &gt; provide the `Number of Instances` &gt; `Click on Launch instance`. It will create 3 Instances using the Launch Template.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697216167935/0ae483ed-ccc9-4250-bd56-d426a9019ff9.png align="center")
    
    Once you click on 3 instances are created using `Launch Template configuration`.
    
3. **<mark>Verify all the instance runs the Jenkins:</mark>**
    
    Copy all 3 instances public `IP address` one by one and paste them into the browser followed by port 8080 like `<IP-address>:8080`.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697216934135/fa0cbb09-8ca0-4cdd-9403-b0e550487160.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697216954817/370f24fc-b4cb-47bb-b448-bc6019419ada.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697216984104/b69c936f-1fcd-4767-9903-f52b33fbd0b0.png align="center")
    

### 🔢 **Auto Scaling Group(ASG)**

* In cloud computing, `flexibility` and `scalability` are paramount. AWS Auto Scaling Groups emerge as the magical wands, ensuring your applications gracefully handle varying workloads.
    
* `Auto Scaling Groups (ASG)` contains a collection of EC2 instances that are treated as a group for the purpose of automatic scaling and management.
    
* `Scaling out` is when we `add the server`, `scaling in` is when we `remove a server`, and `scaling up` is when we `increase the size of an instance`.
    

### **🤔 Why We Use AWS Auto Scaling Groups? 🌪️**

* **Dynamic Workloads**: Applications experience fluctuating traffic. Auto Scaling Groups adapt to changing demands, ensuring you always have the right number of instances.
    
* **High Availability**: Enhances fault tolerance by distributing instances across multiple Availability Zones (AZs), guaranteeing continuity even during failures.
    
* **Cost Efficiency**: Scales up during peak periods and down during lulls, optimizing costs by utilizing resources only when needed.
    
* **Automated Management**: Automates the provisioning and termination of instances based on user-defined policies, eliminating manual intervention.
    
* **Improved Performance**: Maintains performance levels by distributing traffic evenly among instances, preventing overloads.
    

### **🎯 Features of AWS Auto Scaling Groups**

* **Scaling Policies**: Define policies to automatically add or remove instances based on metrics like CPU utilization, network traffic, or custom application metrics.
    
* **Health Checks**: Auto Scaling Groups monitor instance health and replace unhealthy instances, ensuring robustness and availability.
    
* **Lifecycle Hooks**: Allows you to perform custom actions when instances launch or terminate, enabling tailored setup procedures.
    
* **Integration with Load Balancers**: Seamlessly integrates with Elastic Load Balancers, enabling balanced distribution of incoming traffic across instances.
    
* **Scheduled Scaling**: Schedule changes to Auto Scaling Group capacity, allowing predictable scaling for planned events or recurring schedules.
    

### **🛒 Use case of ASG:- E-Commerce Website Scaling 🛒**

Imagine you run an e-commerce website. Here's how Auto Scaling Groups come to your aid:

* **Morning Rush**: As customers flock to your website in the morning, Auto Scaling detects the increased traffic and automatically launches additional instances to handle the load.
    
* **Flash Sale**: During a flash sale event, traffic spikes dramatically. Auto Scaling ensures your website stays responsive by rapidly adding instances to cater to the surge.
    
* **Nighttime down**: As the night falls and traffic goes down, Auto Scaling scales down, terminating unnecessary instances to save costs while maintaining a minimal, efficient setup.
    

### 👨🏼‍💻 **Task: 2**

* Create an `Auto-scaling group` using an earlier created `launch template` specify the required information, and specify the `Desired capacity 1`, `Max capacity 3` and `Min capacity 1`
    
* Once ASG is created verify the ASG has maintained its `Desired capacity 1` or not means 1 instance should created using ASG.
    

1. **<mark>Create Auto-scaling group(ASG):</mark>**
    
    Go to the AWS management console on the left side at the bottom and `Click on` `Auto Scaling Groups` &gt; and `Click on Create Auto Scaling group`.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697222737697/a0c3f925-8f5e-4107-975e-64bda9f7235a.png align="center")
    
    In the `Name` provide the name, in the `Launch template` select created or create new and `Click on Next`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697222985428/26b9094f-a99d-4af7-bd2b-8a993f66a0a2.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697223012825/f196c6e7-d579-47d2-9515-b0c31e4986a7.png align="center")
    
    In the `Network` select if you have your VPC created or keep it as it is, In `Availability Zones and subnets` select as per your wish and `Click on Next`.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697223179533/f02a2574-ad5a-4c55-b4ca-33615461fd61.png align="center")
    
    On the next page in the `Load balancing` keep `No load balancer` for now. Keep the remaining configuration as it is and `Click on Next`.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697223342091/edacc722-a3d9-420b-8397-580658a55b68.png align="center")
    
    On the next page in the `Configure group size and scaling policies` set the `Desired capacity is 1` , `Minimum capacity is 1` , `Maximum capacity is 3`
    
    keep the remaining configuration as it is and `Click on Next`.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697223526291/535f870e-ac96-4b64-b547-ab3077dac503.png align="center")
    
    On the next page in `Add notifications - optional` do not add the notification directly `Click on Next`.
    
    On the next page in `Add tags` add if you want to add tags to the ASG. and `Click on Next`.
    
    On the next page Review your configuration and `Click on Create Auto Scaling group`.
    
2. **<mark>Verify the ASG &amp; EC2 Instance:</mark>**
    
    You can see as soon as ASG created, `1 EC2 Instance is also created because ASG maintain its desired state 1`.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697223994323/6d92c64f-d829-4fd3-90cf-d5fbe6593740.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697224012683/d2e4112d-1140-4f50-b298-5a022a695e5e.png align="center")
    
3. **<mark>Delete ASG &amp; Verify EC2 Instance:</mark>**
    
    Once you `delete the ASG`, the `running instances will also get terminated`.
    
    `Go to ASG` &gt; `Select the ASG` &gt; `go to Action` &gt; `Click on Delete` &gt; Confirm the deletion and `Click on delete`.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697224255709/e5c360c6-dec4-4a9e-a411-e7a9e6606f27.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697224422805/e2ab5ee4-42f8-499e-9dba-a25c40950719.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697224507616/3a820a65-0a85-4fda-99c9-5ca596b31d8a.png align="center")
    

### 📝 **Summary**

* In this blog, I have discussed how to automate EC2 instance creation using Launch Templates so we can save our desired configuration in the form of Launch templates can in the future.
    
* We have also seen how can create the EC2 instance using the launch template and make our task automated and make our desired configuration ready for future use.
    
* Instance Types: We have seen the various types of instance types we can use the instance according to our needs and requirements.
    
* Auto Scaling Groups: We have seen the ASG how it provides us the autoscaling functionality based on the criteria.
    
* We will see more about ASG and how ASG is in Load Balancer in upcoming blogs.
    

---

> **Thank you🙏🙏... for taking the time to read this blog. I hope you found the information helpful and insightful. So please keep yourself updated with my latest insights and articles on DevOps 🚀 by following me on**
> 
> So, Stay in the loop and stay ahead in the world of DevOps!
> 
> ***Happy Learning !... Keep Learning ! 😊***