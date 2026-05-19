# Advanced GitHub Actions & Secure CI/CD

## Training Notes with Examples

---

# 1. Diving Deeper into GitHub Actions

[GitHub Actions Documentation](https://docs.github.com/actions?utm_source=chatgpt.com)

GitHub Actions becomes extremely powerful when workflows:

* React to events
* Use secrets securely
* Integrate with cloud tools
* Perform automated security checks

---

# GitHub Actions Architecture Overview

```text id="jkk0r7"
GitHub Event
     ↓
Workflow Triggered
     ↓
Runner Executes Jobs
     ↓
External Tools/Cloud Integration
     ↓
Deployment + Security Validation
```

---

# 2. Trigger Workflows Based on Events

---

# What is an Event?

An event is an activity that triggers a workflow.

Examples:

* Code push
* Pull request
* Tag creation
* Release publishing
* Manual execution

---

# Common GitHub Actions Events

| Event             | Triggered When        |
| ----------------- | --------------------- |
| push              | Code pushed           |
| pull_request      | PR created/updated    |
| workflow_dispatch | Manual trigger        |
| schedule          | Scheduled cron job    |
| release           | New release published |
| issues            | Issue created         |
| fork              | Repository forked     |

---

# Example 1: Trigger on Push

```yaml id="b78vv2"
on:
  push:
    branches:
      - main
```

Meaning:

* Run workflow whenever code is pushed to main branch.

---

# Example 2: Trigger on Pull Request

```yaml id="0o34h6"
on:
  pull_request:
    branches:
      - main
```

Use Case:

* Run tests before merging code.

---

# Example 3: Multiple Events

```yaml id="aqd0qs"
on:
  push:
    branches:
      - main

  pull_request:
    branches:
      - main
```

Meaning:

* Trigger workflow on both push and PR.

---

# Example 4: Scheduled Workflow

```yaml id="67q2oz"
on:
  schedule:
    - cron: "0 2 * * *"
```

Meaning:

* Run daily at 2 AM UTC.

Use Cases:

* Backup jobs
* Security scans
* Cleanup tasks

---

# Example 5: Manual Trigger

```yaml id="t1ihhu"
on:
  workflow_dispatch:
```

Meaning:

* User manually starts workflow from GitHub UI.

---

# Real Enterprise Example

## Banking Application

| Event        | Action                     |
| ------------ | -------------------------- |
| push         | Run unit tests             |
| pull_request | Run security scans         |
| release      | Deploy production          |
| schedule     | Nightly vulnerability scan |

---

# 3. Environment Variables in GitHub Actions

---

# What are Environment Variables?

Variables used to store reusable values.

Examples:

* App names
* Environment names
* URLs
* Version numbers

---

# Example Workflow Variables

```yaml id="pw5s0l"
env:
  APP_NAME: payment-service
  ENVIRONMENT: production
```

---

# Using Variables

```yaml id="nvw08w"
steps:
  - name: Print Variables
    run: echo $APP_NAME
```

---

# Job-Level Variables

```yaml id="3s75o6"
jobs:
  build:
    env:
      NODE_ENV: production
```

---

# Step-Level Variables

```yaml id="5k4clj"
steps:
  - name: Temporary Variable
    env:
      VERSION: v1.0
```

---

# Benefits of Environment Variables

* Reusability
* Easier maintenance
* Cleaner workflows
* Centralized configuration

---

# 4. Secrets in GitHub Actions

---

# What are Secrets?

Encrypted sensitive values stored securely in GitHub.

Examples:

* API tokens
* Passwords
* Cloud credentials
* SSH keys

---

# Why Secrets Matter

Never hardcode sensitive values:

❌ Bad Practice:

```yaml id="o3g6l6"
password: mypassword123
```

✅ Correct:

```yaml id="jlwmj4"
password: ${{ secrets.DB_PASSWORD }}
```

---

# Adding Secrets

```text id="vhp5vz"
Repository
   ↓
Settings
   ↓
Secrets and Variables
   ↓
Actions
```

---

# Example Secret Usage

```yaml id="2tn0vn"
env:
  AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
  AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
```

---

# Best Practices for Secrets

| Best Practice               | Reason            |
| --------------------------- | ----------------- |
| Never print secrets in logs | Prevent leakage   |
| Rotate secrets regularly    | Reduce risk       |
| Use least privilege         | Limit access      |
| Store centrally             | Better governance |

---

# 5. Integrating GitHub Actions with Other Tools & Services

GitHub Actions integrates with:

* Cloud providers
* Docker
* Kubernetes
* Slack
* Jira
* Security tools

---

# Common Integrations

| Tool       | Purpose                   |
| ---------- | ------------------------- |
| Docker     | Container builds          |
| Kubernetes | Deployments               |
| AWS        | Cloud deployment          |
| Azure      | CI/CD pipelines           |
| Slack      | Notifications             |
| Terraform  | Infrastructure automation |

---

# Example: Docker Integration

```yaml id="c84e2y"
- name: Build Docker Image
  run: docker build -t myapp:v1 .
```

---

# Example: AWS Integration

```yaml id="yl7tbg"
- name: Configure AWS Credentials
  uses: aws-actions/configure-aws-credentials@v4
  with:
    aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
    aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
    aws-region: us-east-1
```

---

# Example: Kubernetes Deployment

```yaml id="nm7x3t"
- name: Deploy to Kubernetes
  run: kubectl apply -f deployment.yaml
```

---

# Example: Slack Notification

```yaml id="jlwm2g"
- name: Send Slack Notification
  uses: slackapi/slack-github-action@v1
```

---

# Real CI/CD Pipeline

```text id="y7es7u"
Code Push
    ↓
GitHub Actions
    ↓
Run Tests
    ↓
Build Docker Image
    ↓
Push to Container Registry
    ↓
Deploy to Kubernetes
    ↓
Send Slack Notification
```

---

# 6. Code Security and Analysis in CI/CD

---

# Why Security in CI/CD Matters

Security issues introduced during development can:

* Leak customer data
* Cause financial loss
* Allow attackers access
* Damage reputation

Modern DevOps includes:

* DevSecOps
* Shift-left security
* Automated scanning

---

# What is DevSecOps?

Security integrated into DevOps workflows.

```text id="u8pry5"
Development + Security + Operations
```

Goal:

* Detect vulnerabilities early.

---

# Security Checks in GitHub Actions

You can automate:

* Dependency scanning
* Secret detection
* Static code analysis
* Container scanning
* Infrastructure scanning

---

# 7. Implementing Security Checks in Workflows

---

# Example Security Workflow

```yaml id="p1n6eh"
name: Security Scan

on:
  pull_request:

jobs:
  security-checks:

    runs-on: ubuntu-latest

    steps:

      - uses: actions/checkout@v4

      - name: Run Dependency Audit
        run: npm audit
```

---

# What Does npm audit Do?

Checks:

* Vulnerable packages
* Known CVEs
* Dependency risks

---

# Example Output

```text id="wmqg3u"
High severity vulnerability found in lodash
```

---

# 8. Static Application Security Testing (SAST)

---

# What is SAST?

Analyzes source code for vulnerabilities without executing it.

Finds:

* SQL injection risks
* Hardcoded secrets
* Unsafe code patterns

---

# Popular SAST Tools

| Tool      | Language Support    |
| --------- | ------------------- |
| SonarQube | Multi-language      |
| CodeQL    | GitHub native       |
| Semgrep   | Fast scanning       |
| Checkmarx | Enterprise security |

---

# Example: GitHub CodeQL

[GitHub CodeQL Documentation](https://docs.github.com/code-security/code-scanning/introduction-to-code-scanning/about-code-scanning-with-codeql?utm_source=chatgpt.com)

---

# CodeQL Workflow Example

```yaml id="6m00if"
name: CodeQL Analysis

on:
  push:
    branches: [main]

jobs:
  analyze:

    runs-on: ubuntu-latest

    permissions:
      security-events: write

    steps:
      - uses: actions/checkout@v4

      - name: Initialize CodeQL
        uses: github/codeql-action/init@v3
        with:
          languages: javascript

      - name: Autobuild
        uses: github/codeql-action/autobuild@v3

      - name: Perform Analysis
        uses: github/codeql-action/analyze@v3
```

---

# Benefits of CodeQL

* GitHub-native
* Automated security scanning
* Detects vulnerabilities early
* Integrated with pull requests

---

# 9. Dependency Vulnerability Scanning

---

# Why Dependency Scanning Matters

Applications use many third-party libraries.

Example:

```text id="00s0ao"
NodeJS App
  ↓
1000+ npm packages
```

One vulnerable package can compromise the application.

---

# Popular Dependency Scanners

| Tool                   | Purpose                 |
| ---------------------- | ----------------------- |
| npm audit              | NodeJS dependencies     |
| Snyk                   | Multi-language scanning |
| Dependabot             | Automated updates       |
| OWASP Dependency Check | Vulnerability detection |

---

# Dependabot Example

[Dependabot Documentation](https://docs.github.com/code-security/dependabot?utm_source=chatgpt.com)

Dependabot automatically:

* Detects vulnerable packages
* Creates update pull requests

---

# Example Dependabot Config

```yaml id="m89s1j"
version: 2

updates:
  - package-ecosystem: "npm"
    directory: "/"
    schedule:
      interval: "daily"
```

---

# 10. Secret Scanning

---

# What is Secret Scanning?

Detects accidentally committed secrets:

* API keys
* Tokens
* Passwords

---

# Example Risk

Developer accidentally commits:

```text id="g2sh33"
AWS_SECRET_KEY=abcd1234
```

Attackers may misuse cloud resources.

---

# GitHub Secret Scanning

[GitHub Secret Scanning Documentation](https://docs.github.com/code-security/secret-scanning/about-secret-scanning?utm_source=chatgpt.com)

GitHub can automatically detect exposed secrets.

---

# 11. Container Security Scanning

---

# Why Container Scanning?

Docker images may contain:

* Vulnerable libraries
* Outdated packages
* Malware

---

# Popular Container Security Tools

| Tool  | Purpose                          |
| ----- | -------------------------------- |
| Trivy | Container vulnerability scanning |
| Grype | Image analysis                   |
| Clair | Registry scanning                |

---

# Example Trivy Scan

```yaml id="xmu6p9"
- name: Scan Docker Image
  uses: aquasecurity/trivy-action@master
  with:
    image-ref: myapp:v1
```

---

# 12. Infrastructure as Code (IaC) Security

---

# Why IaC Security Matters

Terraform/Kubernetes misconfigurations can expose systems.

Examples:

* Public S3 buckets
* Open security groups
* Unencrypted databases

---

# IaC Security Tools

| Tool    | Purpose             |
| ------- | ------------------- |
| Checkov | Terraform scanning  |
| tfsec   | Terraform security  |
| Kubesec | Kubernetes security |

---

# Example Terraform Security Scan

```yaml id="o7jlwm"
- name: Run Checkov Scan
  uses: bridgecrewio/checkov-action@master
```

---

# 13. Best Practices for Secure Development

---

# Security Best Practices

| Best Practice                | Explanation                  |
| ---------------------------- | ---------------------------- |
| Shift-left security          | Scan early in development    |
| Use secrets manager          | Avoid hardcoded credentials  |
| Automate scans               | Reduce manual errors         |
| Principle of least privilege | Minimal required permissions |
| Enable branch protection     | Prevent unsafe merges        |
| Review pull requests         | Human validation             |
| Use signed commits           | Verify authenticity          |

---

# Secure GitHub Workflow Example

```text id="z6cwtx"
Developer Pushes Code
        ↓
Pull Request Created
        ↓
GitHub Actions Triggered
        ↓
Run Unit Tests
        ↓
Run SAST Scan
        ↓
Run Dependency Scan
        ↓
Run Container Scan
        ↓
Approval Required
        ↓
Deploy to Production
```

---

# Enterprise DevSecOps Example

## E-Commerce Platform

### CI Pipeline Includes:

* Unit testing
* SonarQube analysis
* Trivy image scanning
* Dependency audit
* Secret scanning

### Deployment Blocked If:

* Critical vulnerabilities found
* Security policy violated

---

# Key Takeaways

| Topic                 | Important Idea                 |
| --------------------- | ------------------------------ |
| Workflow Triggers     | Automate based on events       |
| Environment Variables | Reusable configuration         |
| Secrets               | Secure sensitive data          |
| Integrations          | Connect with cloud/tools       |
| DevSecOps             | Security integrated into CI/CD |
| SAST                  | Scan source code               |
| Dependency Scanning   | Detect vulnerable libraries    |
| Secret Scanning       | Prevent credential leakage     |
| Container Security    | Scan Docker images             |
| IaC Security          | Secure Terraform/Kubernetes    |
