---
title: "Guide to Understanding Jenkins🧛‍♂️Master-Slave 👷‍♂️👷‍♀️ Architecture 🚀"
datePublished: Wed Sep 06 2023 16:05:28 GMT+0000 (Coordinated Universal Time)
cuid: clm7xl0mh000009l5dzqlaawn
slug: guide-to-understanding-jenkinsmaster-slave-architecture
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1694016235596/255253d1-e99f-4e2e-9956-f79a6cf145c4.png
tags: jenkins, jenkins-devops, jenkins-master-slave, jenkins-pipeline, devops-trainwithshubham-jenkins-cicd-automation-devopsengineer-90daysofchallenge-cloudcomputing-linux-aws-azure-testing-blogging

---

Jenkins, the open-source automation server, is a powerhouse tool for continuous integration and continuous delivery (CI/CD). One of its standout features is the master-slave architecture, which empowers users to scale their build and deployment processes efficiently. 🏗️

### ***🎆 Introduction***

In this blog post, we'll deep dive into the `Jenkins master-slave architecture`, exploring its benefits, setting it up, and providing an example to illustrate its usage. 🌐

### 🧛‍♂️ ***Jenkins Master***

Jenkins’s server or master node holds all key configurations. The Jenkins master server is like a control server that orchestrates all the workflow defined in the pipelines.

👇 Following are the characteristics of Jenkins Master:

* Scheduling build jobs.
    
* Dispatching builds to the slaves for the actual execution.
    
* Monitor the slaves (possibly taking them online and offline as required).
    
* Recording and presenting the build results.
    
* A Master instance of Jenkins can also execute build jobs directly.
    

### 👷‍♂️👷‍♀️ ***Jenkins Slave/Workers***

An agent is typically a Java executable that runs on a machine or container that connects to a Jenkins master and this agent actually executes all the steps mentioned in a Job.

When you create a Jenkins job, you have to assign an agent to it. Every agent has a label as a unique identifier.

When you trigger a Jenkins job from the master, the actual execution happens on the agent node that is configured in the job.

👇 Following are the characteristics of Jenkins Master:

* It hears requests from the Jenkins Master.
    
* Slaves can run on a variety of operating systems.
    
* You can configure a project to always run on a particular Slave machine or a particular type of Slave machine.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693486764516/9b7e1965-9bbe-45b6-912a-651240574eb8.png align="center")

### 🌟***Benefits of Jenkins Master-Slave Architecture***

🔹 ***Scalability:*** Master-slave architecture enables distributing workloads across multiple nodes, improving performance and accommodating larger projects.

🔹 ***Resource Optimization:*** Slaves can be configured on different machines with different operating systems and hardware, optimizing resource utilization.

🔹 ***Isolation:*** Build jobs on different slaves run in isolated environments, preventing dependencies or conflicts from affecting each other.

🔹 ***24/7 Availability:*** With dedicated slave nodes, builds and deployments can continue even if the master node experiences downtime.

🔹 ***Security:*** Sensitive code and data can be isolated on specific slave nodes, enhancing security.

### ⚙️***Setting Up Jenkins Master-Slave Architecture***

1. ***Pre-requisites***
    
    Let’s say we’re starting with a fresh Ubuntu 22.04 Linux. To get an agent working make sure you install `Java (same version as Jenkins master server ) and Docker on it.`
    
2. ***Prepare Master and Slave Node***
    
    Create two EC2 instances and name it `Jenkins-master` and `Jenkins-slave1`.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694004300167/ebb4c75c-4d08-4b0d-8ca9-7515c2e12cef.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694004328230/e75749ec-d683-4263-a512-8460f19f5e3f.png align="center")
    
3. ***Generate SSH keys on “Jenkins-master”***
    
    1. Generate SSH keys on `Jenkins-master` by running
        
        “`ssh-keygen`”. or if you face the SSH key format issue try with `ssh-keygen -b 1024 -t rsa`
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694004617731/32fe9f51-acbc-4dd0-9d9d-ffb87691be1f.png align="center")
        
    2. You can generate SSH keys on the slave node also and configure them accordingly.
        
    3. Now goto `“.ssh`” folder and there will be public and private keys generated in `Jenkins-master`.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694004683355/579097c8-291b-4cf1-9f84-b2e81c6584af.png align="center")
        
4. ***Configure Slave Nodes***
    
    1. Add public key from “`Jenkins-master`” to “`Jenkins-slave1`” under location “`.ssh/authorized_keys`”.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694004881890/aa7aeac5-3a94-4450-90c9-7ac06e4a091d.png align="center")
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694004848792/b4e62287-7815-483a-902b-5ee4c92a8d70.png align="center")
        
5. ***Connect Slave Nodes to Master***
    
    1. Go to the `Jenkins dashboard`, and click on “`Manage Jenkins`”.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693576512759/c0cf68f1-6674-43b0-9548-43828fd6cd45.png align="left")
        
    2. Now, click on “`Manage Nodes and Clouds`”.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693502830203/257ac00f-07a2-4da8-ac9c-846228c21aea.png align="left")
        
    3. Now, click on “`+ New Node`”.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693502996033/bdefc294-5011-4f5a-9a27-275f9bffd89b.png align="left")
        
    4. Enter the `Node name` and select `Permanent Agent` and click on `create`.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693503198128/aafb9dc1-2a5a-4086-828d-88d847f9c7fe.png align="left")
        
    5. Enter the required details as per your requirement.
        
    6. Make sure the `Remote root directory` you are specifying should be present in the slave node.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693503445680/99256ac5-18ac-4a4a-8eba-3ca6d524c9de.png align="left")
        
    7. Enter the `Labels` which is required.
        
    8. In the `Usage` Select as per your requirement I will select it here `Use this node as much as possible`.
        
    9. In `Launch method` Select as per your requirement I will select it here `Launch agents via SSH`.
        
    10. In the `Host` enter your `Jenkins slave node public IP address` .
        
    11. In `Credentials` Select your credentials or click on `Add` To add the credentials I will `Add( and click on Jenkins pop-up)` Here the new credentials.
        
    12. Select `Domain` as it is.
        
    13. In the Kind select `SSH Username with private key` .
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693505013667/8ff31c3a-fb5d-4b75-9e58-fc4e916d0d6f.png align="left")
        
    14. In the Username add what user you want to connect to the target server I will choose `ubuntu`as my target server user.
        
    15. Go to the Jenkins-master server in go to the `.ssh/` open the `id_rsa` copy the secret key.
        
    16. In the `Private Key` Select `Enter directly` and click on `Add` .
        
    17. `Enter/Paste` the secret key carefully and enter the passphrase If you provided at the time of generating and click on `Add` .
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694005288010/653955c8-0f2b-4b82-b4a9-6c04bfc8b042.png align="left")
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694005354772/177cd007-4b56-47e1-b012-c5fb8a05be7f.png align="left")
        
    18. Now select the newly created `credentials`.
        
    19. Add other required details and click on `Save`.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694005432127/b71416cb-fcc7-4800-8275-79d1839c5da5.png align="left")
        
    20. Now you will see slave node is added.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693506512196/8283e530-06a6-4eda-8e3d-1b20d96af175.png align="left")
        
    21. Now click on the newly created slave node and click on `Launch agent.`
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693506593373/129515b0-4c08-4bd8-a988-d077467b3264.png align="left")
        
    22. Now, you can see the agent `Authentication successful` and `Agent successfully connected and online` also connected to Jenkins master.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694005726987/aa62a7e2-6fdf-41bf-8413-184eb68f6e8d.png align="left")
        

### ***🏍Running the Job/Project at the Jenkins-slave1 node***

1. Create a new project or you can tie the existing project with the Jenkins slave node.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694007192971/8a136929-f25e-4059-9019-081dcf2b8645.png align="center")
    
2. Now, go to configurations in your task or project scheduled in Jenkins, **Select** `Restrict where this project can be run` and add the Label as same with the name of Node.
    
3. Click on Save, and your project will be tied to `Jenkins-slave1`.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694007270395/9bcac3ac-268e-41fc-a9a4-ebf0c1490479.png align="center")
    
4. On the Dashboard you can see the slave node is also added
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694007573684/c424c7a5-2a12-4a15-9a81-8e444c06110f.png align="center")
    
5. Once you click on `Build now` the job will be executed by `Jenkins slave1 node`successfully.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694007756973/2bcac072-c00e-422e-9d75-0a66c9bcba8a.png align="left")
    

### 🎉**Conclusion**

In this blog, we have seen how J`enkins master-slave architecture` is an efficient and scalable CI/CD pipeline. It empowers teams to distribute workloads, optimize resources, and enhance security, all while ensuring consistent and reliable builds and deployments. By understanding and implementing this architecture, development teams can achieve greater productivity and streamline their software delivery process.

---

> **Thank you🙏🙏... for taking the time to read this blog. I hope you found the information helpful and insightful. So please keep yourself updated with my latest insights and articles on DevOps 🚀 by following me on**
> 
> So, Stay in the loop and stay ahead in the world of DevOps!
> 
> ***Happy Learning !... Keep Learning ! 😊***