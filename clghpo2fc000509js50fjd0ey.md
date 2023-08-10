---
title: "Day-23 Task: Jenkins Freestyle Project for DevOps Engineers."
datePublished: Sat Apr 15 2023 08:23:21 GMT+0000 (Coordinated Universal Time)
cuid: clghpo2fc000509js50fjd0ey
slug: day-23-task-jenkins-freestyle-project-for-devops-engineers
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1681546921899/fb4cc6b7-57ee-40b5-8d2f-7711873024a7.jpeg
tags: docker, github, git, jenkins, docker-compose

---

### ***What is Jenkins?***

Jenkins is an open-source continuous integration-continuous delivery and deployment (CI/CD) automation software DevOps tool written in the Java programming language. It is used to implement CI/CD workflows, called pipelines.

Jenkins is a tool that is used for automation, and it is an open-source server that allows all the developers to build, test and deploy software. It works or runs on Java as it is written in Java. By using Jenkins we can make a continuous integration of projects(jobs) or end-to-endpoint automation.

Jenkins achieves Continuous Integration with the help of plugins. Plugins allow the integration of Various DevOps stages. If you want to integrate a particular tool, you need to install the plugins for that tool. For example Git, Maven 2 project, Amazon EC2, HTML publisher, etc.

### ***What is CI/CD?***

* `CI or Continuous Integration` is the practice of automating the integration of code changes from multiple developers into a single codebase. It is a software development practice where the developers commit their work frequently to the central code repository (Github or Stash). Then there are automated tools that build the newly committed code and do a code review, etc as required upon integration. The key goals of `Continuous Integration` are to find and address bugs quicker, make the process of integrating code across a team of developers easier, improve software quality, and reduce the time it takes to release new feature updates.
    
* `CD or Continuous Delivery/Deployment` is carried out after Continuous Integration to make sure that we can release new changes to our customers quickly in an error-free way. This includes running integration and regression tests in the staging area (similar to the production environment) so that the final release is not broken in production. It ensures to automate the release process so that we have a release-ready product at all times and we can deploy our application at any point in time.
    

### ***What Is a Build Job?***

* A Jenkins build job contains the configuration for automating a specific task or step in the application building process. These tasks include gathering dependencies, compiling, archiving, or transforming code, and testing and deploying code in different environments.
    
* Jenkins supports several types of build jobs, such as freestyle projects, pipelines, multi-configuration projects, folders, multibranch pipelines, and organization folders.
    

### ***What is Freestyle Projects ?? 🤔***

* A freestyle project in Jenkins is a type of project that allows you to build, test, and deploy software using a variety of different options and configurations.
    

### *Task 1: (Jenkins Freestyle project with Jenkins, GIT, Docker Dockerfile)*

1. Create an agent for your app.
    
2. Create a new Jenkins freestyle project for your app.
    
3. In the `"Build"` section of the project, add a `build step` to run the `"docker build"` command to build the image for the container.
    
4. Add a second step to run the `"docker run"` command to start a container using the image created in step 3.
    

To know more about installing Jenkins visit the link

[https://deepakcloud22.hashnode.dev/day-22-getting-started-with-jenkins](https://deepakcloud22.hashnode.dev/day-22-getting-started-with-jenkins)

***Step: 1***

1\. Once install Jenkins `Login to Jenkins` using EC2 instance public IP with port 8080 `<Public-IP>:8080`

2\. Then create a `"New Item"` freestyle project and click on Ok as shown below :

3\. In this project, we required Docker to run the Docker container.

To install Docker use the below command `sudo apt install docker.io -y`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681504155492/1d652201-4ecd-4151-8f88-0ed29977ce5a.png align="left")

4\. In General, we can specify `descriptions` of our job or Project.

5\. We can specify a `GitHub project` with "`Project URL`*"* which we copied from GitHub repo URL.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681505425779/fb3262be-a51d-442d-a8f7-03e4dedece85.png align="left")

6\. We could also specify `Source code management` with Git info by giving the `repository URL,` and specifying the branch name `main/master` in my case it is `main` as below.

***Note:*** If the GitHub repository is Public then we do not need to provide credentials else repository is private then need to provide credentials.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681505307846/b0d17f93-ad84-4a83-8f56-09596d4dcd0e.png align="left")

7\. In the `"Build Steps"` section of the project, select `Execute shell` and

* Add a build step to run the `"docker build"` command to build the image for the container.
    
* Add a second step to run the `"docker run"` command to start a container using the image created in step 3. and click on `Apply and Save`
    

***Note:*** To avoid permission being denied while trying to connect to the Docker daemon add Jenkins user into the docker group using the below command `sudo usermod -a -G docker jenkins` and reboot the instance `sudo reboot`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681506874094/3d0d377f-a226-4d9c-845a-8e110983ba90.png align="left")

8\. Now, Yo will inside the project and click on `Build Now` to build the project

After successfully build under the `Build History` click on the `build number prefix with #` and see the `Console Output` with all the steps executed by Jenkins

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681507841495/dce4b832-a902-4ad9-b99f-16c23597393d.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681507887963/dc886a00-6fca-47ad-8819-05eda45f68c6.png align="left")

9\. We can see the projects deployed from GitHub at the location

`cd /var/lib/jenkins/workspace` as well

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681509191989/03b68e3e-3abf-4024-b8bc-855c6db333ad.png align="center")

10\. Now we will check the image which we have created using Dockerfile and the container which we have deployed using the image using the below commands

`sudo docker images` To see all the images at the docker host

`sudo docker ps` To see all the running containers

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681509439018/446d6929-721c-46a2-85a8-12380048f8ab.png align="center")

11\. Now use copy the `EC2 instance public ip` and paste it into the browser followed by `:8000` and `app name`

`<Public-IP>:8000/todo`

***Note:*** Expose port `8000` into the `EC2 instance security group` by adding `edit inbound rule`

***Congratulation*** our application is successfully deployed and accessible

🕺🕺👏👏🎉🎉

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681510099475/83ecf173-3a29-4aaa-8268-c408b50b5477.png align="center")

### *Task 2: (Jenkins Freestyle project with Jenkins, GIT, Docker DocerCompose File.)*

1. Create a Jenkins project to run the `"docker-compose up -d"` command to start the multiple containers defined in the compose file.
    
2. Set up a cleanup step in the Jenkins project to run the `"docker-compose down"` command to stop and remove the containers defined in the compose file.
    

***Step1***

1\. In continuing to the first task, we create `docker-compose.yml` the file inside our project. Make sure docker-compose should be installed.

To install use the command `sudo apt-get install docker-compose -y`

To validate the docker-compose file use command

`sudo docker-compose config`

To see the docker-compose use command `cat docker-compose.yaml`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681544333496/ba14fc42-9c81-434a-a451-80bec7db7d53.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681544392665/227571d1-4302-495e-947c-fbaff99ef91a.png align="center")

2\. In `Build step` a section, `add build steps` like this. Here `docker compose down` is taken first to `remove and stop the containers` define in the compose file then afterward we use `docker compose up -d` the command to deploy the container. click on `Apply and save`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681512766891/e6962be1-0cd6-490e-b364-c803c8908302.png align="center")

3\. Now click on `Build Now` Build the project and see the console output by clicking on `Console Output`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681544587761/4b0ac57b-75aa-42a9-ad00-8aed4bf86784.png align="center")

4\. Now you can see the container is created

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681516880485/ed74cf26-f480-457f-93a6-58f16ab41ba0.png align="center")

5\. The compose container also working as expected on port `8001`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1681545852050/2d91221f-428a-4931-bb84-01b777212280.png align="center")

**Reference: Shubham Londhe** : [**Video**](https://www.youtube.com/watch?v=wwNWgG5htxs)

---

> ***Thank you for reading the article.***
> 
> ***Thanks for your valuable time.***
> 
> ***Happy Learning !... Keep Learning ! 😊***