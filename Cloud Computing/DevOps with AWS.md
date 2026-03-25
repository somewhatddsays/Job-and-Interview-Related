# DevOps with AWS

## Section 1 &mdash; AWS Networking & Infrastructure Fundamentals
### 1. What is a `Static IP` and a `Public IP`?

#### Static IP Address
A Static IP address is a fixed IP address assigned to a resource. <br>
It does not change even after restarting the instance.<br>
In **AWS**
* Elastic IP (EIP) is a static public Ipv4 address.
* Commonly used for:
  * Bastion hosts
  * Production web servers
  * Whitelisted services

#### Public IP Address
A Public IP allows a resource to communicate over the internet. <br>
In AWS:
* Automatically assigned public IPs are dynamic.
* They change if the instance is stopped and started.
* Elastic IPs remain constant

#### Interview Tip:
**Elastic IP** = Static Public IP<br>
**Default Public IP** = Dynamic Public IP

### 2. Difference between Security Group and Network ACL (NACL)
Understanding this is extremely important in AWS interviews. <br>

#### Security Group
* Works at the instance level.
* Acts like a firewall for EC2.
* Stateful (return traffic automatically allowed).
* Support allows rules only.

**Example:** <br>
If you allow inbound SSH (port 22), return traffic is automatically allowed.

#### Network ACL (NACL)
* Works at the subnet level.
* Stateless (must allow inbound and outbound separately).
* Supports both allow and deny rules.

**Example:**<br>
 You can deny traffic from a specific IP range at subnet level.

#### Key Differences

| Feature      | Security Group      | NACL                     |
|:-------------|:--------------------|:-------------------------|
| `Scope`      | Instance level      | Subnet level             |
| `Stateful`   | Yes                 | No                       |
| `Rules`      | Allow Only          | Allow + Deny             |
| `Evaluation` | All rules evaluated | Rules evaluated in order |

### 3. What are IAM Policies in AWS?
Policies define permissions in AWS.<br>
They are **JSON** documents that answer:
* Who can access?
* What actions?
* On which resources?
* Under what conditions?

#### Types of IAM Policies

| Type                        | Description                                            |
|:----------------------------|:-------------------------------------------------------|
| `AWS Managed Policies`      | Created and maintained by **AWS**                      |
| `Customer Managed Policies` | Created and managed by you                             |
| `Inline Policies`           | Attached to a specific IAM `user`, `group`, or `role`  |

#### Important Concept: The Least Privilege
Always grant minimum required access.
 ---


## Section 2 &mdash; Amazon S3 & Replication

### 1. How to Configure Cross-Region Replication (CRR)?
Steps:
1. Enable versioning on both source and destination buckets.
2. Create a replication rule.
3. Select designation region.
4. Assign an IAM role.
5. Enable  replication.

### 2. What happens if a file is Deleted in Source Bucket?
**By default**:
* Deleting in source does NOT delete in destination.
* Only new objects and updates replicate.

**If Delete Marker replication is enabled**:
* Delete replicate as well/

### Important Interview Insight:
CRR replicates objects, not bucket configurations.

 ---


## Section 3 &mdash; Virtualization & Containers

### 1. What is Virtualization?
Virtualization allows multiple Virtual Machines (VMs) to run on a single physical server using a hypervisor.<br>
**Example:**
* VMware
* KVM
* Hyper-V

Each VM has its own OS.

### 2. What is a Containerization?
Containerization package:
* Application 
* Dependencies
* Runtime

**Containers** share the host OS kernel. <br>
**Example:**
* Docker
* Podman

### Key Difference

| Virrtualization | Containerization |
|:----------------|:-----------------|
| Heavyweight     | Lighweight       |
| Separate OS     | Shared OS        |
| Slower boot     | Fast Startup     |

 ---


## Section 4 &mdash; Docker

### 1. What is a Dockerfile?
A **Dockerfile** is a script containing instructions to build a Docker image.

### Example Dockerfile

```yaml
FROM node:18-alpine
WORKDIR /app
COPY package* .json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD ["node", "server.js"]
```

### 2. What is a Docker Networking?
Docker networking allows containers to communicate with:
* Other containers
* Host machine
* External systems

|                             |                                                                             |
|:----------------------------|:----------------------------------------------------------------------------|
| **Default Docker Bridge**   | `bridge`                                                                    |
| **Create a Docker Network** | `docker network create my-network`                                          |
| **Run a Container**         | `docker run -d --name my-container my-image`                                |
| **Build and Run**           | `docker build -t my-image`<br> `docker run -d --name my-container my-image` |

 ---


## Section 5 &mdash; Kubernetes

### 1. What is a Deployment?
A deployment:
* Manages replicas
* Ensure desired state
* Supports rolling updates
* Enables rollback

### 2. Explain Pod Simply
A pod is the smallest unit in Kubernetes. <br>
Think of it as a lunchbox:
* It can contain one or more containers
* Containers share network and storage.

### 3. Deployment Strategies
1. `Rolling Update` <br>Gradual replacement
2. `Recreate` <br> Delete old, create new.
3. `Blue-Green` <br> Switch traffic fully.
4. `Canary` <br> Gradually traffic shift.

### 4. What is StatefulSet?

Used for stateful applications.<br> Features:
* Stable network identity
* Persistent storage
* Ordered deployment

**Example:**
* MySQL
* Cassandra

### 5. What is DaemonSet?
Runs one Pod per node. <br> Common use cases:
* Monitoring Agents
* Log collectors
* Security Agents

### 6. What is a Kubernetes Service?
Provides stable access to Pods. <br> **Types:**
* ClusterIP
* NodePort
* LoadBalancer
* ExternalName

### 7. LoadBalancer vs. Ingress

| Feature   | LoadBalancer   | Ingree            |
|:----------|:---------------|:------------------|
| `Layer`   | L4             | L7                |
| `Routing` | Single service | Multiple services |
| `Cost`    | Higher         | Lower             |

Ingress is more efficient for multiple services.
 ---

### 8. Can you create a Pod without Deployment?
Yes. But:
* No auto-healing
* No Scaling
* No rolling updates

Deployment is recommended.


## Section 6 &mdash; Terraform

### 1. Sample Terraform Script

```yaml
provider "aws"{
  region = "us-east-1"
}

resource "aws_s3_bucket" "my_bucket"{
  bucket = "my-bucket-terraform-demo"
  acl = "private"
}

resource "aws_instance" "my_ec2" {
  ami = "ami-0c02fb55956c7d316"
  instance_type = "t2.micro"
  tags = {
    Name = "TerraformDemo"
  }
}

```
### 2. Explanation
* Provider defines **AWS region**.
* **S3** resource creates private bucket.
* **EC2** resource launches instance.

#### Important Interview Concepts
* terraform init 
* terraform plan
* terraform apply
* terraform destroy
* State file
* Remote backend
* Locking
 ---


## Section 7 &mdash; Kubernetes on AWS (EKS)

### 1. How to setup `EKS`
**Steps**:
* Create EKS cluster.
* Create node group.
* Configure kubectl.
* Deploy workloads

**Commands:** <br> `aws eks update-kubeconfig --name cluster-name`

#### Important EKS Concepts
* Managed Node Groups
* Fargate
* IAM Roles for Service Accounts (IRSA)
* VPC CNI Plugin
 ---


## Section 8 &mdash; Advanced Interview Additions (Commonly Asked)

### Difference between `IAM Role` and `IAM User`
* `User` = Permanent identity
* `Role` = Temporary credentials

### What is Autoscaling?
Automatically increases or decreases EC2 instances based on load.

### What is Launch Template?
Defines **EC2** configuration for scaling..

### What is CloudWatch?
Monitoring services for:
* Logs
* Metrics
* Alarms

### What is High Availability?
System remains operational even if component fail.<br> Achieved using:
* Multi-AZ deployment
* Load balancer
* Auto scaling


## Final Interview Advice
When answering:
* Don't just define.
* Explain real-world usage.
* Mention


























 ---


