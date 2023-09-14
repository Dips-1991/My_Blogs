---
title: "☸️ Kubernetes ConfigMap and Secret: Unlocking Application Configuration and Secrets 🔒🔑🛡️"
datePublished: Thu Sep 14 2023 15:10:04 GMT+0000 (Coordinated Universal Time)
cuid: clmjb4l9g00000amhfj71eukh
slug: kubernetes-configmap-and-secret-unlocking-application-configuration-and-secrets
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1694704052340/1e7428ac-67e1-4f6d-8278-a902908cd0bd.png
tags: 90daysofdevops, kubernetes-configmap, kubernetes-secrets, tws, kubernetesadmin-kubernetessecurity-kubernetesbestpractices-containernetworking-kubernetesautomation-kubernetesmonitoring

---

### **Introduction**

Kubernetes is popular for its flexibility and robustness in managing containerized applications. Two vital components for achieving this are `ConfigMaps` and `Secrets`. In this blog, we'll delve into the world of ConfigMaps and Secrets.

`ConfigMaps and Secrets` in Kubernetes are essential for managing configuration data and sensitive information. Here are scenarios where you would use ConfigMaps and Secrets:

### **🧰 ConfigMaps**

ConfigMaps provides a way to store configuration data separately from your application code. They are like a treasure chest of configuration settings that your applications can access without hardcoding.

In Kubernetes, ConfigMaps and Secrets are used to store configuration data and secrets, respectively. ConfigMaps stores configuration data as key-value pairs.

In this blog, we are using the `ConfigMap and Secret` for `Mysql Database`

### **🏗️ Creating a ConfigMap**

You can create a ConfigMap using a YAML manifest file like this:

```apache
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-configmap
  namespace: mynamespace
data:
  MYSQL_DB: "mydb"
```

**Explanation**:

* As of now, we know about the `Manifest YAML` file and its attributes
    
* Here the new thing is `data:.`
    
* `data`: This is where you define `key-value` pairs for your configuration settings. In this example, we have 1 key-value pairs: `MYSQL_DB`.
    

### **✍ Using a ConfigMap in a Pod**

Here's a YAML manifest file for creating a Pod that uses the ConfigMap `my-configmap`:

```apache
  apiVersion: apps/v1
  kind: Deployment
  metadata:
    name: mysql-configuration
    namespace: mynamespace
    labels:
        app: mysql
  spec:
    replicas: 1
    selector:
      matchLabels:
        app: mysql
    template:
      metadata:
      namespace: mynamespace
        labels:
          app: mysql
      spec:
         containers:
         - name: mysql-container
           image: mysql:8
           ports:
           - containerPort: 3306
           env:
           - name: MYSQL_DATABASE
             valueFrom:
               configMapKeyRef:
                 name: my-configmap
                 key: MYSQL_DB
```

**Explanation**:

* In the `env` section, we define environment variables. For this `MYSQL_DATABASE`, we set its value using a reference to the `my-configmap` ConfigMap. This is done via `configMapKeyRef`, where we specify the `name` of the ConfigMap and the `key` we want to use. This way, the value of `MYSQL_DB` in the ConfigMap is injected as an environment variable into the container.
    

### **🔐Secrets:**

Secrets are akin to ConfigMaps but are designed specifically for sensitive data, such as passwords, API keys, or TLS certificates. They provide an additional layer of security for critical information.

### **🏗️ Creating a Secret**

Here's a YAML manifest file for creating a Secret named `my-secret`:

Before that, we are passing the password value into the data field in base64 encrypted format so let's make the password base64 encrypted.

```apache
 echo -n 'dipak@123' | base64
 # ZGlwYWtAMTIz
 echo -n 'ZGlwYWtAMTIz' | base64 --decode
 #dipak@123
```

```apache
  apiVersion: v1
  kind: Secret
  metadata:
    namespace: mynamespace   
    name: my-secret
  type: Opaque
  data:
    password: ZGlwYWtAMTIz
```

**Explanation**:

* type: Hre we use an `opaque secret`, allows for unstructured `key:value` pairs that can contain arbitrary values.
    
* `data`: This is where you define `key-value` pairs for your configuration settings. In this example, we have 1 key-value pairs: `password` in a base64 encrypted format.
    

### **✍ Using a Secret in a Pod**

We have our Deployment file just add the new env variable attach the secret there and update the Deployment file.

```apache
  apiVersion: apps/v1
  kind: Deployment
  metadata:
    name: mysql-configuration
    namespace: mynamespace  
    labels:
      app: mysql
  spec:
     replicas: 1
     selector:
       matchLabels:
         app: mysql
     template:
       metadata:
         namespace: mynamespace
         labels:
           app: mysql
       spec:
         containers:
         - name: mysql-container
           image: mysql:8
           ports:
           - containerPort: 3306
           env:
           - name: MYSQL_DATABASE
             valueFrom:
               configMapKeyRef:
                 name: my-configmap
                 key: MYSQL_DB
           - name: MYSQL_ROOT_PASSWORD
             valueFrom:
               secretKeyRef:
                 name: my-secret
                 key: password
```

### 🧾 **Applying ConfigMap & Secret**

Run the below command to create the required`(ConfigMap, Secret, Deployment)` object.

```apache
kubectl apply -f <file-name>
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694702194175/a71c3093-c394-4718-9cbb-c5f482113615.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694695256620/d30a5b9f-5f00-4999-9006-43953a53ee02.png align="center")

Login Into the container running inside the Pod using the command.

`kubectl exec -n <namespace here> <pod-name> -c <container-name> -it -- /bin/sh`

Once you log in to the container you are inside the container then login to the MySQL database running inside the container using the command.

```apache
mysql -u root -p <your-decrepted password>
```

Then hit the command to show the database we have specified in the ConnfigMap file.

```apache
show databases;
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694703704183/8202fbe0-2d52-4154-bbbe-a6709532ea39.png align="center")

### **📝Summary**

* **ConfigMaps** (🧰) store configuration data and are excellent for decoupling configuration from application code.
    
* **Secrets** (🔐) secure sensitive information and are indispensable for safeguarding credentials and certificates.
    

ConfigMaps and Secrets are like the keys to unlocking the full potential of your Kubernetes applications. Use them wisely to streamline configuration management and secure your sensitive data. 🌟

---

> **Thank you🙏🙏... for taking the time to read this blog. I hope you found the information helpful and insightful. So please keep yourself updated with my latest insights and articles on DevOps 🚀 by following me on**
> 
> So, Stay in the loop and stay ahead in the world of DevOps!
> 
> ***Happy Learning !... Keep Learning ! 😊***