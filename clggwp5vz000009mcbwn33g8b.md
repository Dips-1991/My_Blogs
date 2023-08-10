---
title: "Day-22: Getting Started with Jenkins"
datePublished: Fri Apr 14 2023 18:52:23 GMT+0000 (Coordinated Universal Time)
cuid: clggwp5vz000009mcbwn33g8b
slug: day-22-getting-started-with-jenkins
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1681498152819/ee8ef746-848a-46dd-be6f-619ebdfa8a98.jpeg
tags: jenkins, cicd, jenkins-devops, jenkins-installation, jenkins-on-ubuntu

---

### ***What is Jenkins?***

Jenkins is an open-source continuous integration-continuous delivery and deployment (CI/CD) automation software DevOps tool written in the Java programming language. It is used to implement CI/CD workflows, called pipelines.

Jenkins is a tool that is used for automation, and it is an open-source server that allows all the developers to build, test and deploy software. It works or runs on Java as it is written in Java. By using Jenkins we can make a continuous integration of projects(jobs) or end-to-endpoint automation.

Jenkins achieves Continuous Integration with the help of plugins. Plugins allow the integration of Various DevOps stages. If you want to integrate a particular tool, you need to install the plugins for that tool. For example Git, Maven 2 project, Amazon EC2, HTML publisher, etc.

### ***Why we should use Jenkins?***

* Open Source with great community support.
    
* A lot of plugins
    
* Easy to Install
    
* Free of cost
    
* It is built with Java and hence, it is portable to all the major platforms.
    

### ***What is CI/CD?***

`CI` means `Continuous Integration` Continuous Integration is used to automate pulling the code from source code management, building, and testing. `CD` means `Continuous Delivery/Deployment` is used to automate the deployment of build code with help of manual Intervention. Finally, the CD is Continuous Delivery/Deployment which will automate the deployment as well without manual intervention.

### ***What is Plugin*?**

A `plugin` is a software add-on that is installed on a program, enhancing its capabilities. Plugins allow the integration of Various DevOps stages. If you want to integrate a particular tool, you need to install the plugins for that tool. For example Git, Maven 2 project, Amazon EC2, HTML publisher etc.

### ***Installation of Jenkins***

To download and install Jenkins on various OS you can visit the link [Download Jenkins](https://www.jenkins.io/download/).

Here we will install and use Jenkins on Ubuntu OS. Follow the below steps

\- Here you can see the installation guide on [Jenkin on Linux](https://www.jenkins.io/doc/book/installing/linux/)

***Step 1: Install Java***

* Create an AWS EC2 Instance AMI of your choice I am picking up Ubuntu.
    
* Jenkins requires the Java Runtime Environment (JRE) required to run the Jenkins because Jenkins is written in Java.
    
* Connect to the AWS EC2 instance and update the system and Check if you already have Java installed on your Ubuntu system
    
    To update the system `sudo apt update`
    
    To check the Java version `java --version`
    
* Depending on which Java version you want to install, Java 8 or 11, run one of the following commands:
    
    * To install OpenJDK 8, run:  `sudo apt install openjdk-8-jdk -y`
        
    * To install OpenJDK 11, run:  `sudo apt install openjdk-11-jdk -y`
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681484762407/c0903a46-1c0a-4649-975b-a2ea6fefbfad.png align="left")
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681484866307/47719bbe-35a3-4257-b648-4267287c3b8c.png align="left")
        

***Step 2: Add Jenkins Repository***

It is recommended to install Jenkins using the project-maintained repository, rather than from the default Ubuntu repository. The reason for that is because the Jenkins version in the default Ubuntu repository might not be the latest available version, which means it could lack the latest features and bug fixes.

* Start by importing the GPG key. The GPG key verifies package integrity but there is no output.
    
    **Run:**
    
    ```plaintext
    curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
      /usr/share/keyrings/jenkins-keyring.asc > /dev/null
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681484923107/b6d9d7aa-664e-41c4-901e-1df2da99e833.png align="center")
    
* Add the Jenkins software repository to the source list and provide the authentication key:
    
    ```plaintext
    echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
      https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
      /etc/apt/sources.list.d/jenkins.list > /dev/null
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681485017618/5e23da7c-a0f6-432e-80ab-10c8a195e376.png align="center")
    

***Step 3: Install Jenkins***

* Update the system repository using:
    
    `sudo apt update`
    
* Install Jenkins by running:
    
    `sudo apt install jenkins -y`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681492868371/2d6f782c-0286-4f0f-8e91-f89b4dc08c6e.png align="center")
    
* To check if Jenkins is installed and running, run the following command:
    
    To check Jenkins's version `jenkins --version`
    
    To check Jenkins's status `sudo systemctl status jenkins`
    
    To start Jenkins's `sudo systemctl start jenkins`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681492940986/75730d7b-e097-495a-a6b4-89083d1fff17.png align="center")
    

***Step 4: Allow port 8080 in EC2 instance***

As we know Jenkins works on port 8080 so we need to allow port 8080 in the security group of the EC2 instance

Go to the `EC2 instance` -&gt; in the `security` click on `Security Groups` click on `Edit inbound rules` add Custom TCP as port 8080 and click on save.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681493761741/0875a930-d721-4c90-8804-80fd9c515efd.png align="left")

***Step 5: Access the Jenkins***

* Now Copy your Instance Public Ip and Add 8080 to it to go to the Jenkins page. `<Public-IP>:8080` and paste in the browser and you will see the start-up page on Jenkins
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681493835327/dda49ef5-a29c-47a9-926f-f7389f064908.png align="left")
    
* To ensure Jenkins is securely set up by the administrator, a password has been written to the log ([not sure where to find it?](https://www.jenkins.io/redirect/find-jenkins-logs)) and this file on the server:
    
    `/var/lib/jenkins/secrets/initialAdminPassword` open the file using `cat` command
    
    ```plaintext
     cat /var/lib/jenkins/secrets/intialAdminPassword
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681494288343/0a69cbff-f7f5-4840-bb97-f7c323b33f94.png align="center")
    
* Please copy the password from either location and paste it into the `Administrator password` and click on continue.
    
* Next, select `Install suggested plugins`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681494443036/bde82223-290c-435e-a784-3d0db8f267eb.png align="center")
    
* Now create the first admin user by providing the below information and click on save and continue.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681494710068/d399b41f-7c3e-4a1d-a538-a252f07cdb87.png align="center")
    
* Now you will come to the `Instance Configuration` page keep it as it is as a Jenkins URL and click on Save and Finish
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681494978614/6590a063-6598-4b65-9537-4c0971a1163d.png align="center")
    
* \*\*\*BOOOOOOOOOOMMMMMMM....\*\*\*🕺🕺👏👏🎉🎉We have successfully installed Jenkins
    
    Now click on `Start Using Jenkins`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681495099822/3eae5c71-bce5-4887-abcd-da8ff7b924e9.png align="center")
    
* Now you will see the `Jenkins dashboard`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681495250400/f5b9e145-e7fb-4887-98da-6aff1c935486.png align="center")
    

### *Create a freestyle project to print "Hello World!!*

* Click on Create a job or `New Item` or Click on `Create a job`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681495897175/1a9cdbf9-f64b-4f71-a22c-61e390c3290d.png align="center")
    
* Enter `Job Name` and Select `Freestyle project` and click on ok
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681496234295/0f74da4d-22c9-49da-a06b-e7ed380979e9.png align="center")
    
* Enter the description as per your wish
    
* Now go to `Build Steps` and select `Execute Shell (It is used to run Linux or shell commands)`.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681496546955/efa9edd6-0161-437b-9a11-6a7d4b5d4800.png align="center")
    
* Now enter the command you want to execute then click on `Apply and Save` .
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681496835234/d9a6c9bd-aa1c-4575-bb64-b0990abf0b76.png align="center")
    
* Now Click on `Build Now` then in `Build History #1` will be created and ckck on it to see the `Console Output.`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681497006112/ba4304a6-0f4f-4b0e-b4f6-555488eb2ff4.png align="center")
    
* Let's click on the `Console Output` and see the output as expected
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681497234169/3e5edf92-d899-4ad4-a3ab-c29dc66196b8.png align="center")
    
    \*\*\*BOOOOOOOMMMMMMM...\*\*\*We have successfully created a job in Jenkins to run Hello World and We can see the output in Console. ***Congratulations*** 💐💐 on your first job in Jenkins 🎉🎉.
    
    ---
    
    > ***Thank you for reading the article.***
    > 
    > ***Thanks for your valuable time.***
    > 
    > ***Happy Learning !... Keep Learning ! 😊***