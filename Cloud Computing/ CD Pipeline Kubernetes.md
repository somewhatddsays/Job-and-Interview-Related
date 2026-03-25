# End-to-End CI/ CD Pipeline for Kubernetes Deployment
Practical DevOps Implementation Guide

---

## Chapter 1 &mdash; Understanding the Goal of This System

Modern software delivery is no longer about manually deploying application to servers Organizations need systems that are:
* Repeatable
* Secure
* Automated
* Scalable
* Recoverable
* Observable

The purpose of this architecture is to design a **fully automated software delivery platform** where:
1. Developers push code
2. The system validates the code
3. Security checks are performed
4. Container image is built
5. Image is scanned for vulnerabilities
6. Image is stored securely
7. Kubernetes automatically deploys it
8. Traffic is routed safely
9. Metrics and logs are monitored

No manual server login.<br>
No manual deployment steps. <br>
No hidden configuration.

Everything is declared, versioned, and reproducible.

This is the real meaning of DevOps maturity.

---

## Chapter 2 &mdash; High Level System Architecture
This pipeline follows a Git-driven automation model.

```shell
Developer &rarr; GitHub &rarr; Jenkins &rarr; Security Scans &rarr; Docker Build &rarr; Trivy Scan &rarr; Push to ECR &rarr; Update Manifests &rarr; ArgoCD &rarr; Kubernetes &rarr; ALB &rarr; Users &rarr; Monitoring
```
The system separates responsibilities clearly.

### Source Control Layer
Stores application code and Kubernetes manifests.

### CI Layer
Build and validates software.

### Security Layer
Prevents vulnerable code from reaching production.

### Artifact Layer
Stores trusted container images

### CD Layer
Automatically deploys to Kubernetes

### Infrastructure Layer
Cloud resources created using infrastructure as Code.

### Observability Layer
Continuously monitors system health.

---

## Chapter 3 &mdash; Why GitOps is Important
**Traditional deployment**:<br>
`Engineers logs into server &rarr; pulls code &rarr; runs commands &rarr; hopes it works`

### Problems
* No audit history
* No rollback guarantee
* Human mistakes
* Hard to scale teams

### GitOps model:
Git repository becomes the source of truth.

`Cluster state = Git state`

* If **Git Changes** &rarr; cluster updates
* If **Git rolls back** &rarr; cluster rolls back

### ArgoCD continuously compares:
Desired State  (Git.) vs. Actual State (Cluster)

This makes deployments:
* Predictable
* Traceable
* Self-healing

---
 
## Chapter 4 &mdash; Infrastructure Provisioning Using Terraform

Infrastructure must never be created manually.

Manual infrastructure causes:
* Configuration drift
* Unrecoverable environments
* Inconsistent production

Terraform solves this using declarative infrastructure.<br>
We describe infrastructure instead of creating it interactively.

---

### Core Resources Provisioned:
**The platform provisions**:
* VPC
* Subnets (public + private)
* Internal Gateway
* NAT Gateway
* Security Groups
* EKS Cluster
* Worker Nodes
* ECR Repository
* IAM Roles
* Load Balancer Permissions

---

### Terrform Workflow

| Workflow                        | Command             |
|:--------------------------------|:--------------------|
| **Initialize provider plugins** | `terrform init`     |
| **Preview Changes**             | `terraform plan`    |
| **Apply Infrastructure**        | `terraform apply`   |
| **Destroy Infrastructure**      | `terraform destory` |


### Why Terrform State Matters
Terraform keeps a file.<br>
State answers:
* What already exists?
* What must be changed?
* What must be created?

Without state Terraform cannot safely update infrastructure.

In real production systems state must be remote and locked.

**Typical setup**:
* **S3 bucket** &rarr; stores state
* **DynamoDB** &rarr; provides locking

Prevents two engineer from modifying infra simultaneously.

---

## Chapter 5 &mdash; Continuous Integration with Jenkins

Continuous Integration ensures every code change is validated automatically. <br>

**The moment code is pushed**:<br>
Pipeline starts.

No human triggers builds.

---

### CI Pipeline Stages

#### Stage 1 &mdash; Fetch Code
Pull source from GitHub.

#### Stage 2 &mdash; Code Quality Analysis
**Detects**:
* Bad practices
* Bugs
* Maintainability issues

Prevents technical debt from entering system.

#### Stage 3 &mdash; Dependency Vulnerability Scan
Checks project libraries for known CVEs. <br>
Prevents usage of compromised libraries.

#### Stage 4 &mdash; File System Security Scan
Ensure secrets are not accidentally committed:
* Keys
* Tokens
* Passwords

#### Stage 5 &mdash; Docker Image Build
Application packaged into container.

#### Stage 6 &mdash; Container Vulnerability Scan
Trivy analyze image layers.

**If critical vulnerabilities exist**: Pipeline fails automatically.


#### Stage 7 &mdash; Push to Registry
Trusted image stored in Amazon ECR.

---

## Chapter 6 &mdash; Container Security with Trivy

Containers are immutable packages. <br>
But immutability does not guarantee safety.

**A container can include**:
* Outdated packages
* Vulnerable OS libraries
* Malware dependencies

**Trivy scans**:
* OS Package
* Language package
* Secrets
* Misconfigurations

Deployment should never proceed if a high severity vulnerability is detected. <br>
This shifts security left &mdash before production.

---

## Chapter 7 &mdash; Container Registry (Amazon ECR)

Container images must be stored securely<br>
ECR provides:
* Private storage
* IAM authentication
* Encrypted storage
* Lifecycle cleanup
* Version Tagging

Images are tagged using commit hashes.<br>

**This ensures traceability**: We know exactly which code version is running.

---

## Chapter 8 &mdash; Continuous Deployment Using Argo CD
After Cl finishes, deployment must occur automatically. <br>
But Kubernetes should not be modified directly by Jenkins.<br>
Instead, Jenkins updates Git manifests.<br>
ArgoCD detects change and deploys. <br>
This separation gives safety and auditability. <br>
---
### ArgoCD Reconciliation Loop
1. Watches Git repository
2. Detects manifest changes
3. Applies to cluster
4. Monitors health
5. Self-heals drift

> If someone manually changes cluster &rarr; ArgoCD revert it.

---

## Chapter 9 &mdash; Kubernetes Application Architecture
The application is divided into three independent components:

#### Frontend
Handles user interface

#### Backend
Handles business logic

#### Database
Handles persistence. <br>
Each runs as separate deployment and service.<br>
Benefits:
* Independent scaling
* Fault isolation
* Easier updates

### Kubernetes Objects Used
* Pods
* Deployments
* Services
* Secrets
* ConfigMaps
* Ingress


---

## Chapter 10 &mdash; External Traffic Routing (Application Load Balancer)

Users access application through domain.<br>

Traffic flow:<br>
`User` &rarr; `DNS` &rarr; `Load Balancer` &rarr; `Ingress`  &rarr; `Service`  &rarr; `Pod`

Load balancer responsibilities:
* Distribute Traffic
* Health checks
* Failover
* SSL termination

---

## Chapter 11 &mdash; Domain & DNS Configuration

DNS maps human readable domain to load balancer. <br>
**Steps**:
1. Create Domain
2. Create A record
3. Point to ALB
4. Configure HTTPS

Now application becomes publicly reachable.

---

## Chapter 12 &mdash; Secret Management
Sensitive information must never be hardcoded.<br>
**Includes**:
* Database credentials
* API Tokens
* Registry passwords

Stored using `Kubernetes Secrets`. <br>
Injected into pods at runtime. <br>
No secrets exist in container images.

---

## Chapter 13 &mdash; Monitoring and Observability

Deployment without monitoring are blind systems.<br>
We implement three pillars:
* Metrics
* Logs
* Traces

### Prometheus
Collect **_system metrics_**:
* CPU
* Memory
* Requests
* Errors
* Latency

### Grafana
Visualize metrics using dashboards. <br>
Engineers can instantly detect:
* Traffic spikes
* Memory leaks
* Slow responses

---

## Chapter 14 &mdash; Reliability Benefits of This Architecture

**This system guarantees**:
* Self-healing
* Auto deployment
* Security validation
* Rollback capability
* Infrastructure reproducibility
* Operational visibility

Failures become events &mdash; not disasters.

---

## Chapter 15 &mdash; Deep Understanding of Kubernetes Internals
Most engineers can deploy to Kubernetes. <br>
Few understand how Kubernetes actually works internally. <br>
Understanding internals is what separates a user from a production engineer. <br>
Kubernetes is not a tool — it is a distributed control system. <br>
It continuously answers one question: <br>
"**Does the actual cluster match the desired state?**"
If not &rarr; it fixes it automatically.

### Kubernetes Control Plane Components

The control plane is the brain of the cluster.

#### API Server
Entry point of the duster. <br>
**Every command you run**:
`kubectl apply` <br>
`kubectl get` <br>
`kubectl delete` <br>

Actually talks to the API server. <br>
**The API server**:
* Validates requests
* Authenticates users
* Stores configuration

#### ETCD
Cluster database. <br>
Stores everything:
* Pods
* Services
* Secrets
* Configurations

If `etcd` is lost &rarr; cluster memory is lost <br>
This is why backups are critical.

#### Scheduler
Decides **where a pod runs**<br>
**It evaluates**:
* CPU availability
* Memory availability
* Node conditions
* Taints and Tolerations
* Affinity rules

Then assigns a node.

#### Controller Manager
Ensures desired state.

**Example**<br>
* Desired replicas = 3
* Actual running = 2

Controller creates 1 new pod.<br> It constantly compares and reconciles.

---

## Chapter 16 &mdash; Worker Node Components

Worker nodes actually run applications.

#### Kubelet

Node agent.<br>

**Responsibilities**:

* Talks to API server
* Ensures containers run
* Reports node health

#### Container Runtime

Runs containers. <br>

**Examples**:

* containerd
* CRI-O

Pulls image &rarr; starts container &rarr; manages lifecycle

#### Kube Proxy

Handles networking rules.

Creates iptables rules so services can route traffic to pods.


---

## Chapter 17 &mdash; Pod Lifecycle Deep Dive

Pods go through phases:<br>

> Pending &rarr; Running -Succeeded / Failed

#### Pod Creation Flow

1. Manifest applied
2. API server stores spec
3. Scheduler selects node
4. Kubelet pulls image
5. Container starts
6. Health checks begin

#### Liveness Probe

Checks if application is alive. <br>

If fails &rarr; container restarted

#### Readiness Probe

Checks if app is ready for traffic.

If fails &rarr; traffic stopped

These prevent broken deployments from receiving users.

---

## Chapter 18 &mdash; Deployment Strategies
Deploying new code safely is critical.

### Recreate Strategy

Stops old version &rarr; starts new version

**Problem**:
* Downtime

Used only for _non-critical_ workloads

### Rolling Update (Default)
Gradually replaces pods.

**Example**:
* 5 replicas

1 old pod removed<br>
1 new pod created

Zero downtime

### Blue-Green Deployment

**Two environments exist**:

`Blue = current production`<br>
`Green = new version`

Switch traffic instantly.

`Rollback = instant`

### Canary Deployment

Small percentage of users see the new version.

**If** 
* `stable` &rarr; **rollout continues.**
* `errors` &rarr; **rollback immediately**

Safety release strategy

---

## Chapter 19 &mdash; Kubernetes Networking Deep Dive

**Networking in Kubernetes is unique**:
* Every pod gets its own IP address.
* Pods communicate directly without NAT.

### Service Types
#### ClusterIP
Internal communication only.

#### NodePort
Exposes on node port.

#### LoadBalancer
Cloud load balancer.

#### Ingress
Layer 7 routing (HTTP routing rules).

### Ingress Controller

Acts as application gateway. <br>
Handles:
* Host based routing
* Path routing
* TLS termination

**Example**:
* `api.example.com` &rarr; backend
* `app.example.com` &rarr; frontend

Single public entry point.

---

## Chapter 20 &mdash; Storage and Persistence
Containers are ephemeral.<br>
Data disappears if pod dies.<br>
Persistent storage solves this.

### Persistent Volume (PV)
Actual storage resource.

### Persistent Volume Claim (PVC)
Request for storage. <br>
Pods use PVC &rarr; Kubernetes attaches storage.













