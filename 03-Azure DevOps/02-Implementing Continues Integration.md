# DevOps Training Content

# Module 2: Azure Pipelines & CI Implementation

---

# 1. DevOps Pipeline

## What is a DevOps Pipeline?

A DevOps Pipeline is an automated workflow that enables software applications to move through different stages of development and deployment efficiently.

The pipeline automates:

* Code integration
* Build process
* Testing
* Deployment
* Monitoring

---

## Purpose of DevOps Pipeline

The main objectives are:

* Faster software delivery
* Reduced manual work
* Improved software quality
* Consistent deployments
* Early bug detection

---

## Typical DevOps Pipeline Stages

```text id="c4l9fx"
Code → Build → Test → Release → Deploy → Monitor
```

---

## Pipeline Workflow Explanation

| Stage   | Description                    |
| ------- | ------------------------------ |
| Code    | Developers commit code         |
| Build   | Application is compiled        |
| Test    | Automated tests run            |
| Release | Package prepared               |
| Deploy  | Application deployed           |
| Monitor | Performance and logs monitored |

---

## Benefits of DevOps Pipelines

* Faster Releases
* Automated Testing
* Improved Collaboration
* Reduced Human Errors
* Better Reliability
* Continuous Feedback

---

## CI/CD Pipeline

### Continuous Integration (CI)

Automatically build and test code after every commit.

### Continuous Delivery (CD)

Automatically prepare applications for deployment.

### Continuous Deployment

Automatically deploy applications to production.

---

# 2. Azure Pipeline

## What is Azure Pipeline?

Azure Pipelines is a cloud-based CI/CD service provided by Microsoft that automates building, testing, and deploying applications.

It supports:

* Any language
* Any platform
* Any cloud

---

## Features of Azure Pipelines

* Multi-platform support
* YAML-based pipelines
* Parallel jobs
* Docker & Kubernetes integration
* Deployment automation
* Secure secret management

---

## Azure Pipeline Architecture

```text id="9kx4vd"
Developer Commit → Azure Repos/GitHub → Azure Pipeline → Build/Test → Deploy
```

---

## Components of Azure Pipeline

| Component | Purpose                  |
| --------- | ------------------------ |
| Pipeline  | Workflow automation      |
| Agent     | Executes pipeline jobs   |
| Stage     | Logical pipeline section |
| Job       | Group of tasks           |
| Task      | Individual operation     |
| Artifact  | Build output             |

---

## Types of Pipelines

### 1. Build Pipeline

Used for:

* Code compilation
* Unit testing
* Packaging

### 2. Release Pipeline

Used for:

* Deployment
* Environment promotion
* Production releases

---

## Supported Source Repositories

Azure Pipelines integrates with:

* Azure Repos
* GitHub
* Bitbucket
* GitLab

---

# 3. Hosted and Private Agents

## What is an Agent?

An Agent is a machine that runs pipeline jobs.

Agents execute:

* Builds
* Scripts
* Tests
* Deployments

---

# Microsoft Hosted Agents

## What are Hosted Agents?

Microsoft provides pre-configured virtual machines to run pipelines.

Supported environments:

* Windows
* Linux
* macOS

---

## Advantages of Hosted Agents

* No maintenance
* Quick setup
* Automatically updated
* Scalable

---

## Limitations of Hosted Agents

* Limited customization
* Runtime restrictions
* Internet dependency
* Build time limits

---

# Private (Self-Hosted) Agents

## What are Private Agents?

Private agents are machines managed by your organization.

They can run on:

* Physical servers
* Virtual machines
* On-premises infrastructure
* Cloud VMs

---

## Advantages of Private Agents

| Benefit            | Description            |
| ------------------ | ---------------------- |
| Full Control       | Customize environment  |
| Better Performance | Dedicated resources    |
| Internal Access    | Access private systems |
| Persistent Tools   | Pre-installed software |

---

## Hosted vs Private Agents

| Feature       | Hosted Agent     | Private Agent       |
| ------------- | ---------------- | ------------------- |
| Maintenance   | Microsoft        | Organization        |
| Customization | Limited          | Full                |
| Cost          | Included minutes | Infrastructure cost |
| Security      | Shared           | Dedicated           |
| Speed         | Shared resources | Dedicated resources |

---

# 4. Pipeline and Concurrency

## What is Pipeline Concurrency?

Concurrency refers to how many pipeline jobs can run simultaneously.

---

## Why Concurrency Matters

Concurrency improves:

* Build speed
* Parallel execution
* Resource utilization
* Faster feedback

---

## Example of Parallel Execution

```text id="2nq8u1"
Job 1 → Unit Testing
Job 2 → Security Scan
Job 3 → Code Analysis
```

All jobs run simultaneously.

---

## Azure Pipeline Concurrency Types

### 1. Parallel Jobs

Multiple jobs running at the same time.

### 2. Multi-stage Concurrency

Different stages executed in parallel.

### 3. Matrix Builds

Run builds across multiple environments.

---

## Benefits of Parallel Pipelines

* Reduced build time
* Faster testing
* Increased productivity
* Better scalability

---

## Concurrency Considerations

* Licensing limits
* Agent availability
* Resource consumption
* Cost optimization

---

# 5. Azure Pipeline YAML and Visual Designer

## What is YAML Pipeline?

YAML pipelines define CI/CD workflows using YAML files stored in source control.

Example file:

```text id="f7px2n"
azure-pipelines.yml
```

---

## Benefits of YAML Pipelines

* Version controlled
* Reusable
* Easy automation
* Infrastructure as Code approach
* Easy collaboration

---

## Sample YAML Pipeline

```yaml id="4l5k2q"
trigger:
- main

pool:
  vmImage: ubuntu-latest

steps:
- script: echo "Hello Azure Pipeline"
```

---

## YAML Pipeline Components

| Component | Purpose           |
| --------- | ----------------- |
| trigger   | Starts pipeline   |
| pool      | Defines agent     |
| steps     | Tasks to execute  |
| stage     | Logical grouping  |
| job       | Unit of execution |

---

# Visual Designer Pipeline

## What is Visual Designer?

Visual Designer is a GUI-based pipeline creation method.

Users can:

* Drag and drop tasks
* Configure visually
* Create classic pipelines

---

## Advantages of Visual Designer

* Beginner friendly
* No YAML knowledge needed
* Quick setup

---

## YAML vs Visual Designer

| Feature         | YAML   | Visual Designer |
| --------------- | ------ | --------------- |
| Version Control | Yes    | Limited         |
| Flexibility     | High   | Medium          |
| Learning Curve  | Medium | Easy            |
| Reusability     | High   | Medium          |

---

# 6. Continuous Integration (CI)

## What is Continuous Integration?

Continuous Integration is the practice of automatically integrating code changes into a shared repository multiple times a day.

---

## CI Workflow

```text id="x7h31k"
Developer Commit → Automated Build → Automated Test → Feedback
```

---

## Objectives of CI

* Detect bugs early
* Improve code quality
* Reduce integration issues
* Enable faster development

---

## CI Pipeline Activities

| Activity          | Purpose                |
| ----------------- | ---------------------- |
| Code Checkout     | Retrieve source code   |
| Build             | Compile application    |
| Unit Test         | Validate functionality |
| Static Analysis   | Code quality checks    |
| Artifact Creation | Package output         |

---

## Benefits of CI

* Faster bug detection
* Reduced integration conflicts
* Improved code quality
* Automated validation

---

# 7. Build Strategy Implementation

## What is Build Strategy?

A build strategy defines how applications are built, tested, and packaged efficiently.

---

## Common Build Strategies

### 1. Incremental Build

Only changed code is rebuilt.

### 2. Full Build

Entire application rebuilt every time.

### 3. Parallel Build

Multiple components built simultaneously.

### 4. Multi-stage Build

Separate build phases for optimization.

---

## Build Optimization Techniques

* Dependency caching
* Parallel jobs
* Artifact reuse
* Containerized builds
* Incremental compilation

---

## Branch-Based Build Strategy

| Branch    | Purpose             |
| --------- | ------------------- |
| main      | Production-ready    |
| develop   | Integration branch  |
| feature/* | Feature development |
| release/* | Release preparation |

---

## Recommended Build Practices

* Keep builds fast
* Automate testing
* Fail fast strategy
* Store build artifacts
* Use reusable templates

---

# 8. Integrating Azure Pipelines

## Integration Capabilities

Azure Pipelines integrates with multiple services and tools.

---

## Common Integrations

| Tool        | Integration Purpose       |
| ----------- | ------------------------- |
| GitHub      | Source code               |
| Docker      | Container builds          |
| Kubernetes  | Deployment                |
| SonarQube   | Code quality              |
| Terraform   | Infrastructure automation |
| Slack/Teams | Notifications             |

---

## GitHub Integration Workflow

```text id="v3h8b9"
GitHub Commit → Azure Pipeline Trigger → Build/Test → Deployment
```

---

## Docker Integration Example

```yaml id="t8r4cx"
- task: Docker@2
  inputs:
    command: buildAndPush
    repository: sampleapp
```

---

## Benefits of Integration

* Centralized automation
* Improved collaboration
* Faster delivery
* Better visibility

---

# 9. Setting up Private Agents

## Why Use Private Agents?

Organizations use private agents when:

* Custom software is required
* Internal network access needed
* Compliance restrictions exist
* Faster builds are needed

---

## Steps to Configure Private Agent

### Step 1: Create Agent Pool

Navigate to:

```text id="6w9m2d"
Azure DevOps → Organization Settings → Agent Pools
```

---

### Step 2: Download Agent

Choose:

* Windows
* Linux
* macOS

---

### Step 3: Configure Agent

Example Linux configuration:

```bash id="u3v4pm"
./config.sh
```

Provide:

* Azure DevOps URL
* PAT Token
* Agent Pool Name

---

### Step 4: Start Agent

```bash id="7l0k1s"
./run.sh
```

---

## Best Practices

* Use dedicated build servers
* Monitor agent health
* Secure PAT tokens
* Install required dependencies
* Enable auto-updates

---

# 10. Analyze and Integrate Docker Multi-Stage Builds

## What is Docker Multi-Stage Build?

Docker Multi-stage builds allow multiple stages in a Dockerfile to optimize image size and security.

---

## Why Multi-Stage Builds?

Traditional Docker builds:

* Produce large images
* Include unnecessary tools
* Increase security risks

Multi-stage builds solve these problems.

---

## Multi-Stage Build Workflow

```text id="4x7vla"
Build Stage → Compile Application → Copy Output → Runtime Image
```

---

## Example Multi-Stage Dockerfile

```dockerfile id="y8k5pt"
# Build Stage
FROM maven:3.8.6-openjdk-11 AS build

WORKDIR /app
COPY . .
RUN mvn clean package

# Runtime Stage
FROM openjdk:11-jre-slim

WORKDIR /app
COPY --from=build /app/target/app.jar app.jar

CMD ["java", "-jar", "app.jar"]
```

---

## Benefits of Multi-Stage Builds

| Benefit           | Description               |
| ----------------- | ------------------------- |
| Smaller Images    | Reduced size              |
| Better Security   | Fewer attack surfaces     |
| Faster Deployment | Smaller transfer size     |
| Cleaner Images    | Only runtime dependencies |

---

## Integrating Docker Builds in Azure Pipelines

### Example Pipeline

```yaml id="1s7n6q"
trigger:
- main

pool:
  vmImage: ubuntu-latest

steps:
- task: Docker@2
  inputs:
    command: buildAndPush
    repository: sampleapp
    dockerfile: Dockerfile
```

---

## Best Practices for Docker Integration

* Use lightweight base images
* Avoid storing secrets in images
* Scan images for vulnerabilities
* Use caching effectively
* Tag images properly

---

# Summary

In this module, we covered:

* DevOps Pipelines
* Azure Pipelines
* Hosted and Private Agents
* Pipeline Concurrency
* YAML & Visual Designer Pipelines
* Continuous Integration
* Build Strategies
* Azure Pipeline Integrations
* Private Agent Setup
* Docker Multi-Stage Builds
