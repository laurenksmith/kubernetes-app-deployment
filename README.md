# Use Kubernetes for 2-Tier App Deployment

- [Use Kubernetes for 2-Tier App Deployment](#use-kubernetes-for-2-tier-app-deployment)
  - [Overview](#overview)
  - [Research](#research)
    - [Why Kubernetes is Needed](#why-kubernetes-is-needed)
    - [Benefits of Kubernetes](#benefits-of-kubernetes)
    - [Success Stories](#success-stories)
    - [Kubernetes Architecture](#kubernetes-architecture)
    - [The Cluster Setup](#the-cluster-setup)
      - [What is a Cluster?](#what-is-a-cluster)
      - [Master vs Worker Nodes](#master-vs-worker-nodes)
      - [Pros and Cons of Using Managed Service vs Launching Your Own](#pros-and-cons-of-using-managed-service-vs-launching-your-own)
      - [Control Plane vs Data Plane](#control-plane-vs-data-plane)
    - [Kubernetes Objects](#kubernetes-objects)
      - [Most Common Kubernetes Objects](#most-common-kubernetes-objects)
      - [Ephemeral Pods](#ephemeral-pods)
    - [How to Mitigate Security Concerns with Containers](#how-to-mitigate-security-concerns-with-containers)
    - [Maintained Images](#maintained-images)
      - [What They Are](#what-they-are)
      - [Pros and Cons of Using Maintained Images for Your Base Container Images](#pros-and-cons-of-using-maintained-images-for-your-base-container-images)
  - [Create and Test Nginx Deployment with NodePort Service](#create-and-test-nginx-deployment-with-nodeport-service)
    - [What I Did](#what-i-did)
    - [Why This Step Matters](#why-this-step-matters)
  - [Websites Used](#websites-used)
    - [Understanding Kubernetes](#understanding-kubernetes)
    - [Kubernetes Architecture](#kubernetes-architecture-1)

## Overview

## Research

### Why Kubernetes is Needed
As applications grow and become more complex, running them across multiple servers manually becomes difficult to manage. Kubernetes solves this by automating deployment, scaling, and management of containerised applications. It ensures that applications run reliably, even when there are hardware failures or traffic spikes. Essentially, it removes much of the manual work involved in keeping systems running smoothly, making deployments faster, more consistent, and easier to control at scale.

### Benefits of Kubernetes
- **Scalability**: Kubernetes can automatically increase or decrease the number of containers running depending on demand.

- **Self-healing**: If a container fails or a node goes down, Kubernetes detects it and replaces it automatically.

- **Portability**: It works the same way across different environments – from a laptop to cloud platforms such as AWS, Azure, or GCP.

- **Resource efficiency**: Kubernetes schedules workloads in a way that makes the best use of available resources.

- **Automation**: Updates, rollbacks, and configuration changes can be managed automatically without downtime.

- **Consistency**: Teams can deploy applications in the same way everywhere, avoiding “it works on my machine” issues!
  
### Success Stories
- **Spotify**:
<br> Spotify uses Kubernetes to manage THOUSANDS of backend services which support its music streaming platform. This improves their scalability as well as the deployment speed.
- **NASA**:
<br> NASA adopted Kubernetes to process massive amounts of space mission data efficiently, and reliably.
- **The New York Times**:
<br> The NY Times migrated its entire digital archive to Kubernetes. This made it easier for them to scale and maintain their content services.

### Kubernetes Architecture
The Kubernetes architecture follows a control-plane and data-plane model.
The Control Plane is responsible for managing the overall state of the cluster — deciding what should run and maintaining the desired configuration. It includes components such as the API Server, etcd (cluster database), Scheduler, and Controller Manager.
The Data Plane consists of the worker nodes that actually run the application workloads. Each node runs a kubelet (which manages containers on that node) and a kube-proxy (which handles networking).

The diagram below shows the key components of a Kubernetes cluster and how they interact:

![alt text](images/Kubernetes-cluster.png)

**Brief explanation of each component in the above diagram**:<br>
1. api = Api Server. Entry point for all communication
2. etcd = Persistance Store. Stores the cluster's state and configuration
3. sched = Scheduler. Decides where pods should run
4. c-m = Controller Manager. Ensures system health and restarts pods if needed
5. c-c-m = Cloud Controller Manager. Integrates with external cloud providers
6. Kubelet. Ensures containers are running properly
7. k-proxy = Kube-Proxy. Routes network traffic between pods and services


This design allows Kubernetes to balance control and automation — the control plane handles decisions and coordination, while the data plane performs the work of running containers.

### The Cluster Setup

#### What is a Cluster?
A Kubernetes cluster is a group of physical or virtual machines that operate together as one system to run and manage containerised applications.
It’s made up of a control plane, which oversees and coordinates the cluster, and a set of worker nodes, where the applications themselves run.
This architecture is what allows Kubernetes to handle important operational tasks — such as scheduling, scaling, and updates — automatically and consistently.

#### Master vs Worker Nodes
A Kubernetes cluster is made up of two main types of nodes:
- **Control Plane Nodes** (formerly known as Master Nodes) – These manage and coordinate the cluster. They handle scheduling, scaling, and monitoring, and maintain the desired state of the system.
- **Worker Nodes** – These run the actual applications and services. Each worker node contains the necessary components to host containers and communicate with the control plane.

Together, the control plane nodes provide intelligence and decision-making, while the worker nodes provide the computing power.
  
#### Pros and Cons of Using Managed Service vs Launching Your Own
| Approach                                            | Pros                                                                                                                                                                      | Cons                                                                                                                               |
| --------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| **Managed Service (e.g., AWS EKS, Azure AKS, GKE)** | - Easy setup and maintenance (cloud provider manages updates and control plane).<br>- Integrated security and monitoring tools.<br>- Scales easily with less manual work. | - Can be more expensive long-term.<br>- Less control over underlying infrastructure.<br>- Dependent on provider’s update schedule. |
| **Self-Managed (Launch Your Own)**                  | - Full control and customisation of setup.<br>- Can be cost-effective for small or on-prem clusters.<br>- Good for learning and experimentation.                          | - Requires more hands-on management and troubleshooting.<br>- Responsibility for updates, security patches, and scaling.           |

#### Control Plane vs Data Plane
- **Control Plane**: The brain of the cluster — it makes global decisions such as scheduling, scaling, and monitoring the overall state. It includes the API Server, Scheduler, Controller Manager, and etcd database.
- **Data Plane**: The muscle of the cluster — this is where the applications actually run. It consists of worker nodes, each with a kubelet and kube-proxy.

### Kubernetes Objects
Kubernetes represents everything it manages as an object.
An object is simply a record of your intended state for a part of the system — for example, which containers should be running, how many replicas you want, or how to expose an application.
When you apply a YAML manifest, Kubernetes reads it as an object definition and ensures the system matches it.

#### Most Common Kubernetes Objects
- **Pod**: The smallest deployable unit — usually one or more containers that share storage, network, and configuration.
- **ReplicaSet**: Ensures the correct number of Pod replicas are running at any time.
- **Deployment**: A higher-level object that manages ReplicaSets and provides rolling updates and rollbacks.
- **Service**: Exposes Pods internally or externally so other parts of the system (or users) can reach them.
- **ConfigMap** and **Secret**: Store configuration data and sensitive information like passwords separately from the container images.
- **PersistentVolume** (PV) and **PersistentVolumeClaim** (PVC): Handle storage so data can survive even if Pods are deleted.

#### Ephemeral Pods

### How to Mitigate Security Concerns with Containers

### Maintained Images

#### What They Are

#### Pros and Cons of Using Maintained Images for Your Base Container Images

## Create and Test Nginx Deployment with NodePort Service
For this step, I deployed an Nginx web server in Kubernetes using a Deployment and a NodePort Service.  
The goal was to run multiple replicas of Nginx and expose them externally via a port on my local machine.  
To make it more personal and visually distinct, I used my own **custom Nginx image** (`laurenksmith/nginx-tech511`) that I had previously pushed to Docker Hub.  
This image includes a modified `index.html` file, so when accessed in the browser, it displays my own version of the Nginx front page.

### What I Did

1. **Enabled Kubernetes in Docker Desktop**

   - In Docker Desktop, I went to **Settings → Kubernetes → Enable Kubernetes** and waited for it to start.
   - I then verified it was running by typing:

     ```bash
     kubectl get svc
     ```

     The output confirmed that the Kubernetes cluster was active:

     ```
     NAME         TYPE        CLUSTER-IP    EXTERNAL-IP   PORT(S)   AGE
     kubernetes   ClusterIP   10.96.0.1     <none>        443/TCP   3m56s
     ```

2. **Ensured I Was in my Repo Folder**

    - Using Bash, I cd'd into my repo folder (github/kubernetes-app-deployment)

3. **Created the Deployment YAML**

   - In my repo, I created a folder named `local-nginx-deploy/`.
   - Inside it, I added a file called `nginx-deploy.yml` with the following configuration:

     ```yaml
     apiVersion: apps/v1
     kind: Deployment
     metadata:
       name: nginx-deployment
     spec:
       replicas: 3
       selector:
         matchLabels:
           app: nginx
       template:
         metadata:
           labels:
             app: nginx
         spec:
           containers:
             - name: nginx
               image: laurenksmith/nginx-tech511
               ports:
                 - containerPort: 80
     ```

   - I applied it using:

     ```bash
     kubectl apply -f local-nginx-deploy/nginx-deploy.yml
     ```

   - To check it was running correctly, I used:

     ```bash
     kubectl get deploy,rs,pod -l app=nginx
     ```

   This showed three pods in the **Running** state.

4. **Created the NodePort Service**

   - I then created a file called `nginx-service.yml` in the same folder with the following configuration:

     ```yaml
     apiVersion: v1
     kind: Service
     metadata:
       name: nginx-svc
     spec:
       type: NodePort
       selector:
         app: nginx
       ports:
         - port: 80
           targetPort: 80
           nodePort: 30001
     ```

   - I applied it using:

     ```bash
     kubectl apply -f local-nginx-deploy/nginx-service.yml
     kubectl get svc nginx-svc
     ```

   - Once it was running, I tested it by visiting **http://localhost:30001** in my browser.

   - The custom Nginx welcome page that I had previously created and built into my Docker image appeared successfully — confirming that my image was being used correctly by the Kubernetes deployment.

![alt text](images/modified-nginx-page-running.png)

4. **Verification and Testing**

   - I also viewed all resources together using:

     ```bash
     kubectl get all -l app=nginx
     ```

     This displayed the deployment, replicasets, and pods, showing that all three replicas were running and connected to the NodePort Service.

   - Finally, I confirmed visually in Docker Desktop’s Kubernetes section that the three Nginx pods were active.

### Why This Step Matters

This step demonstrated how Kubernetes can:

- Deploy multiple replicas of a containerised web server.
- Maintain availability and consistency across all replicas.
- Expose internal services externally using a NodePort.
- Seamlessly use my own Docker Hub image (`laurenksmith/nginx-tech511`).

From a personal perspective, I liked that I could **see my own customised Nginx front page** running across all pods — a small detail that made the deployment feel much more real and rewarding to complete.



## Websites Used

### Understanding Kubernetes
- [Youtube: Kubernetes Explained in 15 Minutes](https://www.youtube.com/watch?v=r2zuL9MW6wc)
- [Kubernetes Documentation](https://kubernetes.io/docs/home/)
- 

### Kubernetes Architecture
- [Geeks for Geeks](https://www.geeksforgeeks.org/devops/kubernetes-architecture/)
- [kubernetes.io - Architecture](https://kubernetes.io/docs/concepts/architecture/)
- [kubernetes.io - Components](https://kubernetes.io/docs/concepts/overview/components/)
- [DevOps Cube](https://devopscube.com/kubernetes-architecture-explained/)
