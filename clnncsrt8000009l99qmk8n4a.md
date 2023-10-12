---
title: "Day-39 Part-1:☁Amazon EC2 User-Data🤵🏻📑"
datePublished: Thu Oct 12 2023 15:47:39 GMT+0000 (Coordinated Universal Time)
cuid: clnncsrt8000009l99qmk8n4a
slug: day-39-part-1amazon-ec2-user-data
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1697009449488/04ee7d4b-8286-44b5-ada6-bfb6283ec0f4.png
tags: cloud, aws, tws, ec2-user-data, ec2-instance

---

### 📖 **Introduction**

In the last blog [Getting Started with AWS Basics☁](https://deepakcloud22.hashnode.dev/day-38-task-getting-started-with-aws-basics#heading-what-are-regions) we learned about the basics of ***AWS***, ***What is IAM***, ***Users****,* **and *User groups***. We have also learned about ***Regions*** and ***Availability zones***, and we have performed some hands-on.

In this article, we are going to learn about the use of ***User data in AWS***.

***So let's get started...🏃‍♀️***

### **🤔 What is Amazon EC2 User Data?**

* Amazon EC2 user data is a feature that allows you to pass metadata to your EC2 instances when they’re launched.
    
* This metadata can be used to automate certain tasks, such as installing software packages, configuring settings, and running scripts.
    
* User data is passed to your EC2 instances as plain text, and it’s automatically made available to your instance as a shell script. This means that you can use any scripting language you want to write your user-data script
    

### 💁 **How to Use Amazon EC2 User-Data**

To use Amazon EC2 user data, you’ll need to create a user data script. This script can be written in any scripting language you want, but we recommend using a shell script because it’s easy to get started with.

Here’s an example user-data script that installs the **Jenkins** on an **EC2 instance**:

1. ✍ **Create the Script File:**
    
    * Here is the shell script file to install the Jenkins on the EC2 instance using user data.
        
    * This script updates the **package manager**, **downloads the required key and package**, **installs Jenkins**, e**nables Jenkins,** and **starts automatically on boot**.
        
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
        ```
        
2. ✈️ **Launch EC2 Instance:**
    
    * Go to **EC2 &gt; Instance** and click on **Create instance.** Provide the required configuration.
        
    * Now this is the place where we need to add your script data. **Expand the Advanced Details tab.** Add the **script** or **choose the file** in the **User data** section and click on the launch instance.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697001637975/1aa2ce76-8d96-4720-b3e9-6a80541d8de2.png align="center")
        
3. ✅ **Verify the installation:**
    
    * Connect the instance and verify the installation using the command.
        
        ```apache
        jenkins --version
        systemctl status jenkins
        ```
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697002258376/520d8c44-06f7-429a-8713-4274691eec82.png align="center")
        
    * Make sure the port `8080` should open in your EC2 instance `Security Group` because Jenkins runs on port 8080.
        
    * Go to the browser and type EC2 instance public IP followed by port 8080
        
        `<EC2-Public-IP>:8080`
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697002485719/4d6a6ad1-2271-4bca-9ada-147d27a1b1c1.png align="center")
        
    * We can see the Jenkins page is visible means we successfully installed the Jenkins on EC2 instance using User data at the time of launch Instance.
        

### ⚖️ **Conclusion**

* Amazon EC2 user data is a powerful feature that allows you to automate your infrastructure setup. By passing metadata to your EC2 instances as plain text, you can use any scripting language you want to automate tasks like installing software packages, configuring settings, and running scripts.
    
* In this blog post, we’ve explained what user data is, how it works, and how you can use it to automate your infrastructure setup. We’ve also provided an example user-data script that installs the Apache web server on an EC2 instance.
    
* If you’re looking to automate your infrastructure setup, Amazon EC2 user data is a great place to start. Give it a try and see how it can help you streamline your workflow and save time.