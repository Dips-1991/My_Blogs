---
title: "Day-24 Task: Complete Jenkins CI/CD  Project"
datePublished: Mon Apr 17 2023 23:48:34 GMT+0000 (Coordinated Universal Time)
cuid: clglhlln7000009mr4w676h8e
slug: day-24-task-complete-jenkins-cicd-project
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1681775168439/ef8dedcb-c528-475d-bec2-34089e8471cc.webp
tags: docker, github, webhooks, jenkins, docker-compose

---

Hey, I am going to Integrate and Deploy the ***Node JS To-Do app using*** `EC2server, GitHub, Docker,` and most important `SSH connection between Jenkins Job and GitHub` and `Jenkins with a GitHub hook trigger for GITScm polling` *feature of Jenkins*.

### ***Prerequisite***

* **Git Understanding**
    
* **GitHub Account**
    
* **AWS Account for the Virtual Machine(EC2 Instance)**
    
* **Docker Understanding**
    
* ***Docker Compose* Understanding**
    
* **Jenkins Understanding**
    

***Note:*** Here we will use ***AWS EC2 with Ubuntu Linux OS***

***Now Let's get started implementing the complete Jenkins CI/CD pipeline***

### ***Fork Project To Your GitHub Account***

You can use this TO-DO app in case you do not have any project

Here is the link [**TO Do App Git Repo**](https://github.com/Dips-1991/node-todo-cicd-Deepak)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681747397584/444548bb-b33c-480a-8b86-71b8a752dbdc.png align="center")

### ***Create EC2 Instance (Virtual Machine)***

Here we will use Ubuntu as an AWS EC2 Instance(Virtual Machine)

***Please check here-&gt;*** [**How to Create EC2 Instance step by step**](https://www.guru99.com/creating-amazon-ec2-instance.html)

Now we will install Jenkins on this EC2 instance and below are the commands.

### ***Installation Off Jenkins***

***Please Check Here -&gt;*** [Installation of Jenkins on Ubuntu](https://hashnode.com/edit/clggwp5vz000009mcbwn33g8b)

### ***Connection Between Jenkins Job & GitHub Repository via GitHub Integration.***

To Create an SSH connection between your `Server(EC2 Instance)` and `GitHub` we need `SSH key`, Let's create it.

* Connect your `EC2 instance` and go to the `Terminal` and use the below `ssh-keygen` command to generate `SSH key`
    
    ```plaintext
    ssh-keygen
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681759504459/6b30490f-2b94-4706-b771-f150ddc697cc.png align="center")
    
* You can see the message as `"Your identification has been saved in /home/ubuntu/.ssh/id_rsa` `Your public key has been saved in /home/ubuntu/.ssh/id_`[`rsa.pub`](http://rsa.pub/) The key fingerprint is:"
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681759707806/698dc00f-bd80-4023-9f8e-212e1c0afe7e.png align="center")
    

### ***Adding SSH & GPG keys In GitHub And Jenkins Project***

* Go to `GitHub` &gt;&gt; `Setting` &gt;&gt; `SSH and GPG keys.`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681760854538/3610a390-de72-431c-abbd-336b8bd580c8.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681760787370/fee7f300-a81b-4952-b6d8-ac8304e9b818.png align="center")
    
* Click on `New SSH key`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681760984898/c1ef9e16-f5cd-4a1b-b6f2-4c99805be108.png align="center")
    
* Provide the `Title` and select the `Key type` **as** `Authentication Key` and also add `public key` in the key field that we created using ssh-keygen
    
* Click on `Add SSH Key` and provide your GitHub password to confirm and you will see the SSH key is added
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681761276395/ab33c1e5-c07b-4ef1-b259-8e2babf35ef4.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681761405330/6d67f19b-4b8f-4190-a06c-103037f976c4.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681761688033/1c5204f3-ca06-415b-a703-4860718a9b96.png align="center")
    

### ***Create Jenkins Project***

As earlier we have installed Jenkins on our server and make sure `port 8080` is open in the server security group to access the Jenkins dashboard

Here we will use `Docker, Docker-compose` to deploy the application in the `Docker container`

* Access the `Jenkins dashboard` using `server ip` with `port 8080` as shown below
    
    ```plaintext
    <server-ip>:8080
    ```
    
* Now go to the `dashboard` and create `New Item/Create a job`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681762920537/6fa3f28b-92fb-4c79-b56b-1a58c85a85d5.png align="center")
    
* Enter the `Item/project Name` and select the `Freestyle project` and click on `Ok`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681763243661/63d7444e-ba24-4bcb-bf0f-38b38b325a18.png align="center")
    
* Now once you created the job enters the `Description` and select the `GitHub project` and copy and enter the GitHub repository project URL as `Project url`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681763615036/204af441-5fd9-4da9-8e87-418aed7d28be.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681763690030/4d12c7c4-7336-43c7-a8c6-0baa6628ed39.png align="center")
    
* Now in `Source Code Management` enter the same repository url we have copied as `Repository URL` field
    
* In the `Credentials` section click on `Add`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681764042043/3b8a0a96-70c7-48bd-af25-3436bfb95f64.png align="center")
    
* Now in the pop-up window keep `Domain` as it is
    
* In the `Kind` select `SSH Username with private key`
    
* In the `Scope` keep it as it is
    
* In the `ID` provide as per your
    
* In the `Description` provide as per
    
* In the `Username` provide your server username in my case it is `ubuntu`
    
* In the Private key add the `private key` which we created using the `ssh-keygen command` and click on `Add`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681764854708/f2c188e0-0d2f-4d12-8896-c3e39865ddcb.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681765042305/4e3e78a6-77e6-435f-b265-7aaea2617ee9.png align="center")
    
* Now in Credentials select which we have created now
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681765363833/7e4e52f7-6818-4bff-80bf-cef7ae4f1b98.png align="center")
    
* In the `Brances to build` keep the `Branch Specifier` as it is in my case it is `*master`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681765562527/75c4c625-ea10-49df-9e91-3da05e6457ab.png align="center")
    

### ***Automate Building And Running Containers***

Note: make sure `Docker and Docker-compose` should install on the server

***Please check Here -&gt;*** [Install Docker on Ubuntu Server](https://hashnode.com/edit/clf3s741o00050al05z8a8ab2)

To install Docker-compose use `sudo apt install docker-compose -y` command

* Now in the `Build Step` under `Execute shell` run the application using `Docker compose` add the command `Apply and Save`
    
* For this first, we have to create the `Docker compose file` to deploy the `Docker container`  
    It is best practice to keep the `Docker compose file` in the `Repository`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681802833198/5a00af1b-d9eb-433b-bec8-f3743bd8ab8e.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681769561716/ee83d143-0e26-45c8-8da4-92eb2dc0f9c8.png align="center")
    
* ***Note:*** If you got a `Permission denaied` related error while building
    
    Add the `Jenkins as user` in the `docker group` Use the below command and reboot the server
    
    ```bash
    sudo usermod -a -G docker jenkins
    sudo rebbot
    ```
    
* After Click on `Build Now` and after successfully build go the `Console output` and check as a `success` the message at the end
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681769055758/0c6d768d-8589-4d97-937b-6b506e2950cc.png align="center")
    
* Now you can see the `Docker container` is deployed and up and running
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681769665539/ab493f6f-db73-4dc1-b880-90835b6a6628.png align="center")
    
* Now copy your Instance Public-IP address and add `:8000/todo` to access the application as below
    
    `[Instance-public-ip]:8000/todo`
    
* ***BBBBoooooooooMMMMM Congratulation we have successfully deployed our application using docker 🕺🕺👏👏🎉🎉***
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681800344163/c8740296-7933-4d31-a5d7-93d7eaafe18c.png align="center")
    

### ***Automate Deployment Using Webhook***

***Install Pugin:***

* Here we need the `GitHub Integration` plugin
    
    * Open your `Jenkins dashboard.`
        
    * `Click` on the `Manage Jenkins` button on your Jenkins dashboard
        
    * `Click` on `Manage Plugins`
        
    * Go to the `Available plugin`
        
    * Search `GitHub Integration`plugin in the `search box`
        
    * `Click` on `Install without restart`
        
    * Click on Restart Jenkins when installation is complete.
        
    * Relogin into Jenkin
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681770840370/a051e4d5-0583-42d3-8d58-10cfbcb45748.png align="center")
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681770914336/285fa64e-d5cd-4b6f-a517-b6b99f97e2cf.png align="center")
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681771082042/fc72ccd6-9e14-4679-9f65-0a9b6400a9ad.png align="center")
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681771192316/2e6a2a38-5ac4-42ac-9ee9-a7dfcb844fdc.png align="center")
        

***GitHub-Webhook Configuration:***

* Go to your `GitHub repository` and click on `Settings.`
    
* Click on `Webhooks` and then click on `Add webhook.`
    
* In the `Payload URL` field copy and paste your `Jenkins environment URL`. and at the end of this URL add `/github-webhook/`
    
* In the `Content type`select: `application/json` and leave the `Secret` field `empty`.
    
* In the `Which events would you like to trigger this webhook?` section keep `Just the push event.` and click on `Add webhook`
    
* `Refresh` the page until you will get the `Right sign` ✔
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681771901314/3001f0e8-4fc3-4df1-af0f-225cd739fbb2.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681802425341/848c5b0c-8319-4a81-a637-a5f9c751f7eb.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681802571049/9ef97358-0d32-4343-8100-fe935df687b9.png align="center")
    
* Go to `Jenkins` &gt;&gt; `Your Job` &gt;&gt; `Configure` &gt;&gt;`Build Triggers` and select `GitHub hook trigger for GITScm polling` and click on `apply and save`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681773053069/43405750-a0cc-4550-bcf6-1110f7f35366.png align="center")
    
* Now we are at our final step make some changes in the code and watch the Jenkins dashboard
    
    Here we have changed the heading `"Welcome To The Amazing & Awesome DevOps World"` to `"Welcome To the DevOps Community"` and committed the changes at the repository itself
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681800791948/0fd5cc80-afad-4522-98c4-1955a692a8a2.png align="center")
    
* After we have changed the code in the repository and committed the changes the `magic happens` 🕺🕺👏👏🎉🎉... Our Job build execution starts without clinking on `Build Now.`
    
* `WebHook` is `added to trigger` *the* `execution of Jenkins jobs` *based on* `GitHub events`*.* If anyone in the developer team changes the code, it will automate the **build now** process like this.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681801904254/b2058a45-92bd-4d78-ba73-7e89635f88e3.png align="center")
    
* We can also see the `docker container` running in the command line
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681802011504/fc0d0c1c-6aa2-4e4b-b8f2-9c4a227248a8.png align="center")
    
* And ***Finally!!!*** the changes have been reflected as well
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681802122246/a9563964-01f7-44df-976f-d1a5e91a444a.png align="center")
    

***BBBBoooooooooMMMMM*** **Congratulation we have successfully automated to trigger the job using Webhook** 🕺🕺👏👏🎉🎉

---

> ***Thank you for reading the article.***
> 
> ***Thanks for your valuable time.***
> 
> ***Happy Learning !... Keep Learning ! 😊***