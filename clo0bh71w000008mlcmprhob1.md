---
title: "Day-41: Setting up an Application Load Balancer with AWS EC2 🚀 ☁"
datePublished: Sat Oct 21 2023 17:31:40 GMT+0000 (Coordinated Universal Time)
cuid: clo0bh71w000008mlcmprhob1
slug: day-41-setting-up-an-application-load-balancer-with-aws-ec2
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1697909436188/fc393e2a-4dc0-472f-825e-91cb0876c30f.jpeg
tags: aws, devops, elb, tws, aws-elastic-load-balancer

---

### ✨**Introduction**

Well, in the previous blog, we have discussed about `Launch template` configuration, Autoscaling/`Autoscaling Groups` to make the application highly available.

Now in this blog, we are deep-diving into the ***AWS Elastic Load Balancer.***

### 🏋 **What is Load Balancing?**

Load balancing is the distribution of workloads across multiple servers to ensure consistent and optimal resource utilization. It is an essential aspect of any large-scale and scalable computing system, as it helps you to improve the reliability and performance of your applications.

![load balancing diagram](https://www.nginx.com/wp-content/uploads/2014/07/what-is-load-balancing-diagram-NGINX-1024x518.png align="left")

### ⚖ **Elastic Load Balancing**

AWS Load Balancers are virtual devices or services that distribute incoming network traffic across multiple targets, such as Amazon EC2 instances, containers, or IP addresses, to ensure your applications are highly available, fault-tolerant, and performant.

### 🛠️ **How Elastic Load Balancing Works**

![AWS ELB - Elastic Load Balancer | Why and What is ELB? | What are listeners  and target groups? - YouTube](https://i.ytimg.com/vi/fMgA3rE0aPY/maxresdefault.jpg align="left")

A load balancer accepts incoming traffic from clients and routes requests to its registered targets (such as EC2 instances) in one or more Availability Zones.

The load balancer also monitors the health of its registered targets and ensures that it routes traffic only to healthy targets. When the load balancer detects an unhealthy target, it stops routing traffic to that target. It then resumes routing traffic to that target when it detects that the target is healthy again.

### 👀 **Key Features & Benefits of Elastic Load Balancing**

* **High Availability**: Load balancers distribute traffic across multiple instances, reducing the risk of a single point of failure and ensuring high availability.
    
* **Auto Scaling**: Load balancers can work with auto-scaling groups to automatically adjust the number of instances based on traffic load.
    
* **Security**: Load balancers can act as a shield against distributed denial-of-service (DDoS) attacks by providing protection and mitigation services.
    
* **SSL/TLS Termination**: They can offload SSL/TLS encryption and decryption, reducing the processing burden on your backend instances.
    
* **Session Management**: Some load balancers support session affinity, which ensures that a user's requests are consistently sent to the same backend instance.
    

### 🔠 **AWS Load Balancer Types**

There are four AWS load balancer types supported

![LoadBalancers_Diagram](https://k21academy.com/wp-content/uploads/2020/09/LoadBalancers_Diagram.png align="left")

### ⭐ **Classic Load Balancer**

* **Classic Load Balancer (CLB)** is a legacy load balancer that is no longer recommended for new applications. It is a Layer 4 load balancer
    
* Supports HTTP, HTTPS, TCP, and SSL listeners and supports sticky sessions using application-generated cookies.
    
* **AWS has announced that CLB will be deprecated on December 31, 2022**.
    

### 💻 **Application Load Balancer**

* AWS Elastic Load Balancing automatically distributes incoming traffic across `multiple targets, such as EC2 instances, containers, and IP addresses`, in one or more Availability Zones.
    
* The Load Balancer distributes the traffic to the appropriate `Target Groups`.
    
* New feature-rich, `layer 7` load-balancing platform.
    
* Supports `web sockets, HTTP, HTTPS, microservices, and container-based applications`, including deep integration with EC2 container service.
    
* Support for `path-based and host-based routing`. Also, provide routing requests to multiple applications on a single EC2 instance.
    
* `Cross-zone load balancing` is always enabled and you can also specify Lambda functions are targeted to serve HTTP(S) requests.
    
* Supports load balancer-generated cookies only for sticky sessions.
    
* **Key Components of an Application Load Balancer:**
    
    1. **Listeners:** ALB uses listeners to check for connection requests from clients. These listeners are configured with specific protocols and ports and are at the forefront of routing decisions.
        
    2. **Rules:** Listener rules define how the load balancer routes requests to its registered targets. Each rule consists of a priority, one or more actions, and conditions. Rules allow for sophisticated traffic management based on various factors.
        
    3. **Target Groups:** These groups route requests to registered targets, such as EC2 instances, using specified protocols and port numbers. A target can be registered with multiple target groups, and health checks can be configured per target group
        
    
    ![Application load balancer](https://k21academy.com/wp-content/uploads/2020/08/illustration-2.png align="left")
    

### 🌐 **Network Load balancer**

* **Network Load Balancer (NLB)** shines as a high-performance solution designed to operate at the `transport layer (Layer 4)` of the Open Systems Interconnection (OSI) model.
    
* Connection baseload Balancing and it supports `TCP protocol`.
    
* Support for static IP addresses for the load balancer. or assign one Elastic IP address per subnet enabled for the load balancer.
    
* Cross-zone load balancing is disabled by default.
    
* **Key Components of a Network Load Balancer:**
    
    1. **Listeners**: NLB uses listeners to check for incoming connection requests from clients. Listeners are configured with specific protocols and ports, serving as the entry point for traffic.
        
    2. **Target Groups**: These groups route incoming requests to registered targets, which can be EC2 instances or IP addresses. You can also configure target groups to support various protocols like TCP, UDP, TCP\_UDP, and TLS, providing flexibility.
        
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697868300430/9ff452d6-85d1-402f-88aa-54adae57f261.png align="center")
    

### 🚪**Gateway Load Balancer**

* Gateway Load Balancer (GWLB) stands out as a specialized solution tailored for deploying and managing virtual appliances.
    
* It makes it simple to scale, install, and manage your third-party virtual appliances.
    
* Provide you with one gateway for distributing traffic across multiple virtual appliances, while scaling them up, or down, based on demand.
    
* **Gateway Load Balancer Endpoints:**
    
    * GWLB uses Gateway Load Balancer endpoints to securely exchange traffic across Virtual Private Cloud (VPC) boundaries
        
    
    ![AWS Gateway Load Balancer 1O1. Digital equipment such as firewalls… | by  Piyush Jalan | Medium](https://miro.medium.com/v2/resize:fit:1121/1*qNMaVza5BzgrimG2fz0gNg.png align="left")
    

### ✍️ Task 1:

**Launch 2 EC2 instances with an Ubuntu AMI and use User Data to install the Apache Web Server.**

**Modify the** `1st instance` **index.html file to include** `your name` **so that when your Apache server is hosted, it will** `display your name` **also do it for** `2nd instance` **which includes"** `TrainWithShubham Community is Super Aweasome :)` **".**

**Create an** `Application Load Balancer (ALB)` **in EC2 using the AWS Management Console.**

**Add EC2 instances to the ALB as Target Groups.**

**Verify that the ALB is working properly by checking the health status of the target instances and testing the load-balancing capabilities.**

1. ✅<mark>Launch The Instance:</mark>
    
    launch 2 EC2 instances with an Ubuntu AMI and use User Data to install the `Apache Web Server`.
    
    Use the User-Data script to install the Apache web server.
    
    ```apache
    #!/bin/bash
    sudo apt-get update
    sudo apt-get install -y nginx
    sudo systemctl start nginx
    sudo systemctl enable nginx
    echo "<html><body><h1>Hello Myself Deepak</h1></body></html>" | sudo tee /var/www/html/index.html
    ```
    
    ```apache
    #!/bin/bash
    sudo apt-get update
    sudo apt-get install -y nginx
    sudo systemctl start nginx
    sudo systemctl enable nginx
    echo "<html><body><h1>TrainWithShubham Community is Super Aweasome :)</h1></body></html>" | sudo tee /var/www/html/index.html
    ```
    
2. ✅<mark>Create Target Group:</mark>
    
    To create an application load balancer go to `Instance` &gt; `Load Balancers` &gt; Under `Click on Taget Group under load balancer` &gt; `On the next page Click on Create target group` &gt; `Add required information` .
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697905574089/6ca160a0-1e9a-4384-9912-a29755787d26.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697905649150/812c8b55-f187-4702-b7ad-fee04fb8ae5e.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697905838705/60cefea2-345f-4ee4-9328-cb4b981411c0.png align="center")
    
    `In the Register targets select both the Ec2 instances and click on "Inclide as pending below"` &gt; `Click on Create target group` .
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697906157063/4b91425a-4123-42c0-9731-cfb7668997f9.png align="center")
    
    You can see Target group is created but we have not associated it with any load balancer yet.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697906324722/c248e31b-8fae-455b-a7e8-7e68ae8e6d75.png align="center")
    
3. ✅<mark>Create Application Load Balancer (ALB):</mark>
    
    To create an application load balancer go to `Instance` &gt; `Load Balancers` &gt; `Click on Create load balancer` &gt; `On the next page Select the load balancer type as "Application Load Balanver"` &gt; Click on Create &gt; `Add required information`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697905073286/c726ced2-5c30-42d1-8dcc-8072deed0b0e.png align="center")
    
    Choose the `IP address type`, `VPC` and in Mapping choose `AZs`where you want your ALB to route the traffic.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697905119705/3026f68c-205d-45ab-8f4e-e33bae98d1cb.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697905206561/acd2ee9e-e118-4477-b7da-57fdb2c37815.png align="center")
    
    Next, create a new Security group and allow the `HTTP protocol with port 80`. and
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697906640782/df6eb9e9-3074-4591-bb7f-6497508dba76.png align="center")
    
    Now select the newly created security group for the load balancer where we have allowed port 80
    
    In `Listeners and routing` select the target group that we created earlier. Keep the remaining setting as it is and `Click on Create load balancer`.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697906810882/b05170bc-17c7-400e-883c-fab55e85be74.png align="center")
    
4. ✅<mark>Verify Application Load Balancer Working:</mark>
    
    First, we have to modify the `Security groups` of both the EC2 instances where we will add the new `HTTP` rule and in `Source` we will add the Security Group which we have created for the `Application load balancer`.
    
    What we will achieve here is the request is coming on both the EC2 instances only from the Load balancer and the Load balancer also balancing the load.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697907484839/5ba2cec7-5fef-4f49-b2d9-fa1d606fc27c.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697907698629/675b1f97-c731-492c-818a-4fe5f2610a31.png align="center")
    
    Now, when we use a load balancer to manage the traffic load balancer provides us the `DNS name` which we have to use to test whether the load is balancing on both instances or not.
    
    Go to Load Balancer you will see the `DNS name`.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697908225235/49cfb387-e19a-45f3-a8d6-5e2b8d7e849e.png align="center")
    
    Copy the `DNS name` and paste it into the browser and keep reloading the page you will see the load is balancing and you will get the response from both instances.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697908381776/5bf9349f-30a1-4725-843a-6ff739fb9859.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697908402005/e4d217fc-cadb-4c07-9633-68c3b4508298.png align="center")
    

### 📜**Conclusion**

AWS load balancers are invaluable tools for any application hosted on the cloud. They enhance performance, increase reliability, and provide a seamless experience for users. By leveraging load balancers, you can focus on developing your application, knowing that AWS is handling the complexities of traffic distribution.

---

> **Thank you🙏🙏... for taking the time to read this blog. I hope you found the information helpful and insightful. So please keep yourself updated with my latest insights and articles on DevOps 🚀 by following me on**
> 
> So, Stay in the loop and stay ahead in the world of DevOps!
> 
> ***Happy Learning !... Keep Learning ! 😊***