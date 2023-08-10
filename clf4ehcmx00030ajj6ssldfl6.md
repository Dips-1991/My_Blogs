---
title: "Day-17 Task: Docker Project for DevOps Engineers (Dockerfile):Part-2"
datePublished: Sat Mar 11 2023 20:09:29 GMT+0000 (Coordinated Universal Time)
cuid: clf4ehcmx00030ajj6ssldfl6
slug: day-17-task-docker-project-for-devops-engineers-dockerfilepart-2
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1678565263583/1e60d98a-2926-4187-bf59-0a9dcab6de63.png
tags: docker, python, django, dockerfile, dockerize-django-application

---

### What is Dockerfile?

Docker is a tool that makes it easy to run applications in containers. Containers are like small packages that hold everything an application needs to run. To create these containers, developers use something called a Dockerfile.

A Dockerfile is like a set of instructions for making a container. It tells Docker what base image to use, what commands to run, and what files to include. For example, if you were making a container for a website, the Dockerfile might tell Docker to use an official web server image, copy the files for your website into the container, and start the web server when the container starts.

Using Dockerfile we can automate the docker image creation

### Components (Commands) of Dockerfile

Here is some command we use to create a dockerfile. Make sure all the commands should be in `capital latter`

* `FROM`: Specifies the base image that the new image will be built on top of. For example, you might use an official Node.js image as the base for an application that runs on Node.js.
    
    This command must be on top of the dockerfile.
    
* `RUN`: Executes a command in the image. This command is run during the image build process. For example, you might use the `RUN` command to install necessary packages or dependencies for your application.
    
* `MAINTAINER :` Author/Owner/Description of the dockerfile.
    
* `COPY`: Copies files from the host machine to the image. For example, you might use the `COPY` command to copy the files for your application into the image. We need to provide a source/destination.
    
* `ADD:` Similar to copy command, it provides a feature to also download files from the internet.
    
    Also, we extract files at the docker image side.
    
* `EXPOSE`: Specifies the ports that should be exposed on the container. For example, you might use the `EXPOSE` command to specify that port 8000 should be exposed on the container.
    
* `WORKDIR:` To set the working dir after the creation of the container For example.
    
* `CMD`: Specifies the command that should be run when a container is created from the image. For example, you might use the `CMD` command to specify that your application should be started when the container is created.
    
* `ENTRYPOINT:` Similar to the CMD, but has higher priority over CMD, The first command will be executed by `ENTRYPOINT` only.
    
* `ENV:` To set the Environment variables.
    

### Task

* Create a Dockerfile for a simple web application (e.g. a Node.js or Python app)
    
* Build the image using the Dockerfile and run the container
    
* Verify that the application is working as expected by accessing it in a web browser
    
* Push the image to a public or private repository (e.g. Docker Hub )
    

### Create Dockerfile

Create a Dockerfile for a simple web application (e.g. a Node.js, Static Website, or Python app)

Make sure 'D' should be capital of the Dockerfile

**Steps:**

1\. Create the `AWS EC2 instance`

2\. Make sure the docker and git should be installed. To Install the docker use the `sudo apt install docker.io -y` command and for git `sudo apt install git -y`

3\. Clone the repository from GitHub to your ubuntu server using the command

`git clone [repository_URL]`

`react_django_demo_app` app git hub link to clone [https://github.com/Dips-1991/react\_django\_demo\_app.git](https://github.com/Dips-1991/react_django_demo_app.git)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678555059692/1a87090d-9efc-4626-a9e1-07fbe9901675.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678555441931/0b3c444b-6642-4d2c-9cb6-2baea985924d.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678559599626/c3ef9ee8-5b26-4cd5-9b93-70cbe248a041.png align="center")

`FROM python:3.9` - Here, the first thing we need to do is define from which image we want to build from. Here we will use the python:3.9 image available from the Docker Hub.

`WORKDIR APP` - Here we create a directory to hold the application code inside the image, this will be the working directory for your application.

`COPY . /app` - Copy your application's code inside the Docker image folder app using COPY instruction

`RUN pip install -r requirements.txt` - This command installs all the dependencies defined in the requirements.txt file into your application within the container

`EXPOSE 8000` - This command releases port 8000 within the container, where the Django app will run

`CMD ["python","`[`manage.py`](http://manage.py)`","runserver","0.0.0.0:8000"]` - This command starts the server and runs the application

### Build Dockerfile

To build an image using Dockerfile, Go to the directory that has your Dockerfile and run the following command

`docker build -t [image-name] .`

`-t` - It indicates assigning a name tag to the image

`[image-name]` - Image name can be anything that you want to give

`.` It indicates that the Dockerfile path is the current directory or specifies your Dockerfile path

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678557484628/9d224e29-7492-4c72-ad8f-e1b244ee8fd3.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678557534586/cf2177d8-ad48-4968-97d6-a512f4254b38.png align="center")

To see the build image use `sudo docker images` command

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678557732061/6edfb434-3972-4922-b55c-647fc9dd40bc.png align="center")

### Deploy Container & Run

To create the container from the image we use `docker run`command

`docker run -it --name [container-name] -p [host-port]:[container-port] [image-name] bash`

`-it` - To create container in interactive mode(log in to the container)

`--name [container-name]` - To specify the name of the container

`-p [host-port]:[container-port]` To expose the container port through host port `(requests coming to the host port should be redirect to the container port)`

To verify the container is deployed and running use `sudo docker ps`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678560190641/48a4341d-974f-46f6-9f5e-d1fa90f14e52.png align="center")

### Verify Application

Verify that the application is working as expected by accessing it in a web browser

`http://ec2-instance-public-ip:8000`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678561996242/d16e5146-227f-4579-a325-3380de57ca8f.png align="center")

### Create Container Image

To share the container image with a public or private repository (e.g. Docker Hub ). First, we need to create the image of the container using below command

`sudo docker commit [container_name] [image_name]`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678562825984/a4801c36-b1c7-485c-bf11-9041eb675fd7.png align="center")

### Push Image To Repository

To push the image into the repository we need to use the below command

First, we need to Rename the image created using the docker commit command with your docker hub username and repo name using below command

`sudo docker tag [image_name] [dockerhub_username/repo_name]`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678563606844/ebd20ad3-31dd-4056-8686-74f662ec59ee.png align="center")

Now, we need to login to the Docker Hub very first time using below command

`sudo docker login`

And we can push the image into the Docker-hub repository using the below command

`docker push [docker-hub-username]/[image-name:[tag-name]`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678564222688/4f9f72b1-cda3-4f11-ac56-bad0b6db949c.png align="center")

Now, We can see our image is pushed into the docker hub

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678564313575/06cb0f48-4800-4a47-81b4-82154ce23577.png align="center")

---

> ***Thank you for reading the article.***
> 
> ***Thanks for your valuable time.***
> 
> ***Happy Learning !... Keep Learning ! 😊***