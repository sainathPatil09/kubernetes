# **Kubernetes Beginners Guide**


## **what is k8s, why k8s and how k8s helps ?** 

* # what is Kubernetes
    - K8s (short for Kubernetes) is an open-source container orchestration platform.

    - It automates the deployment, scaling, and management of containerized applications.

    - "Containerized applications" just means apps that are packaged in containers (like Docker).  
  
    ## Explaination to 5 year old

    You have lots of toy robots 🧸🤖.  
    Each robot can do a small job like sing, dance, or clean.  
    At first, you have only 2 robots, so you can take care of them yourself.  

    But then — you get 100 robots! 😱
    Now it's too hard to watch them all:  
    * Some robots fall down 🤕 
    * Some get tired 🥱
    * Some forget their jobs 😵

    #### Kubernetes (K8s) is like a magical robot teacher 👩‍🏫✨.
    * It tells the robots what to do.
    * It wakes up the robots if they fall.
    * It fixes problems without you even asking.
    * It keeps everything moving smoothly so you can just watch and enjoy!  


* # why kubernetes
    - Managing a few containers manually is fine... but what if you have hundreds or thousands?

    - What if you need to restart a crashed container automatically?

    - What if you want to scale up your app during high traffic automatically?

    - Kubernetes was built to solve all these problems efficiently.

* # How Kubernetes helps
    - Deployment Automation: Deploy apps easily without manual setup each time.

    - Scaling: Automatically increase or decrease the number of app instances based on load.

    - Self-healing: If a container crashes, Kubernetes restarts it automatically.

    - Load Balancing: Distributes traffic across containers to prevent overload.

    - Rolling Updates: Update your app without downtime.

    - Resource Management: Optimizes usage of your server resources (CPU, memory).

# In short:
* ###  👉 Without Kubernetes = manual, messy, hard to scale.  
* ###  👉 With Kubernetes = automatic, clean, scalable, reliable.


# **Kubernetes Architecture**
![k8s architecture diagram](https://miro.medium.com/v2/resize:fit:4800/format:webp/1*QWJijlj7kwd0hIYk8Wsnow.png)
### **Kubernetes has two big parts**
- Master (Control Plane) — The "Boss" 👑
- Workers (Worker Nodes) — The "Helpers" 🛠️

### More Detailed:
| Part | What it Does | Easy Explanation|
|------------|-------------|------------|
| Control Plane (Boss)   | Controls everything in the system  | Like the principal of a school 📚|
| Node (Worker)    | Machines that run your apps      | Like teachers teaching students 🧑‍🏫
| Pod    | Smallest unit. Runs 1 or more containers.     | Like a small classroom with students 🚸|
| Container | Your app inside a package | Like a student who does homework 📒|


## 🧩 Main Components inside Control Plane (Boss area):

- API Server 📞 → Talk to Kubernetes (like the phone line)

- Scheduler 📅 → Decides where your app should run (like a timetable maker)

- Controller Manager 🤹 → Keeps checking if everything is fine (like a monitor)

- etcd 📚 → Stores all data safely (like a diary)


## 🧩 Main Components inside Worker Node (Helper area):

- Kubelet 👨‍🔧 → Takes care of pods, talks to Control Plane.

- Kube-proxy 🌐 → Manages networking (lets apps talk to each other).

- Container Runtime 🚀 → Runs the actual containers (like Docker).

## 📖 What is kubectl ?
- kubectl is the command-line tool for interacting with a Kubernetes cluster.

- It’s like a remote control 🎮 that lets you talk to Kubernetes and tell it what to do.
- When you type a command in kubectl, it talks to the Kubernetes API server and executes the action you requested (like creating, deleting, or updating resources).


# **Kubernetes setup**

#### Setting up Kubernetes (K8s) can differ depending on whether you are running it locally (for development and testing) or in production (for real-world applications).

## 🏠 Local Kubernetes Setup
>- ## [Minikube](https://minikube.sigs.k8s.io/docs/start/?arch=%2Fwindows%2Fx86-64%2Fstable%2F.exe+download)

>- ## [Kind](https://kind.sigs.k8s.io/docs/user/quick-start/)

## 🌐 Production Kubernetes Setup  
- ### Kubernetes on Cloud Providers (Managed K8s)
    - Amazon EKS (Elastic Kubernetes Service) – AWS managed Kubernetes service.

    - Google GKE (Google Kubernetes Engine) – Google Cloud's managed Kubernetes service.

    - Azure AKS (Azure Kubernetes Service) – Microsoft's managed Kubernetes service.

# **Kubernetes Core Concepts**

## **Namespace, Pods, Workloads**

- ## **Namespace**  
    Namespace is like a separate folder 📁  
    logical partitions within k8s  
    environmental sepration - `dev, staging, prod`  
    by default k8s has default namespace  
    `kubectl create namespace my-namespace`  
    `kubectl get namespaces`  
    `kubectl delete namespace my-namespace`
- ## **Pod**  
    A Pod is like a box 📦 carrying one or more containers 🚚 together, with their shared network and storage.  
    Pod can have one or multiple containers  
    `kubectl get pods -n my-namespace`

- ## **Workloads** 
    - ### Deployments 
        A Deployment is a Kubernetes resource that helps you manage and scale your applications  
        self-healing, scaling, Rolling updates   
        `kubectl apply -f deployment.yml`

    - ### ReplicaSets 
        Ensure that a specified number of identical Pods are running at all times  
        ReplicaSets are same Deployments but replicasets do not have rolling updates

    - ### DaemonSets
        DaemonSets are also same as replicasets only difference is that it ensure that atleat one pod is running in one node  
        means if we have 3 worker node it enure that each node has one pod running  

    - ### StatefulSets
        StatefulSet is a tool in Kubernetes that helps you manage stateful applications (apps that need persistent storage and unique identities for each Pod).  
        It ensures that even if Pods crash or get restarted, they will still have their data and stable names.


## **Services, ConfigMaps, Secrets**

- ## **Services**
    Pods can come and go (because of scaling, updates, crashes), and every time a Pod restarts, its IP address can change.  
    Kubernetes Service gives a stable way to talk to your Pods, no matter how many times they restart or move!  
    **Types of Services**
    - NodePort
    - ClusterIP
    - LoadBalancer
    - ExternalName 

- ## **ConfigMaps**
    Used to store non-sensetive configuration data (like: Database URL, API keys, Environment modes) separately from application code  
    keeps configuration separate  
    easier to update  

- ## **Secrets**
    What about sensetive data ( like: passwords, Database credentials, Tokens ),  Protects your important private information  
    Automatically encoded (base64) — not easily readable at first glance.
    
## **Persistent Volumes (PV) and Persistent Volume Claims (PVC)**
- ## **Persistent Volumes (PV)**
    PV is like a physical storage space.  
    Kubernetes admins create PVs.  
    Can be anything: Disk, NFS, Cloud Storage, etc.
- ## **Persistent Volume Claims (PVC)**
    PVC is like a request for storage.  
    Pods make a PVC saying: "I need storage of 5GB."  
    Kubernetes matches PVC with a suitable PV.  
