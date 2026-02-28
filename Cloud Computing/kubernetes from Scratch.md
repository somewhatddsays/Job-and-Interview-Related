# Kubernetes from Scratch

## Table of Contents
1. Introduction to Kubernetes
    - What is Kubernetes
    - What does orchestration do?
    - Famous container orchestrators
2. Kubernetes Architecture & Components
   - Master node vs Worker node 
   - Master node components 
   - Worker node components 
   - Add-ons (DNS. Web UI. Runtime)
3. Kubernetes Core Concepts
   - Pods
   - Deployments
   - Services
   - Namespaces
   - Desired State
   - Secrets
   - CoreDNS
   - ReplicaSet vs. Deployment
   - DaemonSet
   - Labels & Selector
   - Annotations
   - Node affinity/ Anti-Affinity
   - Taints & Tolerations
   - ConfigMaps
   - Volumes
4. kubectl Commands + Essentials
   - kubectl syntax
   - Common commands list
   - Vim setup for YAML
   - PODS, Deployments, Services, Volumes
   - Secrets, ConfigMaps, Ingress
   - Scheduler, RBAC, Troubleshooting
5. Kubernetes YAML (Basics + Examples)
   - YAML vs JSON
   - Required YAML fields
   - apiVersion and Kind reference
6. Kubernetes Installation (kubeadm on CentOS)
   - Prepare nodes
   - Install Docker + Kubernetes tools
   - Initialize cluster
   - Join worker nodes
   - Deploy first Pod + Service
7. Kubernetes Namespace
   - What is namespace?
   - Why namespaces matter
   - Resource quotas in namespaces
8. Kubernetes Deployments
   - Deployment vs ReplicationController
   - Strategies (Recreate vs RollingUpdate)
   - Upgrade, Rollback, History
   - Scaling + NodeSelector
9. Kubernetes Networking
   - Container-to-container
   - Pod-to-pod
   - External-to-service
   - ClusterIP vs NodePort vs LoadBalancer vs Ingress
   - Ingress rules + Ingress Controller
10. Kubernetes Storage
    - PersistentVolume (PV)
    - PersistentVolumeChain(PVC)
    - NFS example
    - Volume types overview
11. Kubernetes Security
    - RBAC (Roles, Bindings)
    - Users vs. ServiceAccounts
    - Namespace-limited user example
    - Secrets usage (env + mount)
12. Kubernetes Logging & Monitoring
    - Prometheus
    - Sematext Docker Agent
    - Kubernetes log metadata

## Introduction to Kubernetes
### What is Kubernetes?
Kubernetes (K8s) is an open-source container orchestration platform originally developed by Google. It is used to manage containerized applications across a cluster of machines.
Kubernetes provides:
- High availability
- Zero downtime deployments
- Auto scaling
- Self-healing
- Automatic rollbacks

📌Kubernetes was inspired by Google's internal systems Borg & Omega (used since ~2003). Google open-sourced Kubernetes in 2014.

---

### What does orchestration do?
Orchestration is the automation of running containers in production.
It handles:
- Configuring and scheduling containers
- Provisioning and deployments
- High availability (HA)
- Application configurations
- Scaling workloads automatically
- Hardware resource allocation (CPU/RAM)
- Load balancing + service discovery
- Health monitoring
- Securing container interactions
---

### Famous Container Orchestrators
- Docker Swarm
- Apache Mesos (Mesosphere)
- Nomad
- Cloud Foundry
- Cattle
- Managed Cloud Kubernetes (Azure, AWS, GCP, IBM, Alibaba)

## Kubernetes Architecture & Components
### 🧩Kubernetes Architecture Overview
A Kubernetes cluster consists of:
#### ✅Master Node (Control Plane)
   The master node manages the cluster and controls scheduling, monitoring, scaling, and maintaining the desired state.
#### ✅Worker Nodes
   Worker nodes run applications in the form of Pods (containers).
   You can run multiple master nodes for High Availability
---
### 🧠Master Node Components
- **API Server** (`kube-apiserver`) \
   The **Main entry point** for all cluster operations.\
   It:
      - receives commands from kubectl, UI, or automation
      - Validate requests
      - coordinates everything in Kubernetes 
---
- **Controller Manager** (`kube-controller-manager`) \
   Runs control loops to maintain the desired state, such as:
      - creating pods
      - scaling pods
      - healing pods
---
- **Replication Controller** \
   Ensures the specified number of Pod replicas are running at all times.
---
- **Node Controller**\
Manages node health and availability in the cluster
---
- **Scheduler(`kube-scheduler`)**\
Decides which worker node should run a new Pod based on:
  - CPU/RAM availability
  - node selectors
  - taints and toleration.
  - affinity/anti-affinity rules
---
- **etcd Cluster**\
etcd is the cluster's key-value database that stores:
  - cluster state
  - node info
  - workloads
  - configurations\

   ✅etcd is critical for Kubernetes.
---
### 🔌Add-ons in Kubernetes
- ✅**DNS (CoreDNS)**\
Provide name resolution inside the cluster
- ✅**Web UI (Dashboard)**\
A visual dashboard to manage and troubleshoot the cluster.
- ✅**Container Runtime**\
Kubernetes supports runtime such as:
  - Docker
  - containerd
  - CRI-O
---
### ⚙️Worker Node Components
- **kubelet**\
The kubelet runs on each node and:
  - connects the node to the master
  - ensures Pods are running
  - reports node health
---
- **kube-proxy** \
Handles networking and routing by:
  - forwarding traffic to the correct Pod 
  - maintaining iptables rules
  - enabling Services to work
---

- kubectl (Kubernetes CLI)\
`kubectl` is the command-line tool used to send commands to Kubernetes API Server. 
Every kubectl command becomes an API call to the master.
---

## Kubernetes Core Concepts
### 🧱Pod
A Pod is the smallest deployable unit in Kubernetes.\
A Pod can run:
1. [X] One container (most common)
2. [X] Multiple tightly coupled containers (advanced use case)\

📌Key Pod notes:
   - Every Pod gets one **IP address** 
   - Containers inside the same Pod share:
     - network namespace 
     - IP address 
     - resources
   - Communication between different Pods happens via **Pod IPs**


















