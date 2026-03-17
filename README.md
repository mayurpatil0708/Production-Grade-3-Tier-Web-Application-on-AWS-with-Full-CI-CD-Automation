---


# 🚀 AWS 3-Tier Architecture with CI/CD, Auto Scaling & Load Balancing

This project demonstrates a **production-style deployment of a full-stack application on AWS** using a **3-tier architecture integrated with CI/CD pipelines and Auto Scaling**.

It focuses on **scalability, high availability, automation, and secure infrastructure design**.

---

## 📌 Project Overview

This system is built using a standard **3-tier architecture**:

- **Web Tier (Frontend)** → React + Nginx  
- **Application Tier (Backend)** → Node.js + Express  
- **Database Tier** → MySQL (Amazon RDS)

The deployment is fully automated using AWS CI/CD services.

---

## 🏗️ Architecture Flow

```

User → External ALB → Web Tier (ASG)
↓
Internal ALB → App Tier (ASG)
↓
RDS (MySQL)

```

---

## 🔧 AWS Services Used

- VPC (Custom Networking)
- EC2 (Web & App servers)
- Auto Scaling Groups (ASG)
- Application Load Balancer (External & Internal)
- RDS MySQL
- S3 (Artifacts storage)
- IAM Roles
- SSM Parameter Store (Secrets management)
- NAT Gateway & Internet Gateway
- CodePipeline
- CodeBuild
- CodeDeploy
- CloudWatch Logs

---

## 🌐 Networking Design

### VPC
- CIDR Block: `192.168.0.0/16`

### Subnets

| Layer        | Subnet CIDR         |
|-------------|---------------------|
| Public      | 192.168.1.0/24, 192.168.2.0/24 |
| Web Tier    | 192.168.3.0/24, 192.168.4.0/24 |
| App Tier    | 192.168.5.0/24, 192.168.6.0/24 |
| Database    | 192.168.7.0/24, 192.168.8.0/24 |

### Routing

- Public Subnets → Internet Gateway (IGW)
- Private Subnets → NAT Gateway

---

## 🔐 Security Design

- Security Groups used for controlled communication:
  - Web ALB → Web Servers
  - Web Servers → App ALB
  - App ALB → App Servers
  - App Servers → Database

- Database is:
  - Not publicly accessible
  - Only accessible from App Tier

---

## ⚙️ Auto Scaling Configuration

- Auto Scaling Groups for:
  - Web Tier
  - Application Tier

- Configuration:
  - Min: 1
  - Max: 4
  - Desired: 2

- Scaling Policy:
  - Target Tracking based on CPU Utilization (70%)

- Benefits:
  - High availability
  - Self-healing infrastructure
  - Automatic scaling based on load

---

## 🔄 CI/CD Pipeline

### Tools Used:
- CodePipeline → Orchestration
- CodeBuild → Build & test
- CodeDeploy → Deployment

---

### Backend Pipeline

1. Code pushed to GitHub
2. Trigger CodePipeline
3. CodeBuild runs backend buildspec
4. Artifacts stored in S3
5. CodeDeploy deploys to App Tier ASG

---

### Frontend Pipeline

1. Code pushed to GitHub
2. Trigger CodePipeline
3. CodeBuild runs frontend buildspec
4. Artifacts stored in S3
5. CodeDeploy deploys to Web Tier ASG

---

## 📦 S3 Buckets

- Code storage bucket
- CodeBuild artifacts bucket (private)

---

## 🔑 Parameter Store (SSM)

Used to securely store:

- DB_HOST
- DB_USER
- DB_PASSWORD
- DB_NAME
- DB_PORT

Benefits:
- Avoid hardcoding credentials
- Secure access during build & deployment

---

## 🖥️ Load Balancers

### External ALB
- Internet-facing
- Routes traffic to Web Tier

### Internal ALB
- Private
- Routes traffic to Application Tier

---

## 🗄️ Database

- Engine: MySQL (Amazon RDS)
- Deployed in private subnets
- Not publicly accessible
- Connected securely via security groups

---

## 📊 Logging & Monitoring

- CloudWatch Logs used for:
  - Application logs
  - CodeBuild logs
  - System logs

---

## 🚀 Key Features

- Fully automated CI/CD pipeline
- Scalable architecture using Auto Scaling
- Secure networking with private subnets
- Separation of concerns (3-tier design)
- Load-balanced high availability setup
- Secrets managed via SSM Parameter Store

---

## ⚠️ Current Limitations

- IAM roles use broad permissions (can be restricted further)

---

## 🔜 Future Improvements

- Add CloudFront (CDN)
- Add Route53 (custom domain)
- Implement HTTPS (SSL/TLS)
- Use least-privilege IAM roles
- Add monitoring alerts (CloudWatch Alarms)

---

## 📚 Learnings

- Real-world AWS architecture design
- CI/CD automation across multiple tiers
- Debugging distributed systems
- Networking concepts (NAT, IGW, subnets, routing)
- Secure handling of application secrets

---

## 👨‍💻 Author

**Mayur Patil**  
Final Year IT Student | DevOps & Cloud Enthusiast  


## ⭐ If you found this helpful, consider giving it a star!


---

