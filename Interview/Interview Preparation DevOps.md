from nis import cat

# Interview preparation Cheat Sheet For DevOps

#### What are the types of Docker Volumes?
Docker provides three types of Volumes:

| Type               | Description                                                 |
|:-------------------|:------------------------------------------------------------|
| `Host Volume`      | Maps a directory from the _host machine_ to the _container_ |
| `Anonymous Volume` | Docker manages the volume without a specific name           |
| `Named Volume`     | User-defined and persisted independently of containers.     |

---

#### What is Kubernetes `taint` and `tolerance`?
* **Taint** is applied on a node to **restrict** and scheduling.
* **Toleration** is applied on pods to **allow** them to run on tainted nodes.

Used to **isolate workloads**, e.g., run only specific apps on specific nodes.

---

#### If you want to add an existing resource to the Terraform state file?
Use the following command:
```aiignore
terraform import <resource_address> <resource_id>
```

---

#### Can pod-to-pod communication happen by default?
Yes.<br>
In kubernetes, all pods can communicate with each other by default within the cluster because the cluster network is **flat and non-restrictive** unless **Network Policies** restrict it.

---

#### What are Helm charts?
A **Helm Chart** is a package of `YAML` templates used to deploy Kubernetes applications through versioned, repeatable, and configurable deployments.

---

#### How will you deploy Jenkins in your organization?
4 common approaches:
1. **EC2 installation** (manual setup)
2. **Docker container**
3. **Helm chart deployment on EKS**
4. **Kubernetes YAML manifests**

---

#### When you deploy Jenkins with Helm, what is the folder structure?
A helm chart typically includes:

```aiignore
Chart.yaml
values.yaml
templates/
    deployment.yaml
    services.yaml
    ingress.yaml
    configmap.yaml
    pvc.yaml
charts/
README.md
```

---

#### How much time will be taken for a Jenkins job completion?
Depends on pipeline stages, application build time, tests, and infra speed.
<br>
Typically ranges from **1 minute to 15+ minutes** depending on the complexity.

---

#### Where do you deploy the microservices?
Usually deployed in:
* **Kubernetes (EKS)**
* **Docker Containers**
* **ECS**
* **EC2**
* **Fargate**

---

#### Who manages the infrastructure in your organization?
Infrastructure is usually managed by the **DevOps Team** using IaC tools like **Terraform**, **ClouFormation**, and **Ansible**.

---

#### Application deployed in EKS but not accessible externally &mdash how will you debug?
**Steps**:
1. Check **Service type** (LoadBalancer/ NodePort).
2. Check **Ingress** configuration.
3. Check **Security Groups** inbound rules.
4. Check **NACLs/ VPC routing**
5. Check **DNS** mapping.
6. Check if pods are running and services endpoints exist.

---

#### Explain the Git branching strategy
Most Common: Gitflow &mdash;
* **main/ master** &mdash; Stable production.
* **develop** &mdash; Active development.
* **feature/** &mdash; New Features
* **release/** &mdash; Pre-Production
* **hotfix/** &mdash; Quick patches on production

---

#### How can you restrict pod-to-pod communication?
Using **Kubernetes NetworkPolicies**:
* Deny all traffic
* Allow only specific namespace/ app/ labels

---

#### Suppose Jenkins pipeline fails &mdash; how will you debug?
* Check console output
* Check **agent availability**
* Validates **credentials**
* Check **Docker build errors**
* Check **Git authentication**
* Check **Stage-specific errors**

---

#### How does communication happen in an EKS cluster?
Through:
* **Kubernetes network (CNI plugin)**
* **Service (ClusterIP/ NodePort/ LoadBalancer)**
* **CoreDNS**
* **VPC routing**

---

#### Python program to read log file and print error count

```python
count = 0
with open("app.log", "r") as f:
    for line in f:
        if "ERROR" in line:
            count += 1
print("Total ERROR messages:", count)
```

---

#### What type of agents are you using in Jenkins?
* Static EC2 agents
* Dynamic agents via Kubernetes plugin
* Docker agents
* Self-hosted runners

---

#### How are you deploying Jenkins: EC2 or EKS?
Depends on the organization, but commonly using **EKS with Helm** for scalability.

---

#### Difference between StatefulSet and Deployment?

| Deployment            | StatefulSet                |
|:----------------------|:---------------------------|
| Stateless apps        | Stateful apps(DB, Kafka)   |
| No stable indentity   | Stable network identity    |
| ReplicaPods identical | Persistent storage per pod |

---

#### Explain RBAC in Kubernetes
**RBAC = Role-Based Access Control** <br>
Controls **who** can access **what** using:
* **Roles**
* **ClusterRoles**
* **RoleBinding**
* **ClusterRoleBinding**

---

#### Jenkins deployed via `Helm` &mdash; how to update plugins?
**Two ways**:
1. Update **values.yaml** &rarr; plugin list.
2. Upgrade chart:

`helm upgrade jenkins -f values.yaml jenkins/ jenkins`

---

#### How do you store secrets in Kubernetes?
Using:
* **Kubernetes Secrets**  (Based64 encoded)
* **AWS Secrets Manager + CSI driver**
* **HashiCorp Vault**
---

#### Lost Jenkins password &mdash; how to restore?
* If using Helm:
    ```aiignore
    kubectl exec -it <pod> --cat
    /var/jenkins_home/secrets/initialAdminPassword
    ```
* Reset via admin account
* Restore backup (if taken)

---

#### What plugins do you use in Jenkins?
Common ones:
* Git
* Pipeline
* Credentials
* Blue Ocean
* Docker
* Kubernetes
* Slack
* SonarQube

---

#### How many DevOps engineers are in your team?
Typical answer: <br>
**4-6 DevOps engineers**, depending on project size

---

#### What is your project architecture?
A clean high-level answer:
* Microservices in **EKS**
* CI/ CD via **Jenkins/ GitHub Actions**
* IaC via **Terraform**
* Monitoring via **Prometheus & Grafana**
* Images in **ECR**
* Logs in **CloudWatch**

---

#### How do you receive tickets?
**Through**:
* JIRA
* ServiceNow
* Azure DevOps Boards

---

#### EC2 instance type used to deploy apps? Is it sufficient?
Example answer:<br>
`t3.medium/ t3.large` <br>
Choose based on:
* CPU
* Memory
* Auto-scaling
* Application load

---

#### Deployment strategies used?
* Rolling update
* Blue-Green
* Canary
* Recreate

---

#### Install Nginx on 10 servers using Ansible?
Use inventory + playbook

```aiignore
hosts: web
tasks:
 - name: Install nginx
    apt: name=nginx state=present
```

---

#### Explain Ansible structure

Folder structure:
```aiignore
inventories/
roles/
playbooks/
group_vars/
host_vars/
ansible.cfg
```

---

#### What is a playbook?
A `YAML file` that defines **tasks**, **modules**, and **roles** to execute automation.

---

#### What rollback strategies do you follow?
* Helm rollback
* Kubernetes deployment revision
* EC2 AMI rollback
* Terraform rollback
* Git revert

---

#### Difference between `git clone` vs. `git fork`, `merge` vs. `rebase`

* **Clone**: Copy repo locally
* **Fork**: Copy repo under your account
* **Merge**: Combines change with merge commit
* **Rebase**: Rewrites commit history for cleaner log

---

#### How to combine multiple commits into single commit?
`git rebase -i HEAD~n`

---

#### What is `.git` folder?
It stores:
* Repo history
* Branches
* Objects
* Configuration

---

#### If you lost .git folder &mdash; how to restore?
You cannot fully restore. You must `reinitialize`

```aiignore
git init
git remote add origin <url>
git fetch
```

---

#### Difference between `git pull` and `git fetch`?
* `git fetch` &mdash; downloads but doesn't merge
* `git pull` &mdash; downloads + merges automatically

---

#### Where do you store Jenkinsfiles and Dockerfiles?
Typically in each service repository:
```aiignore
/app
    Dockerfile
    Jenkinsfile
```

---

#### Docker stops & restarts — data lost. How to fix?
Use **Docker volumes** or **bind mounts** to persist data.

---

#### What is CrashLoopBackOff?
Pod keeps crashing and Kubernetes keeps restarting it. Causes:
* App errors
* Wrong configs
* Missing dependencies
* Liveness probe failure

---

#### How to delete unused Docker containers and images?
`docker system prune -a`

---

#### What type of Load Balancers have you used? 
* **ALB** 
* **NLB** 
* **CLB** In Kubernetes:
* **Ingress** Controller
* **Service LoadBalancer**

---

#### What are S3 storage classes? 
* Standard 
* Standard-IA 
* One Zone-IA 
* Glacier
* Glacier Deep Archive 
* Intelligent-Tiering

---

#### How to locate the path of a file?
`find / -name filename`

---

#### How to delete log files >50MB and older than 30 days?

`find /var/log -type f -size +50M -mtime +30 -delete`

---

#### Difference between CMD and ENTRYPOINT?
* **CMD**: Default command (can be overridden)
* **ENTRYPOINT**: Always executed and cannot be overridden (unless using --entrypoint).

---

#### How did you reduce deployment cost by 40%?
Sample answer: 
* Migrated workloads to **EKS with auto-scaling**
+ Used **Spot instances**
* Implemented **CI/CD** to reduce idle compute
* Optimized Docker images
* Reduced unused infrastructure with **Terraform** cleanup 
* Used $3 lifecycle policies




















