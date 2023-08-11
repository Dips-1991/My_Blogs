---
title: "Deep Dive into Docker 🐳Networking 🔌 and Its Types"
datePublished: Fri Aug 11 2023 20:38:04 GMT+0000 (Coordinated Universal Time)
cuid: cll71vfcj000109lhausmaefq
slug: deep-dive-into-docker-networking-and-its-types
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1691785641675/0d1d83ba-1d93-4ba7-9bf0-1d96255c07bf.png
tags: devops, devops-journey, trainwithshubham, 90daysofdevops-chanllenge, dockernetworking

---

### 🚀 ***Introduction***

[Docker](https://spacelift.io/blog/docker-tutorial) is a containerization platform that uses OS-level virtualization to package software applications and their dependencies into reusable units called containers. Docker containers can be run on any host with Docker or an equivalent container runtime installed, whether locally on your laptop or in a remote cloud.

Docker includes a networking system for managing communications between containers, your Docker host, and the outside world. Several different network types are supported, facilitating a variety of common use cases.

Docker networking is a fundamental aspect of containerization that allows containers to communicate with each other, the host, and external networks. In this blog, we'll explore the different types of Docker networking, their purposes, and use cases, and provide a practical example.

### 🏢 ***Impact in Real Life***

* 📈 **Scalability:** Overlay networks enable seamless communication between backend services, even if distributed across different hosts.
    
* 🏞️ **Isolation:** Bridge networks ensure containers can communicate while being isolated from external networks.
    
* ⚡**Performance:** Host networking provides maximum throughput for the database container.
    
* 🧘**Flexibility:** Macvlan networks are ideal for scenarios where containers need unique MAC addresses.
    

### 🌐 ***Checking available networks in the system***

Here we will check the available network layer in the system using the below command

```bash
ip address show
ip link show
ip link
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691768058094/eba2dd0a-ac63-40ef-a103-425fcdf3c22c.png align="center")

Here you will see 2 by default network is showing in the system

Now after installing the docker, you can see that one more network layer is added which is `docker0` so docker is used the `docker0` network layer

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691769375213/ad817491-7639-4d47-827c-6a5af6f633dc.png align="center")

### ✍️ ***Types of Docker Networking***

Here are seven different types of Docker networks explained.

1. **Bridge Network:**
    
    * 🌉 **Description:** Default network for containers on a single host.
        
    * 🏠 **Use Case:** Applications with multiple containers needing communication within the same host.
        
    * 📌 **Key Points:**
        
        * Isolated internal network.
            
        * Containers can access each other using container names as hostnames.
            
        * Containers can't directly access the host network.
            
2. **Host Network:**
    
    * 🏠 **Description:** Containers share the host's network namespace.
        
    * 🚀 **Use Case:** Performance-critical applications needing direct access to the host network.
        
    * 📌 **Key Points:**
        
        * No network isolation between containers.
            
        * Containers use the host's network stack.
            
        * Optimal network performance.
            
3. **Overlay Network:**
    
    * 🎭 **Description:** Spans multiple Docker daemons and hosts.
        
    * 🌐 **Use Case:** Containers distributed across a cluster of machines requiring inter-host communication.
        
    * 📌 **Key Points:**
        
        * Uses the overlay driver to create networks.
            
        * Facilitates seamless communication between containers on different hosts.
            
        * Suited for microservices architectures.
            
4. **Macvlan Network:**
    
    * 🖥️ **Description:** Assigns a unique MAC address to each container.
        
    * 🏢 **Use Case:** Containers needing direct connectivity to the physical network.
        
    * 📌 **Key Points:**
        
        * Containers appear as separate physical devices on the network.
            
        * Provides a bridge between virtual and physical networks.
            
        * Enables containers to be part of VLANs.
            
5. **None Network:**
    
    * 🚫 **Description:** Containers with no network access.
        
    * 🔒 **Use Case:** Containers where network access is not needed, enhancing security.
        
    * 📌 **Key Points:**
        
        * Containers are isolated from any network.
            
        * Suitable for containers with restricted functionality.
            
6. **Custom Bridge Network:**
    
    * 🌉 **Description:** User-defined bridge network with custom configurations.
        
    * 🛠️ **Use Case:** Fine-tuned networking requirements for specific applications.
        
    * 📌 **Key Points:**
        
        * Users can create and manage their own bridge networks.
            
        * Provides more control over network settings.
            
7. **Network Aliases:**
    
    * 🔗 **Description:** Assigning multiple network aliases to a container.
        
    * 📊 **Use Case:** Running multiple services on a single container with different network identities.
        
    * 📌 **Key Points:**
        
        * Containers can have multiple virtual network interfaces.
            
        * Useful for multi-service containers without launching separate containers.
            

### 📝 **Managing Networks**

1. **Listing networks:** You can list all your Docker networks with the command:
    
    ```bash
     docker network ls
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691771174287/497e979b-9a53-4f4d-94b4-168212952585.png align="center")
    
2. **Creating a user-defined network:** You can create the custom/user define network with the command:
    
    ```bash
    docker network create <your-network-name>
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691771501443/6609589a-4885-44ae-a431-548af185579a.png align="center")
    
    You can see the new custom network is created as `my-network`
    
3. **Deleting the network:** You can delete the network with the command:
    
    ```bash
    docker network rm <your-network-name/id>
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691772122612/964acba4-bc8e-4ec9-8708-99f6bc528fc2.png align="center")
    
4. **Delete all unused networks:** You can automatically delete all unused networks using the `network prune` command:
    
    ```bash
    docker network prune
    ```
    

### 🔗 ***Connecting Containers to Networks***

You can create a new container without setting the `--network` flag then the containers will create within the default bridge network.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691773437039/f65493ce-2329-41d5-8cb7-ef947bbe955b.png align="center")

We can see the container added in the default bridge network.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691774166340/097d61bf-9ba6-4bce-9c34-f3be62e64c66.png align="center")

You can attach new containers to a network by setting the `--network` flag with your `docker run` command.

Now create your own network add attach the network to the container

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691774801568/8957bb56-f6e3-4f33-93f4-35246f44ddf3.png align="center")

After inspecting the my-network you can see the newly created container `con2` added into the custom network `my-network`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691774941965/996e238f-5783-4176-a1df-6f8aa5d502ad.png align="center")

### 📡 ***Connecting Containers to Containers***

1. **Using Different Networking:**
    
    Here we will create two Ubuntu containers `con1` in the `default bridge` network and `con2` in custom `my-network` and let's see if can we able to achieve network isolation with the help of docker networking
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691777535054/c4a7e8a2-2fa3-4cac-947e-0a1fffae69e1.png align="left")
    
    Now try communicating between the two containers, using their names/id, Enter into the container `con1` and try to connect to the container `con2`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691778945894/66b1a88c-a6ee-4726-a324-0114bbfd6f3b.png align="center")
    
    The containers aren’t in the same network yet, so they can’t directly communicate with each other.
    
2. **Using the Same Networking:**
    
    Now, Here we will create two Ubuntu containers `con3` and `con4` in same custom `my-network` , and let's see how can we achieve network isolation with the help of docker networking.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691779537203/405ca61d-cfd6-44fb-8b01-e34aa87e9ece.png align="center")
    
    Now try communicating between the two containers, using their names/id, Enter into the container `con3` and try to connect to the container `con4`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691779778294/84b0f863-6d1b-4342-8318-a467ae99777f.png align="center")
    
    Now the containers are in the same network, so they can directly communicate with each other.
    

### 💻 ***Host Networking***

Bridge networks are what you’ll most commonly use to connect your containers. Let’s also explore the capabilities of host networks, where containers attach directly to your host’s interfaces. You can enable host networking for a container by connecting it to the built-in `host` network

Here we will create `nginx web server` container in it and try to access it from the localhost

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691781658493/297a1b31-9f91-40df-a4da-f7fed9f33434.png align="center")

NGINX listens on port 80 by default. Because the container’s using a host network, you can access your NGINX server on your host’s [`localhost:80`](http://localhost:80) or in`EC2 instance IP Address` even though no ports have been explicitly exposed

***Note:*** If you are using EC2 instance make sure `port 80` should be open in the inbound rule of the EC2 instance security group

Copy the IP address of the EC2 instance and paste it into the browser you are able to see the nginx page

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691782081100/bdc7954e-cc48-4944-8411-c6e69ed4415d.png align="center")

### 🚫 ***None Networking***

When a container’s networking is disabled, it will have no connectivity available – either to other containers or your wider network. Disable networking by attaching your container to the `none` network

Here we will create a container into none network and try to ping google.com

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691782653120/c67048bf-7904-4fb6-9876-24f9b437f04b.png align="center")

### 🤦‍♀️ ***Removing Containers from Networks***

Docker lets you freely manage network connections without restarting your containers. In the previous section, you saw how to connect a container after its creation; it’s also possible to remove containers from networks they no longer need to participate in

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691784083590/1f981492-3273-4d60-86fc-5e9f3675fd8c.png align="center")

Now the container is no belongs to my-network network

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1691784185763/d9cdd962-17b7-47f1-bed7-14ede87cbc8e.png align="center")

### **🎉🔑**Conclusion:

🔗 Understanding Docker networking 🌐 and its types is crucial for designing efficient, scalable, and secure containerized applications. By leveraging the appropriate networking type for each scenario, you can optimize communication, performance, and isolation within your container ecosystem.

***Special Thanks & Reference Video @[Shubham Londhe](@TrainWithShubham)***

%[https://www.youtube.com/live/UNew_BBNVPk?feature=share] 

---

> **Thank you🙏🙏... for taking the time to read this blog. I hope you found the information helpful and insightful. So please keep yourself updated with my latest insights and articles on DevOps 🚀 by following me on**
> 
> So, Stay in the loop and stay ahead in the world of DevOps!
> 
> ***Happy Learning !... Keep Learning ! 😊***