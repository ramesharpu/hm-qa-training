# GitHub Actions, Self-Hosted Runners & Hosted Runners

## Training Notes with Examples

---

# 1. Understanding GitHub Actions

[GitHub Actions Documentation](https://docs.github.com/actions?utm_source=chatgpt.com)

## What is GitHub Actions?

GitHub Actions is a CI/CD automation platform built into GitHub.

It helps automate:

* Code building
* Testing
* Deployment
* Security scanning
* Infrastructure automation

---

# Real-World Analogy

Imagine a factory assembly line.

When developers push code:

1. GitHub detects the change
2. Actions automatically start workflows
3. Tests and deployments run automatically

---

# Basic Workflow Architecture

```text id="4lq6sv"
Developer Pushes Code
        ↓
GitHub Event Triggered
        ↓
Workflow Starts
        ↓
Jobs Execute
        ↓
Steps Run Commands
        ↓
Deployment/Notification
```

---

# Core Components of GitHub Actions

| Component | Meaning                       |
| --------- | ----------------------------- |
| Workflow  | Complete automation pipeline  |
| Event     | Trigger for workflow          |
| Job       | Group of tasks                |
| Step      | Individual command/action     |
| Runner    | Machine executing workflow    |
| Action    | Reusable automation component |

---

# Example Events

| Event             | Trigger              |
| ----------------- | -------------------- |
| push              | Code pushed          |
| pull_request      | PR created           |
| schedule          | Cron-based execution |
| workflow_dispatch | Manual trigger       |

---

# Example Simple Workflow

```yaml id="e0jxpv"
name: NodeJS CI

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

| Section | Purpose         |
| ------- | --------------- |
| name    | Workflow name   |
| on      | Trigger event   |
| jobs    | Work sections   |
| runs-on | Runner OS       |
| uses    | Reusable action |
| run     | Shell command   |

---

# Benefits of GitHub Actions

* Native GitHub integration
* Easy automation
* Faster delivery
* Reduced manual work
* Supports CI/CD
* Cloud and on-prem support

---

# 2. Creating Custom Workflows Using Actions

---

# What is a Custom Workflow?

A custom workflow is a user-defined automation pipeline.

Stored inside:

```text id="frlkd2"
.github/workflows/
```

---

# Example Scenario

When code is pushed:

1. Run tests
2. Build Docker image
3. Deploy to Kubernetes

---

# Example Custom Workflow

```yaml id="0t3vtx"
name: CI-CD Pipeline

on:
  push:
    branches:
      - main

jobs:

  test:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - name: Install NodeJS
        uses: actions/setup-node@v4
        with:
          node-version: 20

      - name: Install Packages
        run: npm install

      - name: Run Unit Tests
        run: npm test

  docker-build:
    needs: test
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - name: Build Docker Image
        run: docker build -t myapp:v1 .
```

---

# Understanding Workflow Dependencies

```yaml id="5xxk22"
needs: test
```

Meaning:

* Run this job only after test job succeeds.

---

# Using Secrets in Workflows

Sensitive data should never be hardcoded.

Use GitHub Secrets:

* API keys
* Passwords
* Tokens

Example:

```yaml id="0d1uv7"
env:
  DOCKER_PASSWORD: ${{ secrets.DOCKER_PASSWORD }}
```

---

# Reusable GitHub Actions

GitHub Marketplace provides reusable actions.

Examples:

* Checkout code
* Setup Java
* Docker login
* Kubernetes deployment

Marketplace:
[GitHub Marketplace](https://github.com/marketplace?type=actions&utm_source=chatgpt.com)

---

# Example Reusable Action

```yaml id="khz2xh"
- uses: actions/checkout@v4
```

Purpose:
Downloads repository code into runner.

---

# 3. Runners in GitHub Actions

---

# What is a Runner?

A runner is the machine that executes workflow jobs.

Without runners:

* Workflows cannot execute.

---

# Types of Runners

| Type               | Managed By        |
| ------------------ | ----------------- |
| Hosted Runner      | GitHub            |
| Self-Hosted Runner | User/Organization |

---

# Runner Workflow

```text id="8oqvlt"
Workflow Triggered
        ↓
Runner Picks Job
        ↓
Executes Commands
        ↓
Returns Results to GitHub
```

---

# 4. Self-Hosted Runners

[Self-Hosted Runners Documentation](https://docs.github.com/actions/hosting-your-own-runners/about-self-hosted-runners?utm_source=chatgpt.com)

---

# What is a Self-Hosted Runner?

A machine managed by you that executes GitHub Actions jobs.

Can run on:

* Physical servers
* Virtual machines
* Cloud instances
* Kubernetes pods

---

# Why Use Self-Hosted Runners?

## 1. Full Control

Customize:

* Hardware
* OS
* Installed tools

---

## 2. Internal Network Access

Useful for:

* Private databases
* Internal APIs
* Corporate systems

---

## 3. Better Performance

Can use:

* High CPU
* GPU
* Large memory servers

---

## 4. Cost Optimization

For heavy workloads, self-hosted may reduce cloud costs.

---

# Self-Hosted Runner Architecture

```text id="sajbxk"
GitHub Repository
        ↓
Workflow Trigger
        ↓
Self-Hosted Runner
(Your VM/Server)
        ↓
Executes Jobs
```

---

# Setting Up a Self-Hosted Runner

---

# Step 1: Navigate to Repository Settings

```text id="gqkh2j"
Repository → Settings → Actions → Runners
```

---

# Step 2: Add New Runner

GitHub generates:

* Download commands
* Registration token

---

# Step 3: Install Runner

Example Linux setup:

```bash id="n8u0li"
mkdir actions-runner && cd actions-runner

curl -o actions-runner-linux-x64.tar.gz -L \
https://github.com/actions/runner/releases/download/v2.317.0/actions-runner-linux-x64-2.317.0.tar.gz

tar xzf ./actions-runner-linux-x64.tar.gz
```

---

# Step 4: Configure Runner

```bash id="8e1h38"
./config.sh --url https://github.com/myorg/myrepo --token TOKEN
```

---

# Step 5: Start Runner

```bash id="5bbfjlwm"
./run.sh
```

---

# Using Self-Hosted Runner in Workflow

```yaml id="qsl6nx"
runs-on: self-hosted
```

---

# Example with Labels

```yaml id="nv2f4o"
runs-on: [self-hosted, linux, docker]
```

Meaning:

* Select runner matching these labels.

---

# Self-Hosted Runner Use Cases

| Use Case              | Why Self-Hosted?          |
| --------------------- | ------------------------- |
| Internal deployment   | Access private network    |
| GPU workloads         | Custom hardware           |
| Enterprise compliance | Full control              |
| Large builds          | High-performance machines |

---

# Advantages of Self-Hosted Runners

| Advantage      | Explanation             |
| -------------- | ----------------------- |
| Customization  | Install any tools       |
| Network access | Reach private resources |
| Performance    | Use powerful machines   |
| Flexibility    | Any environment         |

---

# Disadvantages of Self-Hosted Runners

| Disadvantage | Explanation                      |
| ------------ | -------------------------------- |
| Maintenance  | You manage updates               |
| Security     | You secure systems               |
| Scaling      | Manual infrastructure management |
| Availability | Your responsibility              |

---

# 5. Hosted Runners

[Hosted Runners Documentation](https://docs.github.com/actions/using-github-hosted-runners/about-github-hosted-runners?utm_source=chatgpt.com)

---

# What are Hosted Runners?

Pre-configured virtual machines managed by GitHub.

GitHub automatically:

* Creates VM
* Runs workflow
* Cleans up VM after execution

---

# Available Hosted Environments

| Runner         | OS      |
| -------------- | ------- |
| ubuntu-latest  | Linux   |
| windows-latest | Windows |
| macos-latest   | macOS   |

---

# Example Hosted Runner

```yaml id="7z4u8q"
runs-on: ubuntu-latest
```

---

# Benefits of Hosted Runners

## 1. No Maintenance

GitHub handles:

* Updates
* Security patches
* Scaling

---

## 2. Quick Setup

No infrastructure setup needed.

---

## 3. Elastic Scaling

Multiple workflows run simultaneously.

---

## 4. Pre-installed Tools

Includes:

* Docker
* NodeJS
* Python
* Java
* Git

---

# Hosted Runner Workflow Example

```yaml id="ot7hva"
name: Python CI

on: push

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - name: Setup Python
        uses: actions/setup-python@v5
        with:
          python-version: "3.12"

      - name: Install Dependencies
        run: pip install -r requirements.txt

      - name: Run Tests
        run: pytest
```

---

# Hosted Runner Lifecycle

```text id="7dt2cu"
Workflow Starts
        ↓
GitHub Creates Temporary VM
        ↓
Workflow Executes
        ↓
VM Destroyed Automatically
```

---

# Hosted Runner Limitations

| Limitation            | Explanation                   |
| --------------------- | ----------------------------- |
| Limited customization | Cannot fully control machine  |
| Public internet only  | No internal network access    |
| Usage limits          | Minutes quota applies         |
| Shared environment    | Less control than self-hosted |

---

# 6. Hosted vs Self-Hosted Runners

| Feature                 | Hosted Runner | Self-Hosted Runner |
| ----------------------- | ------------- | ------------------ |
| Managed by              | GitHub        | User               |
| Maintenance             | GitHub        | User               |
| Customization           | Limited       | Full               |
| Internal access         | No            | Yes                |
| Scaling                 | Automatic     | Manual             |
| Setup complexity        | Easy          | Medium/High        |
| Security responsibility | Shared        | Mostly user        |

---

# Which Runner Should You Choose?

---

# Use Hosted Runners When

* Small/medium projects
* Open-source projects
* Quick CI setup
* Standard workloads

---

# Use Self-Hosted Runners When

* Enterprise environments
* Internal deployments
* GPU/large compute needs
* Compliance requirements
* Private network access required

---

# Real Enterprise Example

## Banking Application

### Hosted Runners

Used for:

* Unit tests
* Linting
* Open-source scanning

### Self-Hosted Runners

Used for:

* Internal deployment
* Database migrations
* Production release automation

---

# End-to-End GitHub Actions Pipeline Example

```text id="hxxmq2"
Developer Pushes Code
        ↓
GitHub Actions Triggered
        ↓
Hosted Runner Executes Tests
        ↓
Docker Image Built
        ↓
Self-Hosted Runner Deploys to Internal Kubernetes Cluster
        ↓
Monitoring & Notifications
```

---

# Key Takeaways

| Topic                | Important Idea                   |
| -------------------- | -------------------------------- |
| GitHub Actions       | CI/CD automation platform        |
| Workflow             | YAML-based automation            |
| Hosted Runner        | GitHub-managed execution machine |
| Self-Hosted Runner   | User-managed execution machine   |
| Hosted Benefits      | Easy and scalable                |
| Self-Hosted Benefits | Full control and private access  |
| CI/CD                | Automated software delivery      |
