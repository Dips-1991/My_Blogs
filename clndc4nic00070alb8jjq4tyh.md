---
title: "🚀Deploying a Reddit Clone App using Kubernetes☸️Ingress and Ingress Controllers 🌐"
datePublished: Thu Oct 05 2023 15:31:12 GMT+0000 (Coordinated Universal Time)
cuid: clndc4nic00070alb8jjq4tyh
slug: deploying-a-reddit-clone-app-using-kubernetesingress-and-ingress-controllers
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1696519435572/372dbbf5-eeb3-4dc2-b58c-59befdd8e687.jpeg
tags: kubernetes, ingress, kubernetes-container, ingress-controllers, tws

---

### **🎆 Introduction**

In a Kubernetes environment, there are many different ways to expose your application to the outside world. One of the most popular methods is through the use of a load balancer or an ingress controller. In this blog post, we will learn about what is Ingress & Ingress Controller in K8's.

Also, we will deploy the Reddit Clone application using Ingress.

![A Beginner's Guide to Ingress and Ingress Controllers in Kubernetes](https://cdn.hashnode.com/res/hashnode/image/upload/v1683609668606/c208032f-4ce3-4d5b-8dac-33cc75717199.png?w=1600&h=840&fit=crop&crop=entropy&auto=compress,format&format=webp align="left")

### **🤔 What is Ingress?**

Ingress is a Kubernetes resource that provides a way to expose HTTP and HTTPS routes from outside the cluster to services within the cluster. It acts as a reverse proxy, routing incoming traffic to the appropriate service based on the URL path and host specified in the request. In simpler terms, Ingress provides a way to manage external access to your services in a more intelligent and flexible way than a simple load balancer.

### **📍 Key features of Ingress**

* **Host-Based Routing:** Ingress allows you to route traffic based on the hostnames requested by clients. This enables hosting multiple services on the same cluster with different domain names.
    
* **Path-Based Routing:** You can route traffic based on the path of the URL requested, allowing you to direct requests to specific services based on their paths.
    
* **TLS Termination:** Ingress can also handle TLS termination, allowing you to encrypt traffic between clients and the Ingress Controller.
    
* **Custom routing:** Some Ingress Controllers allow you to define custom routing rules using middleware. Middleware allows you to add additional functionality to your Ingress rules, such as rewriting URLs or modifying headers.
    

### **🤔 What is Ingress Controller?**

An Ingress Controller is a Kubernetes resource that runs as a pod in the cluster and is responsible for implementing the rules defined in Ingress resources. In other words, the Ingress Controller is the component that handles the traffic routing based on the Ingress rules.

There are many different Ingress Controllers available for Kubernetes, each with its unique features and limitations. Some of the most popular Ingress Controllers include:

* **Nginx Ingress Controller:** A popular and versatile Ingress Controller based on the Nginx web server. It offers a wide range of features and is well-documented.
    
* **Traefik:** A modern, dynamic Ingress Controller that supports multiple backends and automatic configuration updates as Ingress resources change.
    
* **HAProxy Ingress:** Based on HAProxy, it provides advanced routing and load-balancing capabilities.
    
* **Kubernetes Native Ingress:** Starting from Kubernetes 1.19, there is also a Kubernetes Native Ingress (sometimes referred to as kube-native-ingress) that uses the Service resources as a basis for routing traffic.
    

### 💁 **How to Use Ingress and Ingress Controllers**

Here are the basic steps to set up and use Ingress and an Ingress Controller in your Kubernetes cluster:

1. **Choose an Ingress Controller:** Depending on your requirements and preferences, select an Ingress Controller that suits your needs. Install it in your cluster.
    
2. **Create Ingress Resources:** Define Ingress resources in YAML files. These resources specify routing rules, paths, hostnames, and TLS configurations. Here's a simple example:
    
    ```apache
    apiVersion: networking.k8s.io/v1
    kind: Ingress
    metadata:
      name: my-ingress
    spec:
      rules:
        - host: myapp.example.com
          http:
            paths:
              - path: /app
                pathType: Prefix
                backend:
                  service:
                    name: my-service
                    port:
                      number: 80
      tls:
        - hosts:
            - myapp.example.com
          secretName: my-tls-secret
    ```
    
3. **Apply Ingress Resources:** Use `kubectl apply` to create the Ingress resources in your cluster:
    
    ```apache
    kubectl apply -f my-ingress.yaml
    ```
    
4. **Check Ingress Status:** Verify that the Ingress Controller has applied the rules by checking the Ingress status:
    
    ```apache
    kubectl get ingress my-ingress
    ```
    
5. **Access Your Application:** Once everything is set up, you can access your application externally using the defined hostnames and paths.
    

### 🚀 **Deploying a Reddit Clone App with Ingress** 🚀

Following are the steps Deploy the Reddit clone application using K8's `Deployment, Service and Nginx Ingress controller`.

### **🛠️ Prerequisites**

First You have to install some Prerequisites for this deployment. [**Click here to set up the prerequisite**](https://trainwithshubham.hashnode.dev/prerequisite-for-deployment-of-a-reddit-copy-on-kubernetes-with-ingress-enabled).

### **🌐 Provision AWS Instances**

1. We will create the 1 `EC2 instance(Ubuntu)` with the instance type `t2.medium` as it is the minimum required to run the Kubernetes cluster.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696436567035/d7edbbfb-cc43-45fa-902a-5d0b0b3ba46c.png align="center")
    

### **📂 Clone the source code**

1. Clone the Reddit clone web application code into the machine.
    
    [https://github.com/Dips-1991/reddit-clone-k8s-ingress.git](https://github.com/Dips-1991/reddit-clone-k8s-ingress.git)
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696437567060/54203853-0a09-443c-a73f-3546194a1edd.png align="center")
    

### **🐳 Write a Dockerfile for the Project**

1. Create the Dockerfile to containerize the application using dockerfile. Here is the Dockerfile.
    
    ```apache
    FROM node:19-alpine3.15
    
    WORKDIR /reddit-clone
    
    COPY . /reddit-clone
    RUN npm install
    
    EXPOSE 3000
    CMD ["npm","run","dev"]
    ```
    

### ⚙️**Build Docker Image**

1. Build the Docker image from the Dockerfile using the following command.
    
    ```apache
    docker build -t <dockerhub-username>/<dockerhub-repo-name> .
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696438339738/84348d87-b3e6-493a-be3b-db6d84abd51b.png align="left")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696438372036/cb31cf16-8ca7-420e-a3ab-1b89bfa5340a.png align="left")
    

### 🔄**Push Docker Image to DockerHub**

1. We will push our created application image into the docker hub repository.
    
2. Make sure you have the DockerHub account created.
    
    ```apache
    docker login
    # Enter your username and password
    docker push <dockerhub-username>/<dockerhub-repo-name>:tagname
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696438924876/089f574c-fcda-4ad6-9f56-7a872230a62a.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696438979841/8ae25147-d613-4513-ad75-a8f3e8f187e6.png align="center")
    

### **✍Write a Kubernetes Manifest File**

1. **📝<mark>Create Deployment YAML:</mark>**
    
    ```apache
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: reddit-clone-deployment
      labels:
        app: reddit-clone
    spec:
      replicas: 2
      selector:
        matchLabels:
          app: reddit-clone
      template:
        metadata:
          labels:
            app: reddit-clone
        spec:
          containers:
            - name: reddit-clone
              image: deepak1603/reddit-clone-app
              ports:
                - containerPort: 3000
    ```
    
2. **📜<mark>Apply the Deployment File and Verify:</mark>**
    
    Apply the Deployment Yaml file to create the deployment, pods, and replica set.
    
    ```apache
    kubectl apply -f <deployment-yaml-file>
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696439635346/f8e3cdf7-9528-4a69-9170-4e9a49522df4.png align="left")
    
3. **📝<mark>Create Service YAML:</mark>**
    
    We need to create a NodePort Service to access our application to the outside world.
    
    ```apache
    apiVersion: v1
    kind: Service
    metadata:
      name: reddit-clone-service
      labels:
        app: reddit-clone
    spec:
      type: NodePort
      ports:
        - port: 3000
          targetPort: 3000
          nodePort: 31000
      selector:
        app: reddit-clone
    ```
    
4. **📜<mark>Apply the Service File and Verify:</mark>**
    
    Apply the Service Yaml file to create the service.
    
    ```apache
    kubectl apply -f <service-yaml-file>
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696440745402/3712636e-3fc9-4dd6-8853-0a6580cbfd64.png align="center")
    

### **🚀 Access the Application**

1. You can now access your application by visiting the URL provided by Minikube:
    
    ```apache
    minikube service <service-name> -- url
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696446228660/1d5707cd-67e0-4494-8506-7cdc64bf6fae.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696446258823/85c64bed-abb5-4fb7-ab7d-8231c0766504.png align="center")
    

### **🌍 Expose the Application to the Internet**

1. To make your application accessible from the internet, you'll need to configure port forwarding.
    
2. Run the following command for port forwarding:
    
    ```apache
    kubectl port-forward svc/<service-name> <local-machine-port>:<service-port> --address 0.0.0.0 &
    ```
    
3. Make sure port `3000` is open in your `EC2 instance security group`.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696447114956/6dde106c-c336-41a2-a573-d6f6dc561d7a.png align="center")
    
4. Copy the EC2 instance public IP address and paste in the browser along with port 3000 like `<EC2-IP>:3000`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696447052275/8038b9e7-294e-46a2-baf8-ad5e300abc99.png align="center")
    

<mark>Congratulations! </mark> 🥇🎉 You've successfully deployed a Reddit clone web app on a Kubernetes cluster hosted on AWS.

### 🎮 **Let's Configure** NGINX Ingress ⚙️

Here we will use the NGINX Ingress controller.

1. 🟢 **<mark>Enable the ingress controller:</mark>**
    
    Minikube doesn't enable ingress by default; we have to enable it first using the command.
    
    ```apache
    minikube addons enable ingress
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696512764467/75b5c3bd-7b2e-409a-9ef1-261e18199cac.png align="center")
    
2. ✅ **<mark>Verify that the NGINX Ingress controller is running:</mark>**
    
    Verify that the ingress resource is running correctly by using the command inside the `ingress-nginx namespace`.
    
    ```apache
    kubectl get pods -n ingress-nginx
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696512797068/7298b7ff-ab0b-4a37-bce9-22428031ee8b.png align="center")
    
3. **📝 <mark>Create Ingress Resources:</mark>**
    
    Define Ingress resources in YAML files. These resources specify routing rules, paths, hostnames, and TLS configurations. Here's an ingress resource file we will use for our Reddit application where we will redirect the traffic to `reddit-clone-service`:
    
    ```apache
    apiVersion: networking.k8s.io/v1
    kind: Ingress
    metadata:
      name: ingress-reddit-app
    spec:
      rules:
      - host: "domain.com"
        http:
          paths:
          - pathType: Prefix
            path: "/test"
            backend:
              service:
                name: reddit-clone-service
                port:
                  number: 3000
      - host: "*.domain.com"
        http:
          paths:
          - pathType: Prefix
            path: "/test"
            backend:
              service:
                name: reddit-clone-service
                port:
                  number: 3000
    ```
    
4. 🗒️ **<mark>Explanation:</mark>**
    
    In the ingress resource file, we have specified the rules.
    
    * `rules:`: Defines the routing rules for incoming traffic.
        
    * `host:` Routes traffic for the exact hostname "[domain.com](http://domain.com)" & Routes traffic for any subdomain of "[domain.com](http://domain.com)".
        
    * `http:`: Specifies that the routing rules are for HTTP traffic.
        
    * `paths:`: Describes the specific paths to match under this host.
        
    * `pathType: Prefix`: Indicates that the path matching should be a prefix match.
        
    * `path: "/test"`: Specifies the path prefix "/test".
        
    * `backend:`: Specifies the backend service to forward the matched traffic.
        
    * `service:`: Specifies the Kubernetes service to forward traffic to.
        
    * `name: reddit-clone-service`: Specifies the name of the Kubernetes service, which is "reddit-clone-service".
        
    * `port:`: Specifies the port of the service to which the traffic will be forwarded.
        
    * `number: 3000`: Specifies that traffic should be forwarded to port 3000 of the "reddit-clone-service".
        
5. **📜<mark>Apply the Ingress Resource File and Verify:</mark>**
    
    ```apache
    kubectl apply -f <ingress-sesource-yaml-file>
    ```
    
    Now we can see the host is `domain.com`,`*.`[`domain.com`](http://domain.com) and it routed the traffic to the Ingress IP `192.168.49.2` .
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696512989368/d9bf200b-352a-473a-b740-0b2434ad60b9.png align="center")
    

### 🔎 **Test ingress**

1. To test the application in the cluster using hostname use the command.
    
    ```apache
    curl -L domain.com/test
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696513553838/ba31e76a-6ab0-4f3d-9aea-a82ab7b5e810.png align="center")
    
    <mark>Congratulations! </mark> 🥇🎉 You've successfully deployed a Reddit clone web app on a Kubernetes cluster hosted on AWS and we are also able to access the application in a cluster with the help of `K8's Ingress and Ingress Controller` using `Hostname` which is mapped with the our `K8's Service` and it will redirect the traffic to the `Ingress IP address`.
    

### 📒 **Summary**

In summary, Ingress and Ingress Controllers are essential tools for managing external access to services in Kubernetes. They provide a flexible and powerful way to route HTTP and HTTPS traffic to your applications, making it easier to manage and scale your containerized workloads.

---

> ***Thank you🙏🙏... for taking the time to read this blog. I hope you found the information helpful and insightful. So please keep yourself updated with my latest insights and articles on DevOps 🚀 by following me on***
> 
> ***So, Stay in the loop and stay ahead in the world of DevOps!***
> 
> ***Happy Learning !... Keep Learning ! 😊***