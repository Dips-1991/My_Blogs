---
title: "Services in Kubernetes: A Deep Dive"
datePublished: Thu Sep 14 2023 06:23:00 GMT+0000 (Coordinated Universal Time)
cuid: clmisarjj000309ldafyx7ql0
slug: services-in-kubernetes-a-deep-dive
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1694672472479/7de75207-df6a-4e25-8de7-3d21cfabbf4b.webp
tags: 90daysofdevops-chanllenge, tws, kubernetesnetworking, kubernetesservice, trainwithshubham-techwithankush-seekhoaursikhao-twscommunitybuilders-90daysofdevops-connections-growth-community-learning-linkedin-devops-awsdevops-awscloud-awscommunity-aws-docker-dockercontainer-dockerhub-kubernetescluster-kubernetesservices-kubernetes-jenkins-ansible-ansibleautomates-linuxsystemadministration-linuxfoundation-linux-git-github-terraform-grafana-prometheus-cicd-cicdpipelines

---

### **Introduction**

Kubernetes is the powerhouse of container orchestration. One of the essential building blocks of Kubernetes is `Services.` In this blog, we'll unravel the magic of `Kubernetes Services`.💥🙌

### **🤔 What Problems Do Kubernetes Services Solve?**

* In Kubernetes, Pods are non-permanent resources - they can appear and disappear as needed. This is because Kubernetes constantly checks to make sure the cluster is running the desired number of replicas (copies) of your app. And Pods are created or destroyed to match this desired state.
    
* If a Pod fails for some reason, no worries - Kubernetes will quickly create a new one to replace it. And if you want to update your app, Kubernetes can destroy old Pods and create new ones with the updated code. So **the set of Pods running at one moment could be totally different from the set running a moment later.**
    
* But here's the thing - if you want to access your app, how do you keep track of which Pod to connect to with all these changing IP addresses of Pods?
    
* Because every time the new IP address is assigned to a pod or newly created pod.
    
* That's where Services come in. They provide an unchanging location for a group of Pods. So even though the Pods themselves are dynamic, the Services make sure you always have a central location to access your app.
    
* The service object is a logical bridge between the pod and end users, which provides `Virtual IP (VP).`
    
* The service allows users to connect to the containers running inside pods using `Virtual IP`.
    

### **🌟Types of Kubernetes Services**

Let's explore the different types of Kubernetes Services

* **ClusterIP Service**
    
* **NodePort Service**
    
* **LoadBalancer Service**
    

### 🌐 **ClusterIP Service**

* ClusterIP Services are used for communication between Pods within the same Kubernetes cluster.
    
* The Service gets exposed on a static IP/virtual IP that's unique within the cluster. When you make a request to that IP, the Service takes care of redirecting traffic to one of the Pods it's associated with.
    
* And if there's more than one Pod, the Service will automatically balance the traffic.
    
* ***Note that ClusterIP Services are meant for Pod-to-Pod communication only. They aren't accessible from outside the cluster.***
    

### 💡Example: **ClusterIP Service**

* Create a `ClusterIP Service` definition for your `httpd`Deployment in a YAML file.
    
    ```apache
    # Defines to create Service type Object      
    apiVersion: v1
    kind: Service
    metadata:
      name: httpd-service
      namespace: httpd-namespace
    spec:
      ports:
        - port: 80                 # Containers port exposed                       
          targetPort: 80           # Pods port                     
      selector:
        name: deployment           # Apply this service to any pods which has the specific label "deployment"
      type: ClusterIP              # Specifies the service type i.e ClusterIP or NodePort
    ```
    
* Create a `Deployment` definition for your `Nginx` Deployment in a YAML file.
    
    ```apache
     apiVersion: apps/v1
     kind: Deployment
     metadata:
        name: httpd-deployments
        namespace: httpd-namespace
     spec:
        replicas: 2
        selector:      # tells the controller which pods to watch/belong to
         matchLabels:
          name: deployment
        template:
          metadata:
            namespace: httpd-namespace
            name: httpd-pod
            labels:
              name: deployment
          spec:
           containers:
             - name: httpd-container
               image: httpd
               ports:
               - containerPort: 80
    ```
    
* Apply the ClusterIP Service definition to your K8s (Minikube) cluster using
    
    the `kubectl apply -f cluster-ip-service.yml` command.
    
* Create the namespace if not created using `kubectl create namespace <namespace-name>` command.
    
* Apply the Deployment definition to your K8s (Minikube) cluster using
    
    the `kubectl apply -f cluster-ip-deployment.yml` command.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694664146586/0c945592-f690-4882-824e-a8fb09a6a7f9.png align="center")
    
* We can see here once the `service` is created the and Virtual IP `10.107.249.160` is assigned to the `cluster` as `CLUSTER-IP` by `Kube-proxy`.
    
* Our `Deployment` and `2 Pods` were also created successfully.
    
* Verify that the ClusterIP Service is working by accessing the `httpd` from the
    
    login to any of the pods using the command `kubectl exec -n <namespace> -it <pod_name> — /bin/bash` .
    
* Copy the `Cluster IP` and type `curl <cluster-ip>:80` .
    
* If curl does not install after login into the pod.
    
* use `apt install curl -y`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694664547502/7f0bfe77-c8c1-4a01-917d-0b7dd4d410ff.png align="center")
    
* Now delete the created pod and test the same things again and see what happens.
    
* Once we have deleted the pod the new pod is created automatically because we have used `Deployment` it for creating the pod and `Replica Set` maintaining the `Desired state` (1 which we have set in Deployment) of the pod and auto-healing.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694664833778/8640d5a5-7836-45f4-9855-ef838cd9767b.png align="center")
    
* `Conclusion:` Even if we delete the pod the new pod is created and the IP address of the pod also changed, and still, we are able to access the application using the `K8s ClusterIP service`.
    

### 🌐 **NodePort Service**

* The NodePort Service is useful when you need to **expose your application to external clients**. This means all traffic that is coming from **outside of the cluster**.
    
* When you create a NodePort Service, Kubernetes opens a port `(in the range of 30000 and 32767)` on all of its worker nodes.
    
* **Note that the same port number is used across all of them. All traffic incoming to the worker node's IP address, and that specific port, is redirected to a Pod linked with that Service.**
    
* You can contact the NodePort Service, from outside the cluster, by requesting : `<NodeIP>:<NodePort>` .
    

### 💡 Example: NodePort Service Service

* Create a `NodePort Service` definition for your `httpd`Deployment in a YAML file.
    
* **Here we have to make some modifications- in** `type`**, we have mentioned the** `types` **as** `NodePort` and the Second thing is we also need to add `nodePort` in `ports` section.
    
* `nodePort:` **Tells Kubernetes which port to** `"open"` **to the** `outside world` **on all of the worker nodes. This makes them accept incoming connections, from outside the cluster, on the port we chose here, 30003. If not specified Kubernetes will automatically assign a port** `(in the range of 30000 and 32767).`
    
    ```apache
    # Defines to create Service type Object (in the range of 30000 and 32767)     
    apiVersion: v1
    kind: Service
    metadata:
      name: httpd-service
      namespace: httpd-namespace
    spec:
      ports:
        - port: 80                # Containers port exposed                       
          targetPort: 80          # Pods port
          nodePort: 30008
             # "open" to the outside world                     
      selector:
        name: deployment          # Apply this service to any pods which has the specific label "deployment"
      type: NodePort              # Specifies the service type i.e ClusterIP or NodePort
    ```
    
* Create a `Deployment` definition for your `httpd` Deployment in a YAML file. (The Deployment YAML file is the same one we have used in an earlier service).
    
    ```apache
     apiVersion: apps/v1
     kind: Deployment
     metadata:
        name: httpd-deployments
        namespace: httpd-namespace
     spec:
        replicas: 1
        selector:      # tells the controller which pods to watch/belong to
         matchLabels:
          name: deployment
        template:
          metadata:
            namespace: httpd-namespace
            name: httpd-pod
            labels:
              name: deployment
          spec:
           containers:
             - name: httpd-container
               image: httpd
               ports:
               - containerPort: 80
    ```
    
* Apply the ClusterIP Service definition to your K8s (Minikube) cluster using
    
    the `kubectl apply -f node-port-service.yml` command.
    
* Create the namespace if not created using `kubectl create namespace <namespace-name>` command.
    
* Apply the Deployment definition to your K8s (Minikube) cluster using
    
    the `kubectl apply -f node-port-deployment.yml` command.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694665303945/79e51c05-b47d-4b76-a42c-1424a5d84bba.png align="center")
    
* As we know once the `service` is created the and Virtual IP `10.101.155.129` is assigned to the `cluster` as `CLUSTER-IP` by `Kube-proxy`.
    
* And the `PORT` is also open `30003` to access the application outside the cluster.
    
* You can now access your application within a cluster by visiting the URL provided by Minikube:
    
    `minikube service <servicename> -n <namespace> created --url`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694665723323/59724dfb-7bb1-44ad-a465-173c97003c10.png align="center")
    
* To make your application accessible from the `Internet(browser)`, you'll need to `Expose the Deployment and configure Port Forwarding`.
    
* ***Why Port Forwarding?***: While NodePort services expose your service to external traffic, you may also need to access the service directly from your local machine, especially during development, debugging, or testing. Port forwarding allows you to do just that.
    
* ***Exposing a NodePort Service****:*
    
    Exposing a NodePort service makes your application accessible from outside the Kubernetes cluster. NodePort services allocate a specific port on each node in the cluster, making it available for external access.
    
    `kubectl expose deployment <deployment-name> -n <namespace-name> --type=NodePort`
    
    `kubectl port-forward svc/<service-name> -n <namespace-name> <local-port>:<pod-port> --address 0.0.0.0`
    
* Make sure the `NodePort(30003)` is open in your `Security Group` of the `EC2` instance.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694666835729/bf9012f9-ad57-4a28-9894-b4d204f82a02.png align="center")
    
* Now copy your EC2 instance Public IP address and enter it into the browser
    
    `<EC2 instance Public IP>:<your-forwared-port>`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694666773677/a9d57701-67a4-4c55-b533-e0b73965fbc0.png align="center")
    

### 🌐 **LoadBalancer Service**

* A LoadBalancer Service is another way you can **expose your application to external clients**. However, **it only works when you're using Kubernetes on a cloud platform(AWS, GCP, Azure ....) that supports this Service type.**
    
* The LoadBalancer Service detects the cloud computing platform on which the cluster is running and creates an appropriate load balancer in the cloud provider’s infrastructure.
    

### 💡 Example: LoadBalancer Service

* Create a `LoadBalancer Service` definition for your `httpd`Deployment in a YAML file.
    
* **Here we have to make some modifications- in** `type`**, we have mentioned the** `types` **as** `LoadBalancer`
    
    ```apache
    # Defines to create Service type Object      
    apiVersion: v1
    kind: Service
    metadata:
      name: httpd-service
      namespace: httpd-namespace
    spec:
      ports:
        - port: 80                # Containers port exposed                       
          targetPort: 80          # Pods port
          nodePort: 30008
             # "open" to the outside world                     
      selector:
        name: deployment          # Apply this service to any pods which has the specific label "deployment"
      type: LoadBalancer              # Specifies the service type i.e ClusterIP or NodePort
    ```
    
* Create a `Deployment` definition for your `httpd` Deployment in a YAML file. (The Deployment YAML file is the same one we have used in an earlier service)
    
    ```apache
     apiVersion: apps/v1
     kind: Deployment
     metadata:
        name: httpd-deployments
        namespace: httpd-namespace
     spec:
        replicas: 2
        selector:      # tells the controller which pods to watch/belong to
         matchLabels:
          name: deployment
        template:
          metadata:
            namespace: httpd-namespace
            name: httpd-pod
            labels:
              name: deployment
          spec:
           containers:
             - name: httpd-container
               image: httpd
               ports:
               - containerPort: 80
    ```
    
* Apply the ClusterIP Service definition to your K8s (Minikube) cluster using
    
    the `kubectl apply -f load-balancer-service.yml` command.
    
* Create the namespace if not created using `kubectl create namespace <namespace-name>` command.
    
* Apply the Deployment definition to your K8s (Minikube) cluster using
    
    the `kubectl apply -f load-balancer-deployment.yml` command.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694668086010/d7f1b521-4565-4694-b302-a90a18a529da.png align="center")
    
* You can see here the `ClusterIP` service also created on top of that `NodePort` service also created and on top of that `LoadBalancer` service was also created and the `EXTERNAL-IP` is pending.
    
* **The type is**  `LoadBalancer`**, but its**  `EXTERNAL-IP`**status is**  `Pending` **since Minikube does not have a service with the LoadBalancer type, because it must be created at the infrastructure level – AWS, GCE, Azure, and then Kubernetes receives an IP or URL from them to route requests to this load balancer.**
    

## **📚 Takeaways**

* `ClusterIP` for internal communication between pods.
    
* `NodePort` for exposing applications externally during development.
    
* `LoadBalancer` for public-facing, production-grade services.
    

In Kubernetes, Services are the linchpin of networking. They ensure seamless communication within your cluster and beyond. By choosing the right type of Service, you can connect your applications reliably and securely, helping your containerized journey take flight.

---

> **Thank you🙏🙏... for taking the time to read this blog. I hope you found the information helpful and insightful. So please keep yourself updated with my latest insights and articles on DevOps 🚀 by following me on**
> 
> So, Stay in the loop and stay ahead in the world of DevOps!
> 
> ***Happy Learning !... Keep Learning ! 😊***