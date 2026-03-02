# Mastering Kubernetes

## Introduction to Kubernetes
### What is Kubernetes?
If I explain Kubernetes in an interview, I usually say:

Kubernetes is an open-source container orchestration platform used to run containerized applications in production reliably.
Instead of manually starting containers, restarting them, scaling them, and connecting them together, Kubernetes automates all of that.

**In simple words**:
- Docker runs containers 
- Kubernetes manages containers at scale 

**Kubernetes provides**:
- High availability (application never goes down)
- Automatic scaling 
- Self-healing (restarts failed containers automatically)
- Zero downtime deployments 
- Load balancing 
- Automatic rollback if deployment fails

>_Kubernetes was originally designed by Google based on their internal systems Borg and Omega, which they used for more than a decade before releasing Kubernetes publicly in 2014._

### What Does Orchestration Mean?

Orchestration means automation of container lifecycle management:\
Kubernetes automatically handles:
- Where containers should run 
- How many copies should run 
- Restarting crashed containers 
- Rolling updates 
- Service discovery 
- Load balancing 
- Resource allocation (CPU/RAM)
- Health monitoring

So instead of managing servers, we define the desired state, and Kubernetes continuously works to maintain it.

**Example**:
You declare **&rarr;** "I want 3 replicas of my application"

If one crashes **&rarr;** Kubernetes automatically creates a new one.

You never manually fix servers again.

### Famous Container Orchestrators

Before Kubernetes became dominant, multiple orchestrators existed:
- Docker Swarm 
- Apache Mesos 
- Nomad

Today, Kubernetes is the industry standard and is offered as managed service by:
- AWS (EKS)
- Azure (AKS)
- GCP (GKE)

## Kubernetes Architecture & Components
A Kubernetes cluster has two main parts:
- **Control Plane (Master Node)** **&rarr;** Brain of the cluster 
- **Worker Nodes** **&rarr;** Where applications actually run

---

### Control Plane Components

#### API Server (kube-apiserver)
This is the front door of Kubernetes.

Every action &mdash; `kubectl command`, UI request, automation pipeline &mdash; goes through the API server.

It validates requests and stores state in etcd.

Think of it as the central communication hub.

---

#### etcd
This is the database of Kubernetes.

**It stores**:
- cluster configuration 
- secrets 
- networking info 
- node health

If etcd is lost **&rarr;** cluster state is lost.\
So in production, etcd must always be backed up.

---

#### Scheduler
The scheduler decides:
>_"On which node should a new Pod run?"_

It checks:
- CPU & memory availability 
- node labels 
- taints & tolerations 
- affinity rules

It does NOT create containers &mdash; it only chooses placement.

---

#### Controller Manager
Controllers constantly monitor cluster state.\
Example controllers:
- Node Controller **&rarr;** checks node health 
- Replica Controller **&rarr;** ensures correct replica count

Controllers implement Kubernetes **`self-healing behavior`**.

---

### Worker Node Components
#### kubelet
Agent running on every node.\
It communicates with API server and ensures containers are running.\
If container dies **&rarr;** `kubelet` restarts it.

---

#### kube-proxy
Handles networking rules and routing.\
It makes Services work by forwarding traffic to correct Pod.

---

#### Container Runtime
Software that actually runs containers:
- containerd 
- CRI-O 
- Docker (older setups)

---

### Cluster Add-ons
#### CoreDNS
Internal DNS system.
database.default.svc.cluster.local

---

#### Dashboard
Web UI for cluster management.

---

## Kubernetes Core Concepts
### Pod
Smallest deployable unit in Kubernetes.\
A Pod contains one or more containers.\
**Important facts**:
- Each Pod has its own IP address 
- Containers inside same Pod share network and storage 
- Pods are temporary (ephemeral)

> _You never manage containers directly in Kubernetes &mdash; you manage Pods._

### Deployment
Deployment manages Pods.\
It provides:
- rolling updates 
- rollback 
- scaling 
- version control

> _We never create Pods directly &mdash; we create Deployments._

### ReplicaSet
Ensures a fixed number of Pods are running.\
Deployment uses ReplicaSet internally.\
So:
Deployment **&rarr;** manages ReplicaSet **&rarr;** manages Pods

---

### Service
Pods change IP frequently.\
Service provides a stable endpoint to access Pods.
It gives:
- fixed IP 
- DNS name 
- load balancing

---

### Namespace
Logical separation inside one cluster.\
Used for:
- teams 
- environments 
- projects
- dev
- staging 
- prod

---

### Desired State Concept
Kubernetes always tries to match **actual state** with **declared state**.\
**You declare**:\
replicas: 3\
**Current**:\
2 running\
Kubernetes automatically creates 1 more.\
No manual intervention needed.

---

### ConfigMap
Stores configuration values separately from application.
>**Example**:\
Instead of hardcoding DB URL inside container,
store it in ConfigMap.

This keeps images reusable.

---

### Secret
**Stores sensitive data**:
- passwords 
- API keys

**Used as**:
- environment variables
- mounted files

>**Important note**:
By default secrets are Base64 encoded, not encrypted.

---

### Labels & Selectors
Labels identify objects:
```
app=frontend
env=production
```
Selectors find objects using labels.\
Services use selectors to know which Pods to send traffic to.

---

### DaemonSet
Runs a Pod on every node.
Used for:
- monitoring agents 
- log collectors 
- security agents

>Example: Prometheus node exporter

---

### Taints and Tolerations
Used to reserve nodes for special workloads.

---

### Affinity & Anti-Affinity
Controls placement rules:
- Run Pods together 
- Run Pods apart

Used for high availability.

---

## kubectl Commands Essentials
General syntax:\
`kubectl <action> <resource>`

### Common Commands
### 🚀 Kubernetes: Lifecycle & Scaling
| Category | Command | Description |
| :--- | :--- | :--- |
| **Delete Resource** | `kubectl delete -f file.yaml` | Removes resources defined in a specific YAML file. |
| **Scaling** | `kubectl scale deploy <name> --replicas=5` | Manually increases or decreases the number of running pods. |
| **Rollback** | `kubectl rollout undo deployment <name>` | Reverts a deployment to its previous stable version. |
| **Check Rollout** | `kubectl rollout status deployment <name>` | Monitors the progress of an update or rollback. |
| **Apply Changes** | `kubectl apply -f file.yaml` | Creates or updates resources defined in a YAML file. |

**Quick Note on Deleting:** If you don't have the YAML file, you can also delete by name:  
`kubectl delete pod <pod-name>` or `kubectl delete service <svc-name>`.

## Kubernetes YAML Basics
Kubernetes is declarative &mdash;  everything is defined using YAML.\
Every YAML must contain:
- apiVersion 
- kind 
- metadata 
- spec

**Example**:
```
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
    - name: nginx
      image: nginx
```

## Kubernetes Installation using kubeadm (Conceptual Understanding)

1. Prepare nodes
2. Install container runtime
3. Install kubeadm, kubelet, kubectl 
4. Initialize master
5. Join worker nodes
6. Install networking plugin

**After joining nodes**:
- kubectl get nodes 
- Cluster becomes ready.

---

## Kubernetes Networking
Kubernetes networking _works in 4 levels_:
1. Container **&rarr;** Container (same pod)
2. Pod Pod **&rarr;** (different nodes)
3. Pod **&rarr;** Service
4. External **&rarr;** Service

---

### Service Types

| Command   | Description                                                                                |
|:----------|:-------------------------------------------------------------------------------------------|
| ClusterIP | Internal Communication inside cluster                                                      |
| NodePort  | Creates cloud load balancer                                                                |
| Ingress   | HTTP routing to multiple services via one endpoint <br/>Ingress is preferred in production |

---

## Kubernetes Storage
| Storage Type                  | Description                        |
|:------------------------------|:-----------------------------------|
| Persistent Volume (PV)        | Actual storage source              |
| Persistent Volume Claim (PVC) | Request for storage by application |

> **NOTE**:
> - Pod uses _PVC_, not _PV_ directly
> - This abstraction allows changing storage backend without modifying application.

## Kubernetes Security

### RBAC (Role Based Access Control)
Controls what users can do.

Objects:
- Role 
- RoleBinding 
- ClusterRole 
- Cluster RoleBinding

---

### Service Accounts
Identity used by Pods to talk to API server.\
Never run production Pods with default service account.

---

### Secrets Usage
Secrets can be injected as:

#### Environment Variable Injection

| Method | How It Works | YAML Field | Use Case | Example |
|--------|--------------|------------|----------|----------|
| Single Secret Key as Env | Inject one secret key as an environment variable | `env[].valueFrom.secretKeyRef` | When only one specific key is needed | DB_PASSWORD |
| Entire Secret as Env | Inject all keys as environment variables | `envFrom.secretRef` | When multiple secret keys are needed as env vars | App config |

#### Volume Mount Injection

| Method | How It Works | YAML Field | Use Case | Example |
|--------|--------------|------------|----------|----------|
| Secret as Volume | Mount secret as files inside container | `volumes[].secret` | TLS certs, SSH keys, config files | /etc/secrets |
| Specific Secret Items | Mount specific keys as specific file paths | `volumes[].secret.items` | Custom file naming | tls.crt → server.crt |
| ReadOnly Volume | Mounted secret volume is read-only (default behavior) | `volumeMounts.readOnly: true` | Security best practice | Prevent modification |

#### Projected Volumes

| Method | How It Works | YAML Field | Use Case | Example |
|--------|--------------|------------|----------|----------|
| Projected Secret Volume | Combine multiple sources into one volume | `volumes[].projected` | Combine secrets + configmaps | Unified config directory |
| ServiceAccount Token Projection | Inject SA token via projected volume | `serviceAccountToken` | Pod authentication to API server | API access |


#### CSI Secret Store (External Secret Providers)

| Method | How It Works | Provider | Use Case | Example |
|--------|--------------|----------|----------|----------|
| Secret Store CSI Driver | Mount secrets from external provider | Azure / AWS / Vault | Cloud-native secret management | AWS Secrets Manager |
| Auto Rotation | Secrets auto-refresh inside pod | CSI Driver feature | Dynamic secrets | Vault rotation |

#### External Secret Controllers

| Method | How It Works | Tool | Use Case | Example |
|--------|--------------|------|----------|----------|
| External Secrets Operator | Sync external secret into Kubernetes Secret | ESO | Cloud-native secret sync | AWS SM → K8s Secret |
| Vault Injector | Sidecar injects secret as file/env | HashiCorp Vault | Dynamic secrets | DB credentials |

#### Init Containers

| Method | How It Works | Use Case | Notes |
|--------|--------------|----------|-------|
| Init Container Fetch | Fetch secret before main container starts | Custom secret retrieval | Manual approach |
| Write to Shared Volume | Init container writes secret to volume | Legacy systems | More control |

#### Sealed Secrets

| Method | How It Works | Tool | Use Case |
|--------|--------------|------|----------|
| Sealed Secret | Encrypt secret for Git storage | Bitnami Sealed Secrets | GitOps workflows |
| Controller Decrypt | Controller decrypts into real Secret | Sealed Secrets Controller | Secure CI/CD |

## Monitoring & Logging
In production, cluster visibility is mandatory.

### Monitoring Stack

**Prometheus** **&rarr;** collects metrics
**Grafana** **&rarr;** visualizes metrics

**Used for**:
* CPU usage
* memory usage
* pod restarts
* request rate

Logs usually collected using agents and sent to centralized system.\
Important because containers are ephemeral &mdash; local logs disappear.

## Final Understanding (Interview Closing Statement)
If I summarize Kubernetes in one line during interview:

Kubernetes is a declarative, self-healing platform that ensures applications run reliably in distributed environments by constantly reconciling the current state with the desired state.

We don't manage servers anymore &mdash; we define expectations, and Kubernetes continuously maintains them automatically.
