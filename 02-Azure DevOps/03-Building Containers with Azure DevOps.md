# DevOps Training Content

# Module 3: Containers, Orchestration & Kubernetes

---

# 1. Introduction to Container

## What is a Container?

A container is a lightweight, portable, and isolated environment used to package an application along with its dependencies, libraries, and configurations.

Containers ensure that applications run consistently across different environments.

---

## Why Containers?

Traditional application deployment faces problems such as:

* “Works on my machine” issue
* Dependency conflicts
* Environment inconsistency
* Difficult scaling
* Slow deployments

Containers solve these challenges.

---

## Container Architecture

```text id="k9d2pl"
Application + Dependencies + Runtime → Container Engine → Host OS
```

---

## Key Features of Containers

| Feature      | Description             |
| ------------ | ----------------------- |
| Lightweight  | Uses shared OS kernel   |
| Portable     | Runs anywhere           |
| Fast Startup | Starts in seconds       |
| Isolated     | Separate environments   |
| Scalable     | Easy horizontal scaling |

---

## Containers vs Virtual Machines

| Feature        | Containers  | Virtual Machines |
| -------------- | ----------- | ---------------- |
| OS Included    | No          | Yes              |
| Size           | Lightweight | Heavy            |
| Startup Time   | Seconds     | Minutes          |
| Performance    | Faster      | Slower           |
| Resource Usage | Low         | High             |

---

## Container Lifecycle

```text id="3r8vqa"
Build → Ship → Run → Scale → Destroy
```

---

## Popular Container Platforms

| Platform   | Purpose                           |
| ---------- | --------------------------------- |
| Docker     | Container creation and management |
| Podman     | Daemonless container engine       |
| containerd | Container runtime                 |
| CRI-O      | Kubernetes runtime                |

---

# Docker Overview

## What is Docker?

Docker is the most widely used container platform that enables developers to build, package, and run applications inside containers.

---

## Docker Components

| Component        | Description        |
| ---------------- | ------------------ |
| Docker Engine    | Core runtime       |
| Docker Image     | Blueprint/template |
| Docker Container | Running instance   |
| Dockerfile       | Build instructions |
| Docker Registry  | Image storage      |

---

## Docker Workflow

```text id="8f7zqv"
Dockerfile → Docker Image → Docker Container
```

---

## Sample Dockerfile

```dockerfile id="1m7qka"
FROM nginx:latest
COPY . /usr/share/nginx/html
EXPOSE 80
```

---

## Basic Docker Commands

### Pull Image

```bash id="0v2kdf"
docker pull nginx
```

### Run Container

```bash id="7w9npl"
docker run -d -p 80:80 nginx
```

### List Containers

```bash id="5y3qmb"
docker ps
```

---

# 2. Introduction to Orchestration

## What is Container Orchestration?

Container orchestration is the automated management of containerized applications.

It handles:

* Deployment
* Scaling
* Networking
* Load balancing
* Monitoring
* Recovery

---

## Why Orchestration is Needed

Managing containers manually becomes difficult when applications grow.

Challenges include:

* Managing hundreds of containers
* Auto scaling
* Service discovery
* High availability
* Fault tolerance

---

## Orchestration Workflow

```text id="2x5mlo"
Container Deployment → Scheduling → Scaling → Monitoring → Recovery
```

---

## Features of Container Orchestration

| Feature              | Description                     |
| -------------------- | ------------------------------- |
| Automated Deployment | Deploy containers automatically |
| Auto Scaling         | Increase/decrease containers    |
| Load Balancing       | Traffic distribution            |
| Self-Healing         | Restart failed containers       |
| Service Discovery    | Container communication         |

---

## Popular Orchestration Tools

| Tool         | Description                         |
| ------------ | ----------------------------------- |
| Kubernetes   | Most popular orchestration platform |
| Docker Swarm | Native Docker orchestration         |
| Apache Mesos | Distributed systems orchestration   |
| Nomad        | Lightweight orchestrator            |

---

## Benefits of Orchestration

* High Availability
* Automated Scaling
* Better Resource Utilization
* Simplified Management
* Disaster Recovery

---

# 3. Introduction to Kubernetes

## What is Kubernetes?

Kubernetes is an open-source container orchestration platform used to automate deployment, scaling, and management of containerized applications.

Originally developed by:
Google

---

## Why Kubernetes?

Kubernetes helps organizations:

* Manage large-scale container environments
* Achieve high availability
* Automate deployments
* Scale applications dynamically

---

## Kubernetes Architecture

```text id="9n4bqe"
Master Node(Control Plane)
        ↓
Worker Nodes
        ↓
Pods → Containers
```

---

# Kubernetes Components

## Control Plane Components

| Component          | Purpose                 |
| ------------------ | ----------------------- |
| API Server         | Entry point for cluster |
| Scheduler          | Assigns workloads       |
| Controller Manager | Maintains desired state |
| etcd               | Cluster database        |

---

## Worker Node Components

| Component         | Purpose         |
| ----------------- | --------------- |
| Kubelet           | Node agent      |
| Kube Proxy        | Networking      |
| Container Runtime | Runs containers |

---

# Important Kubernetes Objects

## Pod

A Pod is the smallest deployable unit in Kubernetes.

It contains:

* One or more containers
* Shared storage
* Shared networking

---

## Deployment

Deployment manages application replicas and updates.

---

## Service

Service exposes applications internally or externally.

---

## Namespace

Namespaces logically separate cluster resources.

---

## ConfigMap & Secret

| Resource  | Purpose              |
| --------- | -------------------- |
| ConfigMap | Store configuration  |
| Secret    | Store sensitive data |

---

# Kubernetes Workflow

```text id="4g8qwr"
Developer → YAML Manifest → API Server → Scheduler → Worker Node → Pod Creation
```

---

# Kubernetes YAML Example

## Pod Example

```yaml id="5v8jtn"
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
spec:
  containers:
  - name: nginx
    image: nginx
```

---

# Kubernetes Features

| Feature           | Description                |
| ----------------- | -------------------------- |
| Self-Healing      | Restarts failed containers |
| Auto Scaling      | Dynamic scaling            |
| Rolling Updates   | Zero downtime deployments  |
| Service Discovery | Internal communication     |
| Load Balancing    | Traffic distribution       |

---

# Kubernetes Benefits

* High Availability
* Scalability
* Portability
* Automation
* Efficient Resource Usage

---

# Common Kubernetes Commands

## Create Deployment

```bash id="0s2xcm"
kubectl create deployment nginx --image=nginx
```

---

## Get Pods

```bash id="1v9npa"
kubectl get pods
```

---

## Get Services

```bash id="4r6qyd"
kubectl get svc
```

---

## Apply YAML File

```bash id="8m3klo"
kubectl apply -f deployment.yaml
```

---

# 4. Azure Kubernetes Service (AKS)

## What is AKS?

Azure Kubernetes Service is a managed Kubernetes service provided by Microsoft Azure.

AKS simplifies:

* Kubernetes deployment
* Cluster management
* Scaling
* Monitoring
* Security

---

## Why Use AKS?

Managing Kubernetes manually can be complex.

AKS reduces operational overhead by managing:

* Control plane
* Upgrades
* Monitoring
* Scaling
* Security patches

---

## AKS Architecture

```text id="3l5nqv"
Azure Portal/CLI
        ↓
AKS Cluster
        ↓
Node Pool
        ↓
Pods & Services
```

---

# AKS Components

| Component | Description            |
| --------- | ---------------------- |
| Cluster   | Kubernetes environment |
| Node Pool | Group of worker nodes  |
| Pod       | Running application    |
| Service   | Application exposure   |
| Ingress   | HTTP routing           |

---

# AKS Features

| Feature               | Description                |
| --------------------- | -------------------------- |
| Managed Control Plane | Azure manages master nodes |
| Auto Scaling          | Dynamic node scaling       |
| Integration           | Azure services integration |
| Security              | Azure AD & RBAC            |
| Monitoring            | Azure Monitor integration  |

---

# Creating AKS Cluster

## Using Azure CLI

### Create Resource Group

```bash id="6c1wpm"
az group create --name aks-rg --location eastus
```

---

### Create AKS Cluster

```bash id="8p5zdl"
az aks create \
--resource-group aks-rg \
--name myAKSCluster \
--node-count 2 \
--enable-addons monitoring \
--generate-ssh-keys
```

---

### Connect to AKS Cluster

```bash id="9m7qte"
az aks get-credentials \
--resource-group aks-rg \
--name myAKSCluster
```

---

# Deploy Application to AKS

## Create Deployment

```bash id="4z2pkn"
kubectl create deployment nginx --image=nginx
```

---

## Expose Deployment

```bash id="5t8vla"
kubectl expose deployment nginx \
--port=80 \
--type=LoadBalancer
```

---

# AKS Networking

AKS supports:

* Azure CNI
* Kubenet
* Load Balancers
* Ingress Controllers

---

# AKS Scaling

## Manual Scaling

```bash id="7y3qnb"
kubectl scale deployment nginx --replicas=3
```

---

## Cluster AutoScaler

Automatically adjusts node count based on workload.

---

# AKS Security Best Practices

* Enable RBAC
* Use Azure AD Integration
* Store secrets securely
* Scan container images
* Use Network Policies
* Enable Monitoring

---

# AKS Monitoring

AKS integrates with:

* Azure Monitor
* Log Analytics
* Prometheus
* Grafana

---

# AKS Benefits

| Benefit            | Description                 |
| ------------------ | --------------------------- |
| Reduced Management | Azure handles control plane |
| Scalability        | Easy scaling                |
| Security           | Enterprise-grade security   |
| Cost Optimization  | Pay-as-you-use              |
| DevOps Integration | CI/CD support               |

---

# Summary

In this module, we covered:

* Container fundamentals
* Docker basics
* Container orchestration
* Kubernetes architecture
* Kubernetes objects and commands
* Azure Kubernetes Service (AKS)
* AKS deployment and scaling

These concepts provide the foundation for modern cloud-native application deployment and container orchestration in DevOps environments.
