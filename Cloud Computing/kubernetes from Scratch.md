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

---
