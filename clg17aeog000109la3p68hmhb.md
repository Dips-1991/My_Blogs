---
title: "Day-18 Task: Docker for DevOps Engineers(Docker-Compose): Part-3"
datePublished: Mon Apr 03 2023 19:04:32 GMT+0000 (Coordinated Universal Time)
cuid: clg17aeog000109la3p68hmhb
slug: day-18-task-docker-for-devops-engineersdocker-compose-part-3
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1680549116671/6e2a97dd-6f51-43fe-b355-2bdd2695bc98.png
tags: docker, yaml, docker-compose, docker-images, docker-network

---

### ***What* *is* *Docker?***

Docker is an open platform for developing, shipping and running applications. Docker enables you to separate your applications from your infrastructure so you can deliver software quickly. With Docker, you can manage your infrastructure in the same ways you manage your applications. By taking advantage of Docker’s methodologies for shipping, testing, and deploying code quickly, you can significantly reduce the delay between writing code and running it in production.

To learn more about docker visit the link [https://deepakcloud22.hashnode.dev/day-16-task-docker-for-devops-engineers-part-1](https://deepakcloud22.hashnode.dev/day-16-task-docker-for-devops-engineers-part-1)

### ***What* *is*** Docker Compose?

Docker Compose is a tool that was developed to help define and share multi-container applications.

With Compose, you use a YAML file to configure your application’s services. Then, with a single command, you create and start all the services from your configuration.

### ***How to Install Docker Compose?***

Visit the Docker official [site](https://docs.docker.com/compose/install/) and download the latest version of the Docker compose tool.

Here we will install the docker-compose tool in the ubuntu linux operating system.

`sudo apt-get install docker-compose -y` : To install the docker-compose tool

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680446031776/c8c776ed-7f06-4507-acda-df67955c2718.png align="center")

`sudo docker-compose --version` To check the docker-compose installed/version

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680446183130/95018a2b-207c-47c7-8315-9174896026bd.png align="center")

### ***What is YAML?***

YAML is a data serialization language that is often used for writing configuration files. Depending on whom you ask, YAML stands for `yet` `another markup language or YAML ain’t markup language` (a recursive acronym), which emphasizes that YAML is for data, not documents.

YAML is a popular programming language because it is human-readable and easy to understand.

YAML files use a .yml or .yaml extension.

### ***Task -1***

Learn how to use the docker-compose.yml file, to set up the environment, configure the services and links between different containers, and also to use environment variables in the docker-compose.yml file.

Here we will create the docker-compose file to deploy the `Wordpress` and `MySQL` containers.

**Step 1: Install docker-compose**

We have already installed the docker-compose in our system.

**Step 2: Create a docker-compose.yml file inside the project folder**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680538771392/1d1809ad-f56c-4967-bb55-b76d5e7ce968.png align="center")

* `version:"3.3"` : denotes that we are using version 3.3 of Docker Compose.
    
* `services` **:** The service section defines all the different containers we will create. In our example, we have two services, WordPress as `web01`, and MySQL as `db01` .
    
* `image` : The image keyword is used to specify the image from the docker hub for WordPress and MySQL containers.
    
* `ports` : The ports keyword is used to expose the ports of the container and the host (the left side port is the `host-port` and the right side is `container-port` )
    
* `container_name` : The container\_name is used to give the name for the containers.
    
* `volumes` : The volume keyword in the service is used to attach the volume to the containers(`wordpress:/var/www/html` and `db-vol:/var/lib/mysql`)
    
* `environment` : the environment keyword is used to set the environment variables. Here we used
    
    \- `MYSQL_USER=wordpress_user` : Mysql user.
    
    \- `MYSQL_PASSWORD=wordpress_password` : Mysql user password.
    
    \- `MYSQL_DATABASE=wordpress` : Mysql database name.
    
    \- `MYSQL_ROOT_PASSWORD="redhat"` : Mysql root password.
    
* `volumes` : This keyword is used as another volume service that will create the volumes which we attach to the containers. (`wordpress: {}` and `db-vol: {}`)
    

**Step 3: Validate the docker-compose.yml file**

`docker-compose config` : Validate the docker-compose file.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680541108643/4010c16b-42dd-4257-bcf6-f7d082557348.png align="center")

**Step 4: Run the docker-compose.yaml file**

`docker-compose up` **:** This command does the work of the docker-compose build and docker-compose run commands. It builds the images if they are not located locally and starts the containers. If images are already built, it will fork the container directly.

The `-d` flag executes the docker-compose file in the background.

`docker ps` : Lists of the running container

`docker-compose ps` : Shows lists of all the containers in the current docker-compose file.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680541813240/4e04c897-7d4e-45ca-b8b0-89dc71da7f14.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680541885724/2c3f3486-8105-4da7-9b04-dee8611c6875.png align="center")

**Step 5: Verify that the WordPress application is working by accessing it in a web browser using EC2 instance public IP address.**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680542093950/7c625223-add8-49e2-93f3-715e661b76b2.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680542547193/1284ec04-22f5-48d4-8a38-21ad202838ac.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680542665559/e8d58ca1-585e-4054-9f4d-246723882b99.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680542706542/fd51cafc-c2bf-4260-9a31-ca1b9fac9a49.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680542815315/42414094-305b-45b8-a7fa-60fd73d9d6a5.png align="center")

`docker-compose down` : This command stops all the services and cleans up the containers, networks, and images.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680543302746/03b0a686-c7b1-4b25-92af-19f748c48936.png align="center")

### *Task-2*

Pull a pre-existing Docker image from a public repository (e.g. Docker Hub) and run it on your local machine. Run the container as a non-root user (Hint- Use `usermod` command to give user permission to docker). Make sure you reboot the instance after giving permission to the user.

* Inspect the container's running processes and exposed ports using the `docker inspect` command.
    
* Use the `docker logs` command to view the container's log output.
    
* Use the `docker stop and docker start` commands to stop and start the container.
    
* Use the `docker rm` command to remove the container when you're done.
    

1\. **Pull a pre-existing Docker image from a public repository (e.g. Docker Hub) and run it on your local machine. Run the container as a non-root user.**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680546077744/0add9b51-e217-45c3-95dc-38c5b8bb7643.png align="center")

2\. Run the container as a non-root user, use the command `usermod` to give a user permission to docker and reboot the instance.

```bash
sudo usermod -a  -G docker $USER
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680546331383/8359761c-c664-47c6-9346-17cc3fc37213.png align="center")

3\. Inspect the container's running processes and exposed ports using the `docker inspect` command.

* First, deploy the container using `nginx:alpine` image using
    

`sudo docker run -d --[container-name] -p [host-port:container-port] [image-name]`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680546895831/ddf526dc-5882-4266-a4e3-949395e40d13.png align="center")

* Inspect the container's running processes and exposed ports using the docker inspect command.
    

`sudo docker inspect [container-name or container-id]`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680546970427/d1a321ea-761b-42a2-9a9e-0f86c094656d.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680547090221/4a67d66c-e005-42d8-aa68-d38dadb7fdf1.png align="center")

4\. Use the `docker logs` command to view the container's log output.

`sudo docker logs [container-name or container-id]`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680547237205/014db33e-fb6a-42fc-b479-0b201ce11515.png align="center")

5\. Use the `docker stop` and `docker start` commands to stop and start the container.

`sudo docker stop [container-name or container-id]` : Stop the running container.

`sudo docker start [container-name or container-id]` : Start the running container.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680547592022/2994b36c-7cf3-4db3-b380-e26cd11001a4.png align="center")

6\. Use the `docker rm` command to remove the container.

First, stop the container if running to remove or

Use `--force`, `-f` : Flag to remove the running container forcefully.

`sudo docker rm [container-name or container-id]`

`sudo docker rm -f [container-name or container-id]`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680547992068/0011bb1f-32cf-408e-8570-ce4dbb5901af.png align="center")

### ***How to run Docker commands without sudo?***

To run the docker command without `sudo` use the command `usermod` and reboot the instance after executing the usermod command.

```bash
sudo usermod -a  -G docker $USER
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680546331383/8359761c-c664-47c6-9346-17cc3fc37213.png align="left")

---

> ***Thank you for reading the article.***
> 
> ***Thanks for your valuable time.***
> 
> ***Happy Learning !... Keep Learning ! 😊***