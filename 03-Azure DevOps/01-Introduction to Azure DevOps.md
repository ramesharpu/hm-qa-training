# DevOps Training Content

## Foundations of Azure & Azure DevOps

---

# 1. Introduction to Azure

## What is Azure?

Microsoft Azure is a cloud computing platform developed by Microsoft that provides services for building, deploying, and managing applications through Microsoft-managed data centers.

Azure offers:

* Virtual Machines (VMs)
* Storage Solutions
* Networking
* Databases
* AI & Machine Learning
* DevOps Services
* Security & Monitoring
* Containers & Kubernetes

---

## Why Cloud Computing?

Traditional infrastructure requires:

* Physical servers
* Manual maintenance
* High upfront costs
* Limited scalability

Cloud computing solves these problems by offering:

| Traditional Infrastructure | Cloud Infrastructure |
| -------------------------- | -------------------- |
| Expensive hardware         | Pay-as-you-go        |
| Manual scaling             | Auto scaling         |
| Slow deployment            | Rapid deployment     |
| Limited accessibility      | Global access        |

---

## Types of Cloud Models

### 1. Public Cloud

Infrastructure shared over the internet.

Examples:

* Azure
* AWS
* GCP

### 2. Private Cloud

Dedicated infrastructure for one organization.

### 3. Hybrid Cloud

Combination of public and private cloud.

---

## Core Azure Services

| Category   | Services                       |
| ---------- | ------------------------------ |
| Compute    | Virtual Machines, App Services |
| Storage    | Blob Storage, File Storage     |
| Networking | Virtual Network, Load Balancer |
| Databases  | Azure SQL, Cosmos DB           |
| DevOps     | Azure DevOps                   |
| Containers | AKS (Azure Kubernetes Service) |

---

## Benefits of Azure

* High Availability
* Scalability
* Security
* Global Presence
* Cost Optimization
* Integration with Microsoft Products

---

# 2. Introduction to DevOps

## What is DevOps?

DevOps is a culture, practice, and set of tools that combines:

* Development (Dev)
* Operations (Ops)

to improve collaboration and automate software delivery.

---

## Traditional Software Development Challenges

Before DevOps:

* Developers and operations worked separately
* Manual deployments
* Slow releases
* Frequent failures
* Difficult rollback process

---

## DevOps Lifecycle

```text
Plan → Develop → Build → Test → Release → Deploy → Operate → Monitor
```

---

## Key DevOps Principles

### 1. Automation

Automating repetitive tasks like:

* Build
* Testing
* Deployment
* Monitoring

### 2. Continuous Integration (CI)

Developers frequently merge code changes.

### 3. Continuous Delivery (CD)

Applications are automatically prepared for release.

### 4. Continuous Monitoring

Track application performance and issues.

### 5. Collaboration

Development and Operations teams work together.

---

## Benefits of DevOps

| Benefit                | Description             |
| ---------------------- | ----------------------- |
| Faster Delivery        | Quick software releases |
| Better Quality         | Reduced bugs            |
| Improved Collaboration | Team alignment          |
| Faster Recovery        | Quick issue resolution  |
| Automation             | Reduced manual work     |

---

## Popular DevOps Tools

| Area           | Tools                    |
| -------------- | ------------------------ |
| Source Control | Git, GitHub, Azure Repos |
| CI/CD          | Jenkins, Azure Pipelines |
| Containers     | Docker                   |
| Orchestration  | Kubernetes               |
| Configuration  | Ansible, Terraform       |
| Monitoring     | Prometheus, Grafana      |

---

# 3. Introduction to Azure DevOps

## What is Azure DevOps?

Azure DevOps is a suite of development tools provided by Microsoft to support the complete DevOps lifecycle.

---

## Azure DevOps Services

### 1. Azure Repos

Git repositories for source control.

### 2. Azure Pipelines

CI/CD pipelines for automated builds and deployments.

### 3. Azure Boards

Agile project management tool.

### 4. Azure Test Plans

Testing management solution.

### 5. Azure Artifacts

Package management system.

---

## Azure DevOps Architecture

```text
Developer → Azure Repos → Azure Pipelines → Deployment → Monitoring
```

---

## Features of Azure DevOps

* End-to-End DevOps Solution
* Cloud-based and On-premises Support
* Integration with GitHub and Jenkins
* Agile Planning Tools
* Automated Testing
* Multi-platform Support

---

## Advantages of Azure DevOps

| Feature          | Benefit             |
| ---------------- | ------------------- |
| CI/CD Automation | Faster deployments  |
| Integrated Tools | Simplified workflow |
| Agile Management | Better tracking     |
| Security         | Access control      |
| Scalability      | Enterprise-ready    |

---

# 4. Introduction to Transformation Planning

## What is Transformation Planning?

Transformation planning is the process of moving from traditional software development practices to modern DevOps and cloud-based methodologies.

---

## Goals of Transformation

* Faster delivery
* Automation
* Cloud adoption
* Better collaboration
* Improved scalability
* Reduced operational cost

---

## Stages of DevOps Transformation

### Stage 1: Assessment

Analyze current infrastructure and processes.

### Stage 2: Planning

Define:

* Tools
* Architecture
* Migration strategy
* Team responsibilities

### Stage 3: Implementation

Adopt:

* CI/CD
* Source control
* Infrastructure automation

### Stage 4: Optimization

Improve performance and monitoring.

---

## Important Considerations

| Area       | Focus                   |
| ---------- | ----------------------- |
| Culture    | Team collaboration      |
| Tools      | Automation tools        |
| Security   | DevSecOps               |
| Training   | Skill development       |
| Governance | Policies and compliance |

---

## Common Challenges

* Resistance to change
* Legacy systems
* Skill gaps
* Security concerns
* Process complexity

---

# 5. Introduction to Source Control

## What is Source Control?

Source control (Version Control System) helps track and manage code changes over time.

---

## Why Source Control?

Without source control:

* Code overwriting
* No change history
* Difficult collaboration
* Hard rollback process

---

## Benefits of Source Control

| Benefit          | Description                           |
| ---------------- | ------------------------------------- |
| Version Tracking | Track all changes                     |
| Collaboration    | Multiple developers can work together |
| Backup           | Code stored safely                    |
| Branching        | Parallel development                  |
| Rollback         | Restore previous versions             |

---

## Types of Version Control

### 1. Centralized Version Control

Example:

* SVN

### 2. Distributed Version Control

Examples:

* Git
* Mercurial

---

## What is Git?

Git is a distributed version control system used to manage source code.

---

## Common Git Concepts

| Concept    | Description                     |
| ---------- | ------------------------------- |
| Repository | Code storage location           |
| Commit     | Saved change                    |
| Branch     | Independent line of development |
| Merge      | Combine branches                |
| Clone      | Copy repository                 |
| Push       | Upload changes                  |
| Pull       | Download changes                |

---

## Basic Git Workflow

```text
Working Directory → Staging Area → Local Repository → Remote Repository
```

---

# 6. Migrating to Azure DevOps

## Why Migrate to Azure DevOps?

Organizations migrate to Azure DevOps for:

* Better collaboration
* Centralized platform
* CI/CD automation
* Agile planning
* Cloud integration

---

## Migration Sources

You can migrate from:

* Jenkins
* GitHub
* SVN
* TFS
* Bitbucket

---

## Migration Components

| Component       | Migration Target |
| --------------- | ---------------- |
| Source Code     | Azure Repos      |
| Build Pipelines | Azure Pipelines  |
| Work Items      | Azure Boards     |
| Packages        | Azure Artifacts  |

---

## Migration Steps

### Step 1: Assessment

Review:

* Existing repositories
* Pipelines
* Dependencies

### Step 2: Planning

Define:

* Migration strategy
* Downtime
* Security policies

### Step 3: Migration Execution

Move:

* Code
* Pipelines
* Users
* Permissions

### Step 4: Validation

Verify:

* Repository integrity
* Pipeline execution
* Access controls

---

## Best Practices

* Start with pilot projects
* Backup repositories
* Train teams
* Automate migration where possible
* Monitor post-migration issues

---

# 7. Git Authentication in Azure Repos

## What is Azure Repos?

Azure Repos provides Git repositories for source code management in Azure DevOps.

---

## Authentication Methods in Azure Repos

### 1. Personal Access Token (PAT)

Used instead of passwords.

### 2. SSH Authentication

Secure communication using SSH keys.

### 3. Azure Active Directory Authentication

Enterprise authentication using Microsoft accounts.

---

# Personal Access Token (PAT)

## Steps to Create PAT

1. Login to Azure DevOps
2. Open User Settings
3. Select Personal Access Tokens
4. Create New Token
5. Choose permissions
6. Copy generated token

---

## Clone Repository Using PAT

```bash
git clone https://<organization>@dev.azure.com/<organization>/<project>/_git/<repo>
```

When prompted:

* Username → anything
* Password → PAT Token

---

# SSH Authentication

## Generate SSH Key

```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

---

## Add SSH Key to Azure DevOps

1. Copy public key
2. Open Azure DevOps
3. User Settings → SSH Public Keys
4. Add Key

---

## Clone Using SSH

```bash
git clone git@ssh.dev.azure.com:v3/organization/project/repository
```

---

# Best Practices for Git Authentication

* Use PAT instead of passwords
* Rotate tokens regularly
* Use SSH for secure automation
* Apply least privilege access
* Enable MFA

---

# Summary

In this module, we covered:

* Azure fundamentals
* DevOps basics
* Azure DevOps overview
* Transformation planning
* Source control concepts
* Migration strategies
* Git authentication methods

This foundation prepares learners for advanced Azure DevOps topics like:

* CI/CD Pipelines
* Infrastructure as Code
* Kubernetes
* Monitoring & Logging
* DevSecOps
* Release Management
