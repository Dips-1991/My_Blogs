---
title: "🐳 Running Reddit Clone using Helm Charts inside Kubernetes Cluster☸️"
datePublished: Sat Oct 07 2023 16:57:51 GMT+0000 (Coordinated Universal Time)
cuid: clnga3s8s000109mbhzmn9vyv
slug: running-reddit-clone-using-helm-charts-inside-kubernetes-cluster
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1696697840044/0b883e78-3c0f-420c-962a-3282d1385b2e.png
tags: kubernetes, devops, helm, helm-chart, tws

---

### **Introduction**

In this blog post, we will walk you through the Helm in K8s. We will learn how we can package our Kubernetes resources and how we can deploy the application using K8's package manager Helm.

### 💼 **What is Helm in K8's?**

* Helm is a package manager for Kubernetes applications. It simplifies the process of defining, installing, and upgrading even the most complex Kubernetes applications. Essentially,
    
* Helm allows you to define your Kubernetes applications as charts.
    
* A Helm chart is a collection of pre-configured Kubernetes resources, which can be versioned, shared, and deployed as a single unit.
    
* Helm provides templating, allowing you to parameterize your Kubernetes manifests and create dynamic, reusable configurations.
    

### **🤔 Why We Need Helm?**

Helm solves several challenges in the Kubernetes deployment process:

1. **Simplified Deployment:** Helm packages Kubernetes manifests into a single unit, making it easier to manage and deploy complex applications.
    
2. **Versioning and Rollbacks:** Helm enables versioning of your applications, allowing you to roll back to previous versions if new deployments cause issues.
    
3. **Templating:** Helm's templating engine enables the dynamic generation of Kubernetes manifests, making it easy to customize deployments for different environments or use cases.
    
4. **Collaboration:** Helm charts can be shared via Helm repositories, making collaboration among developers and promoting the sharing of best practices.
    

### 🧩 **Helm Components**

Here are the components of the Helm.

* **<mark>Chart:</mark>** A Helm package that contains pre-configured Kubernetes resources.
    
* **<mark>Values.yaml:</mark>** A file where users can define customizable parameters for their charts.
    
* **<mark>Templates:</mark>** Kubernetes manifest files with Helm-specific templating.
    
* **<mark>Release:</mark>** A deployed instance of a Helm chart.
    
* **<mark>Repository:</mark>** A collection of pre-packaged charts that users can fetch from.
    

### 🏛 **Helm Architecture**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696576803413/d508e00d-6ae3-433e-a35b-f32bf10e924c.png align="center")

* As we we know we are interacting with our K8's cluster with the help of Kubectl CLI which communicates with the Kube API server and proceeds with the rest of the things.
    
* Now to work with helm command, Helm internally communicates with Kubectl CLI so that the helm chart can understand which Kubernetes cluster it is interacting with
    

### 📌 **Real-World Example**

Imagine you are managing a microservices-based application with multiple services that need to be deployed and scaled independently. Helm allows you to create charts for each service, define their dependencies, and manage their deployments as a cohesive application. When you need to update a service or roll back to a previous version due to issues, Helm simplifies the process, making your DevOps tasks more efficient and error-free.

Helm is a valuable tool in the DevOps toolbox, streamlining Kubernetes deployments and making it easier to manage complex applications in a containerized environment.

### 🛠️ **Helm Installation**

* ### 📜 **Prerequisites**
    
    **<mark>Kubernetes cluster:</mark>** You should have a Kubernetes cluster up and running.
    
* To install Helm use the below command in your system.
    
    ```apache
        curl https://baltocdn.com/helm/signing.asc | gpg --dearmor | sudo tee /usr/share/keyrings/helm.gpg > /dev/null
        sudo apt-get install apt-transport-https --yes
        echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/helm.gpg] https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
        sudo apt-get update
        sudo apt-get install helm
        helm version
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696591015035/aae9ef48-1d1a-4fd8-ad3b-ba705e02d50b.png align="center")
    

### 📄 **Basic helm command**

* <mark>Create helm chart:</mark>
    
    Create the helm chart directory with some predefined YAML files and folders like `Chart.yaml, values.yaml, templates folder, deployment.yaml, ingress.yaml, service.yaml, serviceaccount.yaml etc.`
    
    ```apache
    #helm-chart-name can be anything as per your convenient
    helm create <helm-chart-name>
    ```
    
* <mark>Install helm chart:</mark>
    
    ***Note***: The `helm install` command takes two arguments -
    
    1. First argument - Release name that you pick.
        
    2. Second argument - Chart you want to install(typically directory you created using helm create command).
        
        ```apache
        helm create <release-name> <chart-name>
        ```
        
* <mark>Helm chart list</mark>
    
    List of all installed helm charts.
    
    ```apache
    helm list -a
    ```
    
* <mark>Helm chart directory structure:</mark>
    
    Use to view helm chart directory structure after creating helm chart.
    
    ```apache
    tree <actual-chartname>
    ```
    
* <mark>Helm Upgrade:</mark>
    
    If you made any changes in the helm chart you need to upgrade your helm chart to reflect the changes.
    
    ```apache
    helm upgrade <release-name> <chart-name>
    ```
    
* <mark>Helm Rollback:</mark>
    
    If you want to switch to your previous version of the helm chart you need to use the helm rollback command.
    
    **Note:** To rollback you need to specify the revision number of the helm chart.
    
    ```apache
    helm rollback <release-name> <revision-number>
    ```
    
* <mark>Helm debug and dry-run:</mark>
    
    Use it to validate your helm chart before installation.
    
    ```apache
    helm install <release-name> --debug --dry-run <chart-name>
    ```
    
* <mark>Helm template:</mark>
    
    Renders the chart templates locally which means it validates the helm chart templates.
    
    ```apache
    #actual-helchart-name is the name of your chart 
    #which is created after hitting the helm create command
    helm templete <actual-helchart-name>
    ```
    
* <mark>Helm Lint:</mark>
    
    Use it to find any errors or misconfigurations with the helm chart.
    
    ```apache
    #actual-helchart-name is the name of your chart 
    #which is created after hitting the helm create command 
    helm lint <actual-helchart-name>
    ```
    
* <mark>Helm uninstall:</mark>
    
    Use to uninstall/remove the helm chart.
    
    ```apache
    helm uninstall <helchart-name>
    ```
    
* To know more about the helm command visit the official helm site.
    
    [https://helm.sh/docs/intro/cheatsheet/](https://helm.sh/docs/intro/cheatsheet/)
    

### **🚀 Running Reddit Clone using Helm Charts**

* **📜 <mark>Prerequisites:</mark>**
    
    * ***Kubernetes cluster:*** You should have a Kubernetes cluster up and running.
        
        ***Helm:*** Helm should be installed on your local machine.
        
* **📝<mark>Create a Helm Chart:</mark>**
    
    * First, we need to create a Helm chart to define the deployment of our application. Open your terminal and run the following command to create a Helm chart.
        
    * This command generates a directory structure for your Helm chart with default templates and values.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696600603021/c58b3091-d59d-4094-9667-78a5ff199a2f.png align="center")
        
* **📝<mark>Edit values.yaml:</mark>**
    
    * Navigate to the "node-app" directory open the `values.yaml` file and update the values as per your requirement.
        
    * **values.yaml:** This configuration specifies the number of replicas, Docker image details, and service and other specifications for your application.
        
    * <mark>Here we replace the image attribute where we will specify the repository as our docker hub image and tag and Service as a NodePort service.</mark>
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696689216894/1d8aa0f5-20ae-49ce-bc9b-05bcc7c7dfdb.png align="center")
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696692460089/9bb12dab-bf23-4234-a8c3-1f1333a50a05.png align="center")
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696689156443/49cc62a6-c4d5-462e-92eb-40da421d6d10.png align="center")
        
* 🔰 **<mark>Deploy Helm Chart:</mark>**
    
    * To deploy the Helm Chart use the command
        
        ```apache
        helm install <helm-chart-release-name> ./<actual-helm-chart-name>
        ```
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696693584102/52c2cac2-b8c7-4284-b2eb-7f423aac77ce.png align="center")
        
* ✅ **<mark>Verify Helm Chart In:</mark>**
    
    * To verify helm chart installation use the command.
        
        ```apache
        helm list -a
        ```
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696693608580/f7d3e232-90d3-4cbd-ba53-a80c62fe0c75.png align="center")
        
    * You can see our helm chart installation done successfully with Revision Number 1.
        
* ✅ **<mark>Verify the Deployment &amp; Service:</mark>**
    
    * To verify that your application has been deployed successfully, you can run the following command to list all the deployments in your cluster.
        
        ```apache
        kubectl get deployments
        kubectl get service
        kubectl get pod
        or
        kubectl get all
        ```
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696693676061/4d407e83-3d97-4259-bdac-ad78034bb439.png align="center")
        
* 🌐 **<mark>Access the Application:</mark>**
    
    * You can now access your application by visiting the URL provided by Minikube.
        
        ```apache
         minikube service <service-name> -- url
        ```
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696693945917/1cd4b79a-7256-457c-8681-0578a36acb5c.png align="center")
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696694168235/005f96e3-c389-4fa4-a8d6-be0200cd3de6.png align="center")
        
    * 🎉 **Congratulations!** You have successfully deployed a Reddit Clone Appl using Helm. Helm makes it easy to define and manage complex Kubernetes deployments, making it an essential tool for DevOps engineers working with Kubernetes.
        

### 📝 **Summary**

* In summary, Helm is essential for simplifying the management and deployment of Kubernetes applications. Its ability to package, version, template, and share applications enhances collaboration, consistency, and scalability in Kubernetes environments.
    

---

> ***Thank you🙏🙏... for taking the time to read this blog. I hope you found the information helpful and insightful. So please keep yourself updated with my latest insights and articles on DevOps 🚀 by following me on***
> 
> ***So, Stay in the loop and stay ahead in the world of DevOps!***
> 
> ***Happy Learning !... Keep Learning ! 😊***