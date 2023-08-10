---
title: "Web-Application Deployment Using Nginx Web Server"
datePublished: Mon Mar 13 2023 18:42:41 GMT+0000 (Coordinated Universal Time)
cuid: clf769evk001209jucb4bemqq
slug: web-application-deployment-using-nginx-web-server
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1678732586920/b8c633a4-f7d2-4a4e-8d88-46dbfcd9623d.jpeg
tags: docker, python, django, nginx, docker-nginx

---

Overall, this project demonstrated how `Nginx Web Server` can be used to deploy web applications in a scalable, secure, and reliable manner, and how Docker can be used to package and deploy these applications with ease.

The technology stack used in this project included `Amazon EC2`, `GitHub`, `Docker`, and `Nginx`. Amazon EC2 provided the virtual server that hosted our application, GitHub allowed us to store and version control our application code, Docker allowed us to package and deploy our application in a containerized environment, and Nginx provided the web server and reverse proxy functionality.

### ***What Is a Web Server?***

A web server stores and delivers the content for a website – such as text, images, video, and application data – to clients that request it. The most common type of client is a web browser, which requests data from your website when a user clicks on a link or downloads a document on a page displayed in the browser.

A web server communicates with a web browser using the Hypertext Transfer Protocol (HTTP). The content of most web pages is encoded in Hypertext Markup Language (HTML). The content can be static (for example, text and images) or dynamic.

A web server might also cache content to speed the delivery of commonly requested content. This process is also known as *web acceleration*.

### ***What is Nginx Web Server?***

`Nginx (pronounced "engine x")` is a popular open-source web server software that is designed to handle high-traffic websites and applications. It is known for its high performance, reliability, scalability, and low resource consumption. It is a web server used for serving static web files 📂.

It is commonly used as a reverse proxy server, load balancer, indexing and HTTP cache. It can also be used as a front-end web server or as a proxy for Apache or other web servers. It also has robust security features and can be easily integrated with other tools and technologies such as SSL/TLS encryption, HTTP/2, and Docker.

### ***Nginx Architecture***

For understanding the further configuration settings of Nginx, we need to get a glimpse of Nginx understanding before that.

Nginx uses the `Master-Slave architecture`, where we have a master who reroutes our request to any of the workers under it by distributing the load on the server, then the Proxy cache is looked for faster response, else after failing to do So the webpage is loaded from the memory itself. An image demonstration will help to understand this structure more clearly.

![](https://media.geeksforgeeks.org/wp-content/uploads/20210708084058/outputonlinepngtools.png align="left")

### ***Features of Nginx***

1. **High-performance:** Nginx is designed to handle a large number of concurrent connections with low memory usage and high efficiency.
    
2. **Scalability:** It is designed to be highly scalable, allowing it to handle large volumes of traffic and requests.
    
3. **Load balancing:** Nginx can distribute incoming traffic across multiple servers, helping to balance the load and improve performance.
    
4. **Reverse proxy:** Nginx can act as a reverse proxy, enabling it to handle requests and route them to appropriate backend servers.
    
5. **Caching:** Nginx can cache content in memory or on disk, reducing the load on backend servers and improving performance for users.
    
6. **Security:** Nginx includes a variety of security features, such as SSL/TLS support, access controls, and HTTP/2 support.
    
7. **Easy to configure:** Nginx is easy to configure and can be customized to meet the specific needs of different applications.
    

Overall, Nginx is a versatile and powerful web server that can handle a variety of use cases, from small websites to large-scale applications.

### ***What is Reverse Proxy?***

In this project, we will majorly focus on the ***Reverse Proxy*** of the Nginx server

***Reverse Proxy:*** server that sits between client devices (such as web browsers) and a web server.

It receives requests from clients, processes them, and forwards them to the web server, which responds back through the reverse proxy to the client. This way, the client never directly communicates with the web server, keeping the server's true location hidden and providing additional security and performance benefits.

### ***Application Deployment Using Nginx Web Server***

***1\. Launch EC2 Instance:***

Launch an instance named with Ubuntu AMI,t2.micro instance type, and make sure to add inbound traffic rules for HTTP, and HTTPS in addition to SSH.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678709998312/78d1081c-8e58-4add-abd7-f719c3aaa49f.png align="center")

***2\. Install Nginx on the server***

To install nginx server use the following command

`sudo apt-get update` First, connect to the server and update

`sudo apt install nginx -y` Install nginx server

`nginx -v` Check the nginx version

`sudo systemctl status nginx` Check the status of nginx

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678710933770/8ba5cd4a-ff09-4568-9ea3-73e5c4040d2a.png align="center")

***3\. Check Nginx From Browser***

* To check the working status of the Nginx server, copy and paste the `Public IP` of the instance over the browser address bar.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678711289591/3a4895f7-a272-4db2-8023-a7ce8d1e86ae.png align="center")

* We can view the homepage details stored in the **index file** on its path `/var/www/html`.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678711434414/530f76ae-a131-4fa2-a525-6944480a9f77.png align="center")

* Installation and configuration files of the Nginx server can be seen at `/etc/nginx` path where
    
    * `nginx.conf` is the configuration file of the Nginx Server.
        
    * `sites-enabled` and `sites-available` are responsible for website deployment and configuration respectively.
        

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678716239923/03a0a0fd-c6b4-4249-a566-3102b40c9741.png align="center")

* To better understand the concept of static web files serving feature of the Nginx server, create another index file with different HTML codes and save it in `/var/www/html/` , default root path of the nginx server
    
* `Note:` Here, I have stopped my EC2 instance that's why the public IP address has been changed.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678719523125/efba0125-92ac-4525-86c0-c3188acafa63.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678719254542/33129925-3f4d-4d76-b621-32ec9966060f.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678719129531/9175af0c-c097-4b89-a897-689fa40362cf.png align="center")

***4\. Clone The Source Code***

Let's start the amazing part of this project by `cloning the source code` to this server using **Git**.

`sudo apt install git -y` : To Install the git on the server

`git --version` : Check the git version

`git clone [repository-url]` : To clone the source code from the repository

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678720045361/cbc20742-4c18-4afa-a6ec-883f66c3c93c.png align="center")

***5\. Install Docker on the Server***

Install docker in this server by using the following command & also check its version by the command

`sudo apt install docker.io -y` : To install docker

`docker --version` : To check the docker version

`sudo usermod -aG docker $USER` : To get the root permissions, we add the current login user to the docker group and reboot the docker service.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678721171394/3a565938-166f-44cc-b19c-5def8eb28562.png align="center")

***6\. Modify Dockerfile***

Go to the source code and modify the Dockerfile and save it.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678722503911/7f2aef25-a962-47e3-96ab-a021421d6dbb.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678722483028/882cd031-c699-4b9e-b44e-e52692ec9832.png align="center")

***7\. Build Docker Image using Dockerfile***

Build a docker image using the following command

`docker build -t [image-name] .`

`docker images` : To check the images in the docker host

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678722979999/88f4fc8c-4835-4fb4-b887-199613306852.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678723075227/1f9cf3c9-faf4-4703-859d-c20983755060.png align="center")

***8\. Run the container from the image***

Deploy the container using the following command

`docker run -d --name[container-name] -p [host-port]:[container-port> [image-name]`

`docker ps` - To check the container is running

`curl -L [local_url]:[External-Ip]` - Check the note app working over the local system.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678725867551/1a72ed17-1b3a-4fe9-bc2a-bf69afafd2ef.png align="center")

***9\. Configure Frontend using Reverse Proxy***

Run this application through the `Reverse Proxy`, not by exposing its external IP publicly on the browser. So get inside the`/etc/nginx` folder 📂 & switched to the `'sites-enabled'` a folder that is only responsible for web deployment. Edit the `default` file present inside it.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678726198591/f047218a-0228-477f-9f62-7bf3f2b66c1b.png align="center")

Here `location /` is for the frontend page of the server and we just configure (added) `proxy_pass http://127.0.0.1:8080;` as a Reverse Proxy & save it.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678726564424/21ceb9fd-2841-4b2e-9152-73fabcdb5dc8.png align="center")

Now, restart the nginx server and make sure the server is in running mode, and copy-paste the EC2 public IP address into the browser and the front-end is accessible

`sudo systemctl restart nginx.service` - To restart the nginx server.

`sudo systemctl status nginx.service` - To check nginx server status.

`[EC2-public-IP]:8080` - To load the application

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678726917203/97d8148a-96b5-4d68-aa16-370c02674bdb.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678727333940/a0d90b9e-39b6-4769-bb76-c594c42dcc7d.png align="center")

***10\. Configure Backend using Reverse Proxy***

The application is now ready but the source code is not updated in the backend to store the data. For this, copy the source code to the Nginx root folder `/var/www/html`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678727823442/68f7adc4-8117-4428-a502-6bf0b1454abc.png align="center")

Now, check backend is working at locally using the following command

`curl -L [local_url>:<external-ip]/api`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678728137318/dd437c02-8695-497b-84e8-7853b8253866.png align="center")

Here we added `location /api` for the backend page of the server.

Add `proxy_pass http://127.0.0.1:8080/api;` as a `reverse proxy` & then save it. Restart the service.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678728708685/508de551-25a3-450d-be1e-1b26781cc0c7.png align="center")

Now, restart the nginx server check the nginx status, and refresh the browser to add notes

`sudo systemctl restart nginx.service` - To restart the nginx server.

`sudo systemctl status nginx.service` - To check the nginx server status.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678729051284/0a41044e-c4bd-451e-8cf8-f87a0f56d249.png align="center")

Now, add some notes and save and check the data is reflecting as it is saved in the backend

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678729461777/59bbda6d-6182-4d65-a95f-750b62dcaf04.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678729495654/abb8bb39-6c79-449d-b9ba-d7ad249c1eb4.png align="center")

That's all our web application is deployed using the Nginx server.

***Reference:*** see this [**video**](https://www.youtube.com/watch?v=xkLQ6xzZZhU) for more details.

---

> ***Thank you for reading the article.***
> 
> ***Thanks for your valuable time.***
> 
> ***Happy Learning !... Keep Learning ! 😊***