# Software Development & Deployment Notes

## Training Notes with Examples

---

# 1. What Happens After Code is Written? (Deployment Overview)

After developers write code, the application goes through several stages before users can use it safely in production.

## Typical Software Delivery Flow

```text
Code → Build → Test → Package → Deploy → Monitor → Maintain
```

---

## Step-by-Step Explanation

### 1. Code Development

Developers write code using languages like:

* Java
* Python
* JavaScript
* Go

Example:
A developer creates a login feature for an e-commerce app.

---

### 2. Version Control (Git)

Code is pushed to Git repositories.

Common platforms:

* GitHub
* GitLab
* Bitbucket

Purpose:

* Track changes
* Collaborate
* Rollback if needed

Example:

```bash
git add .
git commit -m "Added login validation"
git push origin main
```

---

### 3. Build Process

Source code is converted into executable artifacts.

Examples:

* Java → JAR/WAR
* React → Static bundle
* Docker → Container image

Tools:

* Maven
* Gradle
* npm
* Docker

---

### 4. Automated Testing

Tests verify whether the application works correctly.

Types:

* Unit Testing
* Integration Testing
* UI Testing
* Security Testing

Example:
Checking whether login accepts valid credentials.

---

### 5. CI/CD Pipeline

Automation tools execute:

* Build
* Test
* Deploy

Tools:

* GitHub Actions
* Jenkins
* GitLab CI
* Azure DevOps

---

### 6. Deployment

Application is deployed to environments:

* Dev
* Test
* Staging
* Production

Deployment methods:

* VM deployment
* Docker containers
* Kubernetes
* Serverless

---

### 7. Monitoring & Observability

Teams monitor:

* Errors
* CPU
* Memory
* Logs
* User traffic

Tools:

* Prometheus
* Grafana
* Datadog
* ELK Stack

---

# Real-World Example

Food delivery app deployment:

1. Developer writes coupon code feature
2. Pushes code to GitHub
3. GitHub Actions runs tests
4. Docker image created
5. Kubernetes deploys app
6. Monitoring detects failures if any

---

# 2. Cost of Failure: Why Apps Crash and Impact on Users

Application failures can cause:

* Revenue loss
* Customer frustration
* Brand damage
* Security issues

---

# Common Reasons Applications Crash

## 1. Coding Bugs

Example:
Null pointer exception causes app crash.

---

## 2. Infrastructure Failure

Example:
Server disk becomes full.

---

## 3. High Traffic

Example:
Flash sale overloads servers.

---

## 4. Database Failure

Example:
Database connection timeout.

---

## 5. Deployment Errors

Example:
Incorrect configuration deployed.

---

# Business Impact of Downtime

| Problem                  | Impact               |
| ------------------------ | -------------------- |
| Banking app down         | Transaction failures |
| E-commerce outage        | Revenue loss         |
| Healthcare system crash  | Patient risk         |
| Streaming service outage | User dissatisfaction |

---

# Famous Example

Facebook outage 2021

Services including:

* Facebook
* Instagram
* WhatsApp

were unavailable for several hours due to network configuration issues.

Impact:

* Millions of users affected
* Huge financial loss
* Operational disruption

---

# 3. User Experience: Functionality (QA) vs Uptime (SRE)

Both QA and SRE are important but focus on different goals.

---

# QA (Quality Assurance)

Focus:
“Does the application work correctly?”

Checks:

* Features
* UI
* Business logic
* Bugs

Example:
Testing login functionality.

---

# SRE (Site Reliability Engineering)

Focus:
“Is the application reliable and available?”

Checks:

* Availability
* Scalability
* Performance
* Recovery

Example:
Ensuring login service works during peak traffic.

---

# QA vs SRE Comparison

| QA                     | SRE                      |
| ---------------------- | ------------------------ |
| Functional correctness | Reliability              |
| Finds bugs             | Prevents outages         |
| Tests features         | Monitors uptime          |
| User workflows         | Infrastructure stability |

---

# Example Scenario

## QA Validation

* Login button works
* Password reset works

## SRE Validation

* Can system handle 1 million users?
* What if server crashes?

---

# 4. Shared Responsibility Model

Modern systems require collaboration among multiple teams.

Everyone shares responsibility for application success.

---

# Teams Involved

| Team           | Responsibility              |
| -------------- | --------------------------- |
| Developers     | Code quality                |
| QA             | Testing                     |
| DevOps         | Deployment automation       |
| SRE            | Reliability                 |
| Security       | Vulnerability management    |
| Cloud Provider | Infrastructure availability |

---

# Cloud Shared Responsibility Example

Using [Amazon Web Services](https://aws.amazon.com/?utm_source=chatgpt.com)

## AWS Handles

* Physical hardware
* Networking
* Data center security

## Customer Handles

* Application security
* User access
* Data encryption
* OS patching (depending on service)

---

# Analogy

Apartment example:

* Building security = Cloud provider
* Locking your apartment = Customer responsibility

---

# 5. SDLC vs STLC vs Deployment Cycle

---

# SDLC (Software Development Life Cycle)

Complete software development process.

Stages:

1. Requirement gathering
2. Design
3. Development
4. Testing
5. Deployment
6. Maintenance

---

# STLC (Software Testing Life Cycle)

Focused only on testing activities.

Stages:

1. Requirement analysis
2. Test planning
3. Test case creation
4. Environment setup
5. Test execution
6. Bug reporting

---

# Deployment Cycle

Focused on releasing software safely.

Stages:

1. Build
2. Package
3. Deploy
4. Verify
5. Rollback (if needed)

---

# Comparison Table

| SDLC                      | STLC                | Deployment Cycle    |
| ------------------------- | ------------------- | ------------------- |
| Entire software lifecycle | Testing lifecycle   | Release lifecycle   |
| Includes coding           | Includes validation | Includes deployment |
| Business focused          | Quality focused     | Operations focused  |

---

# 6. Environments: Dev, Test, Staging, Production

Applications move through multiple environments before production.

---

# 1. Development Environment (Dev)

Purpose:
Developers write and test code.

Characteristics:

* Frequent changes
* Unstable sometimes

Example:
Developer testing new APIs.

---

# 2. Test Environment

Purpose:
QA team validates features.

Characteristics:

* Test data
* Automated testing

Example:
Testing payment workflow.

---

# 3. Staging Environment

Purpose:
Production-like validation.

Characteristics:

* Mirrors production
* Final verification

Example:
Load testing before release.

---

# 4. Production Environment

Purpose:
Real users access application.

Characteristics:

* Stable
* Highly monitored

Example:
Live banking application.

---

# Environment Flow

```text
Dev → Test → Staging → Production
```

---

# Real Example

For a shopping app:

| Environment | Purpose               |
| ----------- | --------------------- |
| Dev         | Developer experiments |
| Test        | QA testing            |
| Staging     | Simulate real users   |
| Production  | Customers shop        |

---

# 7. Version Control (Git) as the Source of Truth

Git stores complete application history.

It becomes the “single source of truth” for:

* Code
* Configuration
* Infrastructure definitions

---

# Benefits of Git

## 1. Change Tracking

See who changed what.

---

## 2. Collaboration

Multiple developers work together.

---

## 3. Rollback

Restore previous versions.

---

## 4. Branching

Develop features independently.

Example:

```bash
git checkout -b feature/payment
```

---

# Git Workflow Example

```text
Developer → Commit → Push → Pull Request → Merge
```

---

# GitOps Concept

Infrastructure is also stored in Git.

Example:
Kubernetes YAML files stored in Git repository.

Benefits:

* Auditability
* Consistency
* Easy rollback

---

# 8. GitHub Actions Workflows

[GitHub Actions Documentation](https://docs.github.com/actions?utm_source=chatgpt.com)

GitHub Actions automates:

* Build
* Testing
* Deployment

---

# What is a Workflow?

A workflow is an automated pipeline defined in YAML.

Location:

```text
.github/workflows/
```

---

# Example Workflow

```yaml
name: CI Pipeline

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Code
        uses: actions/checkout@v4

      - name: Install Dependencies
        run: npm install

      - name: Run Tests
        run: npm test
```

---

# Workflow Explanation

| Section | Purpose           |
| ------- | ----------------- |
| on      | Trigger event     |
| jobs    | Tasks to run      |
| steps   | Commands executed |
| runs-on | Runner OS         |

---

# Real CI/CD Flow Using GitHub Actions

```text
Developer Pushes Code
        ↓
GitHub Actions Triggered
        ↓
Build Application
        ↓
Run Tests
        ↓
Create Docker Image
        ↓
Deploy to Kubernetes
```

---

# Benefits of GitHub Actions

* Automation
* Faster releases
* Reduced manual effort
* Better reliability
* Easy integration with GitHub

---

# Key Takeaways

| Topic                 | Important Idea                        |
| --------------------- | ------------------------------------- |
| Deployment Overview   | Code goes through build, test, deploy |
| Failures              | Downtime impacts business heavily     |
| QA vs SRE             | Functionality vs Reliability          |
| Shared Responsibility | Multiple teams ensure success         |
| SDLC/STLC             | Different lifecycle perspectives      |
| Environments          | Safe progression before production    |
| Git                   | Source of truth                       |
| GitHub Actions        | CI/CD automation                      |
