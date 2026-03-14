# AWS Interview Guide (Practical + Scenario Based)

---

## Why AWS Skills Matter

Cloud adoption has changed how businesses build and operate systems. AWS is a leader in cloud computing, so demand for AWS-skilled engineers (DevOps / SRE / Cloud Engineers / Architects) continues to grow.

This guide helps you prepare with **real interview expectations**, focusing on:

- clear explanations (**what + why + how**)
- real production thinking
- troubleshooting mindset
- common follow-ups interviewers ask

---

## Table of Contents

### Core AWS Foundations
1. AWS Basics (Regions, AZs, Global Services)
2. IAM (Users, Roles, Policies, Security Best Practices)
3. Networking (VPC, Subnets, Routing, NAT, IGW, NACL, SG)
4. Compute (EC2, Auto Scaling, AMIs)
5. Storage (S3, EBS, EFS)
6. Load Balancing (ALB, NLB, CLB)
7. Databases (RDS, DynamoDB, Aurora)

### Operations + Monitoring + Automation
8. CloudWatch + Monitoring
9. CloudTrail + AWS Config
10. CloudFormation (IaC)
11. Backup + DR (RTO/RPO)
12. Cost Optimization

### Security + Best Practices
13. WAF, Shield, GuardDuty, Macie
14. Shared Responsibility Model
15. Well-Architected Framework

### Interview Scenarios + MCQs
16. Real-world scenario questions
17. Quick MCQs for practice

---

## 1) AWS Basics (Must Know)

### Q1. What is AWS?

**Answer:** AWS (Amazon Web Services) is a cloud platform offering compute, storage, networking, databases, security, analytics, and managed services.

Key advantage: **pay-as-you-go**, scalability, global infrastructure.

---

### Q2. What is the difference between a Region and an Availability Zone (AZ)?

**Answer:**

- **Region:** A geographic location (example: Mumbai, N. Virginia)
- **AZ:** A physically separate datacenter within a region

Best practice: Deploy across **multiple AZs** for high availability.

**Follow-up:** What is a Local Zone?
Local Zones provide AWS services closer to large metro areas to reduce latency.

---

### Q3. Which AWS services are global (not region-specific)?

Common global services include:

- IAM
- Route 53
- CloudFront
- WAF (global mode with CloudFront)

---

## 2) IAM (Identity and Access Management)

### Q4. What is IAM and why is it important?

**Answer:** IAM is used to securely manage access to AWS resources.

IAM controls:
- Users and credentials
- Permissions via policies
- Access via roles
- MFA and authentication

---

### Q5. IAM User vs IAM Role (Most asked)

**IAM User**
- Has long-term credentials (password/access keys)
- Used by humans or external systems

**IAM Role**
- Has temporary credentials (assumed role)
- Best for AWS services (EC2, Lambda, ECS, EKS)

Best practice: Use **roles** instead of storing access keys.

---

### Q6. What are IAM Policies?

**Answer:** Policies define **permissions** using JSON documents.

Types:
- AWS Managed Policies
- Customer Managed Policies
- Inline Policies

Best practice: **Least privilege** access only.

---

### Q7. What is an Instance Profile?

**Answer:** An Instance Profile is how an IAM Role is attached to an EC2 instance.

---

### Q8. What is MFA and why should you use it?

**Answer:** MFA adds a second layer of authentication beyond passwords.

Use MFA for:
- Root user
- Admin users
- Privileged operations

---

## 3) EC2 (Elastic Compute Cloud)

### Q9. Stop vs Terminate an EC2 instance

**Stop**
- Instance shuts down (can start again)
- EBS root volume remains (by default)

**Terminate**
- Instance is deleted permanently
- Root EBS volume is deleted (default behavior)

**Follow-up:** Can you prevent accidental termination?
Yes → enable **termination protection**.

---

### Q10. EC2 pricing models (Very common)

- **On-Demand:** Flexible, pay per second/minute
- **Reserved Instances:** 1–3 year commitment → cheaper
- **Spot Instances:** cheapest, can be interrupted
- **Savings Plans:** flexible alternative to RIs

---

### Q11. What is an AMI?

**Answer:** AMI (Amazon Machine Image) is a template used to launch EC2 instances (OS + configs).

Common design types:
- **Fully Baked AMI** (everything pre-installed)
- **Just Enough OS (JeOS)**
- **Hybrid AMI**

---

### Q12. How do you recover an EC2 instance if you lost the key?

Typical approach:
1. Stop instance
2. Detach root EBS volume
3. Attach volume to a temporary instance
4. Fix SSH config / authorized_keys
5. Re-attach volume back
6. Start instance

---

### Q13. How do you auto-recover EC2 using CloudWatch?

Steps:
1. Create a CloudWatch alarm
2. Choose **Recover this instance** action
3. Alarm triggers recovery automatically

---

## 4) Auto Scaling

### Q14. What is Auto Scaling?

**Answer:** Auto Scaling automatically adds/removes EC2 instances based on demand.

Scaling types:
- **Scale Out / In** (add/remove instances)
- **Target tracking** (keep CPU ~50%)
- **Scheduled scaling**

---

### Q15. Can you add an existing EC2 instance to an Auto Scaling Group?

Yes (from EC2 console):
- Instances → Actions → Instance Settings
- Attach to Auto Scaling Group

---

## 5) Load Balancing (ELB)

### Q16. Types of AWS Load Balancers

- **ALB (Application Load Balancer)** → L7 HTTP/HTTPS routing
- **NLB (Network Load Balancer)** → L4 TCP/UDP, high performance
- **CLB (Classic Load Balancer)** → legacy

---

### Q17. When do you use ALB vs NLB?

**ALB**
- HTTP routing (path-based, host-based)
- SSL termination
- Microservices

**NLB**
- TCP/UDP traffic
- Low latency
- Static IP support

---

## 6) Amazon S3 (Storage)

### Q18. What is S3?

**Answer:** S3 is object storage designed for durability and scalability.

Features:
- Versioning
- Lifecycle rules
- Encryption
- Cross-Region Replication

---

### Q19. S3 vs EBS (Very common)

**S3**
- Object storage
- Not attached to EC2
- Used for backups, logs, static assets

**EBS**
- Block storage
- Attached to EC2
- Used like a disk

---

### Q20. How do you control S3 access?

Use:
- IAM Policies
- Bucket Policies
- Access Control Lists (ACLs - older)
- Block Public Access

Best practice: Prefer **Bucket policy + IAM policy**, avoid ACL unless required.

---

## 7) VPC (Networking)

### Q21. What is a VPC?

**Answer:** A VPC is a logically isolated network in AWS where you deploy resources.

Inside a VPC:
- Subnets (public/private)
- Route tables
- IGW / NAT Gateway
- NACL / Security groups

---

### Q22. Security Group vs NACL

**Security Group**
- Stateful
- Instance level
- Only allows rules (no deny rules)

**NACL**
- Stateless
- Subnet level
- Supports allow + deny rules

---

### Q23. NAT Gateway vs NAT Instance

**NAT Gateway**
- Managed service
- Highly available
- Scales automatically

**NAT Instance**
- Self managed
- Needs patching + scaling
- More operational overhead

---

### Q24. VPC DNS not resolving — what could be wrong?

Fix by enabling:
**DNS Hostnames**
**DNS Resolution**

---

## 8) Route 53 (DNS)

### Q25. Domain vs Hosted Zone

**Domain**
- Your registered name (example.com)

**Hosted Zone**
- DNS record container for routing traffic for that domain

---

### Q26. Latency Based Routing vs Geo DNS

**Latency Routing**
- Sends traffic to lowest latency region

**Geo Routing**
- Routes based on user location (country/continent)

---

## 9) Databases (RDS & DynamoDB)

### Q27. Reserved vs On-Demand DB instances

They work the same technically, but billing differs:
- Reserved is cheaper long-term
- On-demand is flexible

---

### Q28. RDS scaling types

Vertical scaling (increase DB size)
Horizontal scaling using read replicas (mostly read scaling)

For massive scale: consider Aurora or DynamoDB.

---

### Q29. DynamoDB consistency models

- **Eventually consistent** (faster reads)
- **Strongly consistent** (latest reads guaranteed)

---

## 10) CloudWatch, CloudTrail & AWS Config

### Q30. What is Amazon CloudWatch?

**CloudWatch** helps monitor:
- metrics (CPU, memory via agent)
- logs
- alarms
- dashboards
- events

---

### Q31. CloudTrail vs AWS Config

**CloudTrail**
- Records API calls (who did what)

**AWS Config**
- Records resource configurations (what changed)

**Interview-ready summary:**
- CloudTrail answers: **WHO**
- Config answers: **WHAT**

---

## 11) CloudFormation (Infrastructure as Code)

### Q32. CloudFormation vs Elastic Beanstalk

**CloudFormation**
- Infrastructure provisioning
- Resources as code

**Elastic Beanstalk**
- App deployment platform
- Abstracts infrastructure management

---

### Q33. What happens if a CloudFormation resource fails to create?

CloudFormation typically:
Rolls back and deletes created resources automatically.

---

## 12) Disaster Recovery Concepts (RTO / RPO)

### Q34. What is RTO and RPO?

**RTO (Recovery Time Objective):** max acceptable downtime
**RPO (Recovery Point Objective):** max acceptable data loss

---

## 13) Security Services (High Value Questions)

### Q35. What is AWS WAF?

**WAF protects web apps from**:
- SQL injection
- XSS
- Bot traffic
- Custom rules

**Modes**:
- Allow
- Block
- Count

---

### Q36. What is AWS Shield?

**AWS Shield** protects against DDoS attacks.
- **Shield Standard**: default basic protection
- **Shield Advanced**: advanced protection + support

---

### Q37. What is GuardDuty?

GuardDuty is threat detection using:
- VPC flow logs
- DNS logs
- CloudTrail events

---

### Q38. What is Macie?

Macie discovers and classifies sensitive data in S3 using ML.

---

## 14) Cost Optimization (Frequently asked)

### Q39. How do you find if you are overpaying in AWS?

**Use**:
- Cost Explorer
- Budgets
- Cost allocation tags
- Trusted Advisor
- Compute Optimizer

**Best approach**:
1. Identify top cost services
2. Analyze idle/unused resources
3. Optimize instance types and storage
4. Use reserved/savings plans

---

## 15) Practical Scenario Questions (Real Interview Style)

### Scenario 1: Website is slow in production

**Debug checklist**:
1. Check ALB latency
2. Check EC2 CPU/memory
3. Check scaling activity
4. Check DB connections
5. Check CloudWatch logs

---

### Scenario 2: S3 access denied for an application

**Check**:
- IAM role attached?
- Bucket policy blocked?
- Public access block enabled?
- KMS permissions missing?

---

### Scenario 3: EC2 in private subnet cannot access internet

**Likely missing**:
- NAT Gateway route
- Route table entry
- Security group outbound rules

---

## Quick MCQs (Interview Practice)

**1) Which database is best for single-digit millisecond latency?**
- A) RDS
- B) Neptune
- C) Snowball
- D) DynamoDB ✅

**2) Which service helps with real-time monitoring and alerts?**
- A) Firewall Manager
- B) GuardDuty
- C) CloudWatch ✅
- D) EBS

**3) Which service provides sign-up / sign-in for mobile apps?**
- A) Shield
- B) Macie
- C) Inspector
- D) Cognito ✅

**4) Which service helps detect sensitive data stored in S3?**
- A) Firewall Manager
- B) IAM
- C) Macie ✅
- D) CloudHSM

---

## Final Interview Answer Framework (Use This!)

Whenever answering AWS questions, follow:

* **What is it?**
* **Why do we use it?**
* **How does it work?**
* **Common real-world use case**
* **Troubleshooting approach**