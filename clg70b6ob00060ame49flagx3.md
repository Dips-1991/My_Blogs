---
title: "Day-20: Docker Commands Cheat-sheet"
datePublished: Fri Apr 07 2023 20:35:48 GMT+0000 (Coordinated Universal Time)
cuid: clg70b6ob00060ame49flagx3
slug: day-20-docker-commands-cheat-sheet
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1680899647056/a201bcb4-26b1-406c-9f13-9cc58aa2cfc6.jpeg
tags: dockerfile, docker-compose, docker-images, docker-container, dockercommands

---

Now it's time to take your Docker skills to the next level by creating a comprehensive cheat-sheet of all the commands you've learned so far. This cheat-sheet should include commands for Docker, Dockerfile, Docker-Compose, Docker Volume as well as brief explanations of their usage. This cheat-sheet will not only help you in the future but also contribute to the DevOps community by providing a useful resource for others.😊🙌

### ***Basic Commands***

1. `sudo apt install docker.io` : To install docker
    
2. `docker -v / --version` : Shows the installed docker version
    
3. `systemctl start docker / service docker start` : Start docker service
    
4. `systemctl stop docker / service docker stop`: Stop the docker service
    
5. `systemctl status docker / service docker status`: Check the docker service status
    
6. `docker ps` : Lists only running containers
    
7. `docker ps -a` : Shows all containers including created, running, and exited.
    
8. `docker images -a` : Lists all images created
    
9. `docker logs` : Shows the logs of the container
    
10. `docker inspect [container-name/image/volume]`: View detail information about an image, container, volume
    
11. `docker stats` : View resource usage statistics for one or more containers
    
12. `docker port` : List the port mappings for a container
    
13. `docker top` : To view the processes inside a container
    

### ***Manage images and containers - Commands***

1. `docker pull [username/repository:tag]` : Download images from registry or
    
    `docker pull [image-name]`
    
2. `docker build -t [tagname/new-image-name] [directory/]` : Build a new docker image from Docker file
    
3. `docker run [image]` : Starts a new container from an image
    
4. `docker run --name [container] [image]` : Start new container and assign a name of container
    
5. `docker run -d [image]` : Starts a new container in backend
    
6. `docker run -p [Hostport]:[container-port] [image]` : Start new container with map ports to container
    
7. `docker run -it [image]` : Start new container in interactive mode(`Login to the container`)with the image through command line
    
8. `docker run -e [myvar=myprop] [image]` : Specify an environmental variable for a docker container
    
9. `docker exec -it [container-ID/name] [executable]` : Start a shell or entering inside a running container or log in to the running container
    
10. `docker rename [oldname] [newname]` : Rename the container
    
11. `docker save [image] > [archivefile]` or
    
    `docker save -o [archivefile] [image]` : Save an image to a tar archive
    
12. `docker commit [container-name] [imagename]` : Create an image of docker container
    
13. `docker load -i [archivefile]` : Load an image to a tar archive
    
14. `docker kill [container]` : Forced shutdown of running container
    
15. `docker rm [container-name/id]` : Delete the stop container
    
16. `docker rm -f [container-name/id]` : Delete the running container
    
17. `docker rm $(docker ps -a -q)` : Delete all running container
    
18. `docker rmi [image]` : Delete a docker image
    
19. `docker rmi $(docker images -q)` : Delete all docker images
    
20. `docker system prune` : Delete all dangling containers, unused images and containers
    
21. `docker login` : Login cli session with registry like Dockerhub using credentials
    
    It will ask to enter the username and password
    
22. `docker remote -v` : Lists out remote docker host
    
23. `docker tag [image] [registry-username/repository:tag]` : Set the tag for images pushed to Dockerhub
    
24. `docker push [registry-username/repository:tag]` : Upload images to registry
    

### ***Docker-Compose & Volumes -Commands***

1. `docker-compose config` : Validate the docker-compose file
    
2. `docker-compose up -d`: Start multiple containers at once in background from the docker-compose file
    
3. `docker-compose ps` : Lists running containre created from docker-compose file
    
4. `docker-compose ps -a` : Lists all running and stoped containre created from docker-compose file
    
5. `docker-compose down` : Stop all running containers and also remove them
    
6. `docker compose logs` : Shows the logs of running containers with docker compose
    
7. `docker compose -d --scale up [service]=[no. of times]` : Scale up the services or containers with limited times as prescribed in yaml file
    
8. `docker service [service] --replicas [no. of times] [image]`: Autoscaling services with set number of times
    
9. `docker volume ls` : Lists all volumes
    
10. `docker volume create [volume]` : Create a volume in the machine
    
11. `docker run -v [HostDir:TargetDir] -it [container] [image]` : Create and connect a container to a volume or mapping local directory with a docker container
    
12. `docker volume rm [volume]` : Delete unused volume from machine
    
13. `docker volume prune` : Delete all the available docker volumes
    
14. `docker volume inspect [volume-name]` : Inspects the volume (Detailed information about volume)
    

---

> ***Thank you for reading the article.***
> 
> ***Thanks for your valuable time.***
> 
> ***Happy Learning !... Keep Learning ! 😊***