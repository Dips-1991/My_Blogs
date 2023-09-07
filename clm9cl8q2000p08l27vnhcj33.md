---
title: "☸️Kubernetes (K8s) Architecture: A Deep Dive 🏊🏼"
datePublished: Thu Sep 07 2023 15:53:19 GMT+0000 (Coordinated Universal Time)
cuid: clm9cl8q2000p08l27vnhcj33
slug: kubernetes-k8s-architecture-a-deep-dive
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1694101828148/6424947f-eccb-4b22-8bf6-4b71361faff9.webp

---

### ☸️***What is Kubernetes?***

Kubernetes, also known as`K8s`, is an open-source system for automating the deployment, scaling, and management of containerized applications.

Originally developed at Google and released as open-source in 2014. Kubernetes builds on 15 years of running Google's containerized workloads and the valuable contributions from the open-source community. Inspired by Google’s internal cluster management system

### ***🤔Why do we call it k8s?***

The reason for using this abbreviation is primarily for convenience in written and spoken communication.

Kubernetes is a complex system with a long name, and the abbreviation `"K8s"` makes it easier to reference and discuss the platform in a more concise manner.

***👇 Here's a breakdown of the abbreviation:***

* `"K"` : Represents the first letter of `"Kubernetes."`
    
* `"8"` : Signifies the eight letters between `"K" and "s."`
    
* `"s"` : Is the last letter of `"Kubernetes."`
    

So, instead of saying or writing out the full name "Kubernetes" each time, people can simply use "K8s" to save time and effort.

### 🤷‍♀️***Benefits of using K8s***

Certainly! Here are the benefits of using Kubernetes (K8s)

* 🚀 **Scalability**: Kubernetes allows you to easily scale your applications up or down to handle changes in traffic and demand.
    
* 💡 **Portability**: Making your applications more portable across different cloud providers or on-premises environments.
    
* 🛡️ **Auto-Healing**: With features like self-healing and rolling updates, Kubernetes ensures that your applications remain available and reliable.
    
* 📦 **Container Orchestration**: It automates container deployment, management, and scaling, saving you time and effort.
    
* 🔄 **Rolling Updates**: K8s facilitates smooth, zero-downtime updates and rollbacks, reducing the risk of disruptions.
    
* 📈 **Resource Efficiency**: Kubernetes optimizes resource utilization, helping you get the most out of your infrastructure.
    
* 🌐 **Load Balancing**: Automatic load balancing ensures even distribution of traffic to your containers.
    
* 📊 **Monitoring & Scaling**: You can easily set up monitoring tools and auto-scaling based on resource utilization.
    
* 🔒 **Security**: Kubernetes offers security features like Role-Based Access Control (RBAC) and Pod Security Policies (PSP) to protect your cluster.
    
* 📜 **Logging & Tracing**: Integrations with logging and tracing solutions make debugging and monitoring easier.
    
* 🚪 **Ingress Controllers**: Manage external access to your services with Ingress controllers.
    
* 🗂️ **Persistent Storage**: Kubernetes supports persistent volumes, enabling data persistence for stateful applications.
    
* 🏷️ **Labeling & Selectors**: Labels help you organize resources, and selectors let you filter and select them efficiently.
    
* 🌌 **Cloud Controller**: You can use Kubernetes to run applications across multiple cloud providers seamlessly.
    
* 🧩 **Extensibility**: Kubernetes is highly extensible, allowing you to add custom functionality via APIs and plugins.
    
* 🌐 **Networking**: Kubernetes handles networking, making it easier to connect and route traffic between pods. `Kube proxy` is responsible for handling the networking in K8s
    
* 🎯 **Resource Isolation**: Pods provide a level of isolation for your containers, preventing conflicts.
    
* 🛰️ **Service Discovery**: Services enable easy discovery and communication between different parts of your application.
    
* 🏆 **Community & Ecosystem**: Kubernetes has a vibrant community and a vast ecosystem of tools and resources to support your projects.
    

### 🏛️ ***Architecture of Kubernetes***

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694092271150/72c0c4c9-cabd-411d-8751-b81eb91cc748.webp align="center")

Kubernetes Cluster mainly consists of Worker Machines called Nodes and a Control Plane. In a cluster, there is at least one worker node. The Kubectl CLI communicates with the Control Plane and the Control Plane manages the Worker Nodes.

* ### 🌌 Kubernetes – Cluster Architecture
    
    As can be seen in the diagram above, Kubernetes has a client-server architecture and has master and worker nodes, with the master being installed on a single Linux system and the nodes on many Linux workstations. 
    
* ### 🛠 **Kubernetes Components**
    
    **Kubernetes** is composed of a number of components, each of which plays a specific role in the overall system. These components can be divided into two categories:
    
    1. 👷‍♂️👷‍♀️ **Worker Nodes:**
        
        Each Kubernetes cluster requires at least one worker node, which is a collection of worker machines that make up the nodes where our container will be deployed.
        
    2. **Master Node (Control Plane):**
        
        The control plane is a master node that is responsible for controlling the worker node and its pods contained within it.
        
    
* ### **🧙‍♂️ Control Plane Components**
    
    It is basically a collection of various components that help us in managing the overall health of a cluster.  For example, if you want to set up new pods, destroy pods, scale pods, etc. Basically, 4 services run on the Control Plane
    
    1. 📡 **Kube-API Server**:
        
        It is like an initial gateway to the cluster that listens to updates or queries via CLI like Kubectl. Kubectl communicates with the API Server to inform what needs to be done like creating pods or deleting pods etc. It also works as a gatekeeper. It generally validates requests received and then forwards them to other processes.
        
    2. 🗄️ **Etcd**:
        
        It is a key-value store of a Cluster. The Cluster State Changes get stored in the etcd. It acts as the Cluster brain because it tells the Scheduler and other processes about which resources are available and about cluster state changes.
        
    3. 🤖 **Controller Manager**:
        
        The kube-controller-manager is responsible for running the controllers that handle the various aspects of the clusters. These controllers include the replication controller, which ensures that the desired number of replicas of a given application is running, and the node controller, which ensures that nodes are correctly marked as “ready” or “not ready” based on their current state.
        
    4. 📆 **Scheduler**:
        
        When the API Server receives a request for Scheduling Pods then the request is passed on to the Scheduler. It intelligently decides on which node to schedule the pod for better efficiency of the cluster.
        
    
* ### **👷‍♂️👷‍♀️ Worker Nodes Components**
    
    These are the nodes where the actual work happens. Each Node can have multiple pods and pods have containers running inside them. There are 3 processes in every Node that are used to Schedule and manage those pods.
    
    1. 🐳 **Container Runtime:**
        
        A container runtime is needed to run the application containers running on pods inside a pod. Example-&gt; Docker,
        
    2. 👷‍♂️**kubelet:**
        
        kubelet interacts with both the container runtime as well as the Node. It is the process responsible for starting a pod with a container inside.
        
    3. **kube-proxy:**
        
        Handles networking, and routing traffic to the right containers.
        
    4. **📦Containers:**
        
        Containers are your applications and their dependencies.
        
    5. **🌱Pods:**
        
        The smallest deployable unit! Pods can contain one or more containers, sharing the same network and storage, like best friends on an adventure!
        
    

### 👩‍💻**kubectl and kubelets**🤖

* ### 👩‍💻 **kubectl**
    
    1. ***Purpose****:* Command-line tool for managing Kubernetes clusters.
        
    2. ***User Interaction****:* Used by administrators and developers to interact with the cluster.
        
    3. ***Functionality****:*
        
        * Creates and manages Kubernetes resources.
            
        * Inspects cluster state.
            
        * Executes commands in containers.
            
    4. ***Role****:* Acts as the "commander" or "administrator" of the cluster.
        
    5. ***Typical Commands****:*
        
        * `kubectl get pods`: List pods.
            
        * `kubectl create deployment`: Create deployments.
            
        * `kubectl exec`: Execute commands in containers.
            
    6. ***Configuration****:* Requires a configuration file with cluster details.
        
    

### 🤖 **kubelets**

1. ***Purpose****:* Node-level agent responsible for managing containers on a Kubernetes node.
    
2. ***User Interaction****:* Typically operates automatically without direct user interaction.
    
3. ***Functionality****:*
    
    * Starts, stops, and monitors containers.
        
    * Mounts volumes and secrets into pods.
        
    * Reports container and pod status.
        
4. ***Role****:* Acts as the "worker" on each node.
    
5. ***Integration****:* Works with container runtimes (e.g., Docker) to manage containers.
    
6. ***Typical Actions****:*
    
    * Ensures containers in pods are running.
        
    * Monitors container health.
        
    * Manages resources for containers.
        
7. ***Configuration****:* Part of the node's configuration, controlled by cluster administrators.
    

---

> **Thank you🙏🙏... for taking the time to read this blog. I hope you found the information helpful and insightful. So please keep yourself updated with my latest insights and articles on DevOps 🚀 by following me on**
> 
> So, Stay in the loop and stay ahead in the world of DevOps!
> 
> ***Happy Learning !... Keep Learning ! 😊***