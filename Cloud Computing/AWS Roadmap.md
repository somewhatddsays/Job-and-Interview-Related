# AWS Roadmap

## Fundamentals (2&mdash;3 Weeks)

### Goal
Understand core AWS Services and cloud concepts.

### Do these with hands-on labs (not videos only)

- **AWS global infrastructure**
- **IAM** (users, roles, policies)
- **EC2** (launch, SSH, security, groups, AMIs)
- **S3** (buckets, versioning, encryption, lifecycle)
- **VPC basics** (subnets, route tables, IGW/ NAT, security groups)
- **RDS basics** (MYSQL/ PostgreSQL instance)
- CloudWatch & CloudTrail


## Core Services Deep Dive (4&mdash;6 Weeks)

### Goal
Build real infra, not slides.

### Compute

- EC2 Auto Scaling
- Elastic Load Balancer (ALB)
- Lambda (serverless basics)

### Storage

- S3 advanced (lifecycle, encryption, versioning)
- EFS, FSx
- Glacier for Backups

### Databases

- RDS (Multi-AZ)
- DynamoDB (NoSQL)
- ElasticCache (Redis)

### Networking

- VPC peering 
- NAT, Endpoints 
- Security groups vs NACLs (contrast and use)

### Monitoring & Logging
- CloudWatch metrics & alarms
- CloudTrail logs 
- Config rules

## Automation & IaC (3&mdash;4 Weeks)

Stop clicking the console once you know the services.
- CloudFormation deep 
- Terraform (industry standard)
- Parameterize stacks, use modules
- `Immutable infra` mindset

### Deliverables:

- Full infra coded in Terraform 
- Build + destroy environments with one command 
- Use workspace/vars for `dev` vs `prod`


## CI/CD & DevOps Flow (3&mdash;4 Weeks)

You must automate deployments.
- CodeCommit / GitHub
- CodeBuild 
- CodeDeploy / CodePipeline 
- Or GitHub Actions + Terraform + AWS

### Deliverables:

- Automated pipeline:
  > commit **&rarr;** build **&rarr;** deploy to staging
- Manual approval gate to prod

## Security & Best Practices (2&mdash;3weeks) &mdash; Non-Negotiable
You must know how to secure production systems.
- IAM best practices (roles, MFA)
- KMS / Secrets Manager
- WAF & Shield basics
- Security Hub + GuardDuty
- Encryption at rest / in transit

**Deliverables**:
- Locked-down prod account
- Key management plan
- Incident response playbook

## Advanced Architecture (4&mdash;6weeks)

**Goal**: Architect scalable, fault-tolerant systems.
- Serverless architectures (API Gateway + Lambda + Dynamo)
- Event-driven with SNS/SQS/EventBridge
- Containerization
  - ECS Fargate
  - EKS basics (Kubernetes)
- Cost optimization patterns

**Deliverables**:
- Event-driven API app with async processing
- CI/CD for containers
- Cost report with rightsizing

## Real Project (4&mdash;8weeks)

### Nothing substitutes real deliverables.

**Build at least 3 portfolio projects**
1. Scalable web application with RDS + ASG
2. Serverless API with Lambda + DynamoDB
3. Containerized app with ECS/EKS + CI/CD

Host **code on GitHub**, demo on **YouTube** (optional), include architecture diagrams









