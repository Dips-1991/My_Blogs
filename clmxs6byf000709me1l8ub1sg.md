---
title: "Managing Persistent Volumes in Your Deployment"
datePublished: Sun Sep 24 2023 18:16:05 GMT+0000 (Coordinated Universal Time)
cuid: clmxs6byf000709me1l8ub1sg
slug: managing-persistent-volumes-in-your-deployment
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1695579263881/976c47c6-23a5-47c2-a8f9-dc98d94a79a6.png
tags: kubernetes, kubernetes-container, kubernetes-persistent-volumes, trainwithshubham, tws

---

### ✨ ***Introduction***

***Are you struggling to keep your Kubernetes data safe and accessible?***

Are you struggling to keep your Kubernetes data safe and accessible? 🤯 Don't worry; Kubernetes has a solution for you! 🚀

In this blog post, we'll dive into the world of Persistent Volumes (PVs) in Kubernetes, explaining what they are, why they're essential, and how to use them effectively. 📦

### **📌 *What are Persistent Volumes (PVs)? 💾***

A `Persistent Volume (PV)` is an abstraction of a physical storage resource, such as a disk, that is provisioned independently from a particular pod or application.

PVs are used to provide a way to manage and abstract the underlying storage resources in a cluster. They ensure data persistence beyond the lifecycle of individual pods.

PVs define access modes (e.g., ReadWriteOnce, ReadWriteMany, ReadOnlyMany) that determine how many pods can access the volume concurrently.

PVCs are used as volume sources in pod definitions, allowing pods to access and use the storage resource associated with the PVC.

### 👇 ***Key Characteristics of PV***

1. **Provisioned Storage:** PVs are typically provisioned in advance by administrators. For example, you can create a PV using a YAML file where `pv.yml` contains the PV specification.
    
2. **Lifecycle Independence:** PVs exist until explicitly deleted, regardless of whether any Pod is using them. They persist across Pod restarts.
    
3. **Access Modes:** PVs support different access modes. Common modes include:
    
    * **ReadWriteOnce** : (can be mounted as read-write by a single node)
        
    * **ReadOnlyMany** : (can be mounted as read-only by multiple nodes)
        
    * **ReadWriteMany** : (can be mounted as read-write by multiple nodes)
        
4. **Reclaim Policies:** Administrators can define a reclaim policy, which determines what happens to the storage when the PV is released. Common policies include "Retain," "Delete," and "Recycle."
    

### **📌 *Persistent Volume Claim (PVC):***

A Persistent Volume Claim (PVC) is a request for storage by a pod or application. It defines the desired storage requirements, such as capacity and access mode.

When a PVC is created, Kubernetes attempts to bind it to an available PV that meets the PVC's requirements (e.g., capacity, access mode).

### 👇 ***Key Characteristics of PVC***

1. **Dynamic Provisioning:** PVCs can be dynamically provisioned if no matching PV with the required specifications is found.
    
2. Kubernetes will automatically create a suitable PV if dynamic provisioning is enabled for the storage class.
    
    where `pvc.yml` contains the PVC specification.
    
3. **Binding to PVs:** When a PVC is created, Kubernetes tries to bind it to a suitable PV based on its requirements (e.g., capacity, access mode, storage class). To create a binding, use the `kubectl get pvc` command to check the status:
    
4. **Lifecycle Bound to Pods:** PVCs have a lifecycle bound to the Pods that use them. When a Pod is deleted or scaled down, the PVC is also released. When the last Pod using a PVC is deleted, the PVC can either be retained (depending on the PV's reclaim policy) or deleted.
    

### ***🛠️ How to Use Persistent Volumes?***

* ### **Define a Persistent Volume**:
    
    Start by creating a Persistent Volume YAML definition file. Here's a simple example of PV.
    
* ```apache
    apiVersion: v1
    kind: PersistentVolume
    metadata:
      name: pv-todo-app
    spec:
      capacity:
        storage: 1Gi
      accessModes:
        - ReadWriteOnce
      persistentVolumeReclaimPolicy: Retain
      hostPath:
        path: "/tmp/data"
    ```
    
* **Explanation:**
    
    As of now, we know the Kubernetes YAML file very well. Here are some new things we are using below to work with PV.
    
* In the Spec
    
    * `spec`: The `spec` section defines the specifications for the PV, including its capacity, access modes, reclaim policy, and storage source.
        
    * `capacity`: This field specifies the capacity of the PV. In this example, it's set to 1 gigabyte (1Gi).
        
    * `accessModes`: It defines the access modes that pods can use to access the PV. The value `ReadWriteOnce` means that the PV can be mounted as read-write by a single node (pod) at a time.
        
    * `persistentVolumeReclaimPolicy`: This field specifies what should happen to the underlying storage resource when the PV is released by all PVCs that use it. In this case, it's set to `Retain`, which means that the data on the storage will be retained even if the PV is no longer in use.
        
    * `hostPath`: This section defines the source of the storage. In this example, it uses a host path, which means that the storage is located on the host machine running the Kubernetes cluster. The `path` field specifies the directory on the host machine where the data is stored, which is `"/tmp/data"` in this case.
        

### ***🛠️ How to Use Persistent Volumes Claim?***

* ### **Define a Persistent Volume *Claim***:
    
    Start by creating a Persistent Volume Claim YAML definition file. Here's a simple example of PVC.
    
* ```apache
    apiVersion: v1
    kind: PersistentVolumeClaim
    metadata:
      name: pvc-todo-app
    spec:
      accessModes:
        - ReadWriteOnce
      resources:
        requests:
          storage: 500Mi
    ```
    
* **Explanation:**
    
    As of now, we know the Kubernetes YAML file very well. Here are some new things we are using below to work with PVC.
    
* In the Spec
    
    * `accessModes`: It defines the access modes that pods can use to access the PVC. The value `ReadWriteOnce` means that the PVC can be mounted as read-write by a single node (pod) at a time. This is a common access mode for PVCs used by single-node applications.
        
    * `resources`: This section specifies the resource requirements for the PVC.
        
        * `requests`: It defines the requested storage resources. In this case, the PVC is requesting 500 megabytes (500Mi) of storage capacity.
            

### ✏️ ***Creating Persistent Volumes & Persistent Volumes Claim***

* To create the resource in Kubernetes use the below command.
    
    ```apache
    kubectl apply -f <pv-yaml-file>
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695574290330/2d00c9c9-52a6-4aa7-ba0e-da25e25fb80e.png align="left")
    
* To create the PVC use the below command.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695574463598/71770beb-eab3-4bf1-ba73-a74ad48f2232.png align="center")
    

### ✏️ ***Creating Deployment to use PV***

* Here is the deployment file to use the PV
    
    ```apache
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: todo-app-deployment
    spec:
      replicas: 1
      selector:
        matchLabels:
          app: todo-app
      template:
        metadata:
          labels:
            app: todo-app
        spec:
          containers:
            - name: todo-app
              image: vishalphadnis/todo-app
              ports:
                - containerPort: 8000
              volumeMounts:
                - name: todo-app-data
                  mountPath: /app
          volumes:
            - name: todo-app-data
              persistentVolumeClaim:
                claimName: pvc-todo-app
    ```
    
* **Explanation:**
    
    As of now, we know the Kubernetes YAML file very well. Here are some new things we are using below to work with PVC with Deployment.
    
    * `spec`: This section defines the specifications for the pods created by the Deployment.
        
        * `volumeMounts`: This section specifies the volume mounts for the container. It defines that a volume named `todo-app-data` should be mounted at the path `/app` within the container.
            
    * `volumes`: This section defines the volumes that can be mounted by the pods created from this template.
        
        * `name: todo-app-data`: This names the volume as `todo-app-data`.
            
        * `persistentVolumeClaim`: This specifies that the volume is backed by a `Persistent Volume Claim (PVC)` with the name `pvc-todo-app`. This means that the data stored in this volume is associated with a PVC, allowing for data persistence even if the pod is recreated or rescheduled.
            
    * ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695575997662/01f1aee9-c489-4588-8e9a-3c7a061a737f.png align="left")
        

### ✅ ***Accessing data in the Persistent Volume in POD***

* Connect to a Pod in your Deployment using the command :
    
    ```apache
    kubectl exec -it <pod-name> -- /bin/bash
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695577229248/58d87433-9efd-4a12-bb36-2f0d67ac0aae.png align="left")
    

### ✅ ***Accessing data in the Persistent Volume After Deleting POD***

* **Delete the Pod**
    
    Now we will delete the created pod and the `Replica Set` will automatically create the pod and we will check if the storage is persistent or not even if the pod is deleted
    
* To delete the pod use the below command
    
    ```apache
    kubectl delete pod <pod-name>
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695577741386/03c6dde5-1999-420d-8118-db3e05cd8b51.png align="left")
    
* **Verify In The Newly Created Pod**
    
    Log into the new pod and Verify the data is available in the newly created pod.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695578003740/680a7b11-2c01-4d06-b133-c1c634702386.png align="center")
    
* 🥇 Congratulation...🎯 Here we can see we have successfully maintained our data in the new pod even if the pod is deleted.
    

### **📝 Summary**

* Persistent Volumes (PVs) are an essential tool for managing data persistence in Kubernetes.
    
* They provide a robust and flexible way to handle storage resources, making your applications more reliable and resilient.
    
* By following the steps outlined above, you can harness the power of PVs and ensure your data remains safe and accessible in your Kubernetes cluster. 🎉Happy Kubernetting! 🚢💡