# DevOps Lab

Laboratório prático para consolidar conhecimentos em **infraestrutura, DevOps, cloud e deployment de aplicações**, com foco em ambientes reais utilizando Linux, Docker, CI/CD, AWS, Terraform, observabilidade e Kubernetes.

Este repositório acompanha minha evolução de **Fullstack Developer para Fullstack Developer com forte base de infraestrutura**.

---

## 🎯 Objective

Build and operate production-oriented applications while developing practical knowledge in:

* Linux
* Docker
* CI/CD
* AWS
* Infrastructure as Code
* Terraform
* Observability
* Kubernetes
* Cloud architecture
* Application deployment and troubleshooting

The main goal is not only to learn individual technologies, but to understand how they work together across the complete application lifecycle.

```text
Development
     ↓
Git
     ↓
CI/CD
     ↓
Docker
     ↓
Container Registry
     ↓
AWS Infrastructure
     ↓
Kubernetes
     ↓
Observability
     ↓
Production
```

---

## 🗂️ Repository Structure

```text
devops-lab/
│
├── linux/
│   ├── commands/
│   ├── networking/
│   ├── processes/
│   └── troubleshooting/
│
├── docker/
│   ├── fundamentals/
│   ├── node-api/
│   ├── compose/
│   ├── networking/
│   ├── volumes/
│   └── troubleshooting/
│
├── cicd/
│   ├── gitlab-ci/
│   └── github-actions/
│
├── aws/
│   ├── ec2/
│   ├── rds/
│   ├── s3/
│   ├── iam/
│   ├── ecr/
│   ├── vpc/
│   └── cloudwatch/
│
├── terraform/
│   ├── fundamentals/
│   ├── aws/
│   ├── modules/
│   └── environments/
│
├── observability/
│   ├── logging/
│   ├── metrics/
│   ├── health-checks/
│   ├── alerting/
│   └── tracing/
│
├── kubernetes/
│   ├── fundamentals/
│   ├── deployments/
│   ├── services/
│   ├── configmaps/
│   ├── secrets/
│   ├── ingress/
│   ├── scaling/
│   └── helm/
│
└── projects/
    ├── project-01/
    └── project-02/
```

---

# 🧭 Learning Roadmap

## Phase 1 — Linux & Infrastructure Fundamentals

**Status:** 🟡 In progress

Topics:

* [ ] Linux filesystem
* [ ] Shell fundamentals
* [ ] Processes and signals
* [ ] Services and systemd
* [ ] Users and permissions
* [ ] SSH
* [ ] Networking fundamentals
* [ ] DNS
* [ ] TCP/IP
* [ ] HTTP/HTTPS
* [ ] Linux troubleshooting

### Practical goal

Operate a Node.js application on a Linux environment and diagnose common application, process, permission and networking problems.

---

## Phase 2 — Docker

**Status:** ⬜ Planned

Topics:

* [ ] Docker architecture
* [ ] Images
* [ ] Containers
* [ ] Dockerfile
* [ ] Image layers
* [ ] Build cache
* [ ] `.dockerignore`
* [ ] Environment variables
* [ ] Volumes
* [ ] Bind mounts
* [ ] Docker networks
* [ ] Docker Compose
* [ ] Multi-stage builds
* [ ] Container security
* [ ] Resource limits
* [ ] Docker troubleshooting

### Practical goal

Containerize a Node.js API with PostgreSQL and Redis.

```text
              Docker Compose
                    │
        ┌───────────┼───────────┐
        │           │           │
        ▼           ▼           ▼
      Node.js    PostgreSQL    Redis
```

---

## Phase 3 — CI/CD

**Status:** ⬜ Planned

Topics:

* [ ] CI/CD fundamentals
* [ ] GitLab CI
* [ ] GitHub Actions
* [ ] Pipelines
* [ ] Jobs
* [ ] Stages
* [ ] Runners
* [ ] Artifacts
* [ ] Caching
* [ ] Environment variables
* [ ] Secrets
* [ ] Docker image builds
* [ ] Container registry
* [ ] Automated deployment
* [ ] Rollback strategies

### Practical goal

Build a pipeline that automatically tests, builds and publishes a Docker image.

```text
Git Push
   ↓
Tests
   ↓
Build
   ↓
Docker Image
   ↓
Container Registry
   ↓
Deploy
```

---

# ☁️ Phase 4 — AWS

**Status:** ⬜ Planned

Focus services:

* [ ] IAM
* [ ] EC2
* [ ] RDS
* [ ] S3
* [ ] ECR
* [ ] CloudWatch
* [ ] VPC
* [ ] Subnets
* [ ] Route Tables
* [ ] Internet Gateway
* [ ] Security Groups
* [ ] IAM Roles
* [ ] Load Balancing
* [ ] AWS CLI

### Practical goal

Deploy a Node.js application on AWS using containerized workloads.

Target architecture:

```text
                    Internet
                       │
                       ▼
                    EC2
                       │
                       ▼
                  Docker
                       │
                       ▼
                  Node.js API
                   │       │
                   ▼       ▼
                  RDS      S3
```

---

# 🏗️ Phase 5 — Terraform

**Status:** ⬜ Planned

Topics:

* [ ] Terraform fundamentals
* [ ] Providers
* [ ] Resources
* [ ] Variables
* [ ] Outputs
* [ ] Data sources
* [ ] State
* [ ] Remote state
* [ ] Modules
* [ ] Workspaces / environments
* [ ] Terraform with AWS
* [ ] Infrastructure dependencies
* [ ] Terraform best practices

### Practical goal

Provision the AWS infrastructure required by the application using Infrastructure as Code.

```text
Terraform
    │
    ├── VPC
    ├── EC2
    ├── Security Groups
    ├── IAM
    ├── RDS
    ├── S3
    └── ECR
```

The infrastructure should be reproducible without manually creating AWS resources through the console.

---

# 📊 Phase 6 — Observability

**Status:** ⬜ Planned

Topics:

* [ ] Structured logging
* [ ] Log levels
* [ ] Request IDs
* [ ] Metrics
* [ ] Application metrics
* [ ] Infrastructure metrics
* [ ] Health checks
* [ ] Readiness checks
* [ ] Liveness checks
* [ ] Alerting
* [ ] Dashboards
* [ ] Distributed tracing
* [ ] OpenTelemetry

### Practical goal

Make the application observable enough to answer:

> What happened?

> When did it happen?

> Which component was affected?

> How many users/requests were affected?

> What caused the failure?

Target observability model:

```text
              Application
                   │
        ┌──────────┼──────────┐
        ▼          ▼          ▼
      Logs      Metrics     Traces
        │          │          │
        └──────────┼──────────┘
                   ▼
             Observability
                   │
                   ▼
                Alerts
```

---

# ☸️ Phase 7 — Kubernetes

**Status:** ⬜ Planned

Topics:

* [ ] Kubernetes architecture
* [ ] Cluster
* [ ] Nodes
* [ ] Pods
* [ ] Deployments
* [ ] ReplicaSets
* [ ] Services
* [ ] Namespaces
* [ ] ConfigMaps
* [ ] Secrets
* [ ] Ingress
* [ ] Resource requests/limits
* [ ] Liveness probes
* [ ] Readiness probes
* [ ] Startup probes
* [ ] Horizontal Pod Autoscaler
* [ ] Rolling updates
* [ ] Rollbacks
* [ ] Helm

### Practical goal

Deploy the Node.js application into Kubernetes and understand how the platform maintains the desired state.

```text
                  Ingress
                     │
                     ▼
                  Service
                     │
          ┌──────────┼──────────┐
          ▼          ▼          ▼
        Pod        Pod        Pod
          │          │          │
          └──────────┼──────────┘
                     │
                     ▼
                    RDS
```

---

# 🚀 Projects

## Project 01 — Containerized Node.js Application

**Status:** ⬜ Planned

A production-oriented Node.js API running with:

* Docker
* Docker Compose
* PostgreSQL
* Redis
* Environment configuration
* Health checks
* Structured logging

The purpose is to establish a solid containerization and local infrastructure foundation.

---

## Project 02 — Cloud-Native Application

**Status:** ⬜ Planned

Complete deployment pipeline integrating the technologies studied throughout the lab.

### Stack

**Application**

* Node.js
* PostgreSQL
* Redis

**Containers**

* Docker
* Docker Compose

**CI/CD**

* GitLab CI / GitHub Actions

**Cloud**

* AWS
* EC2
* RDS
* S3
* ECR
* IAM
* VPC
* CloudWatch

**Infrastructure**

* Terraform

**Orchestration**

* Kubernetes
* Helm

**Observability**

* Logs
* Metrics
* Health checks
* Alerts
* Tracing

### Target architecture

```text
                         Git
                          │
                          ▼
                       CI/CD
                          │
             ┌────────────┴────────────┐
             │                         │
             ▼                         ▼
           Tests                  Docker Build
                                       │
                                       ▼
                                      ECR
                                       │
                                       ▼
                                  Kubernetes
                                       │
                    ┌──────────────────┼──────────────────┐
                    ▼                  ▼                  ▼
                  Pod                Pod                Pod
                    │                  │                  │
                    └──────────────────┼──────────────────┘
                                       │
                         ┌─────────────┴─────────────┐
                         ▼                           ▼
                        RDS                         Redis
                         │
                         ▼
                        S3

                    Observability
                         │
              ┌──────────┼──────────┐
              ▼          ▼          ▼
            Logs      Metrics     Traces
```

---

# 🧪 Troubleshooting

A major part of this repository is documenting failures and their solutions.

Examples:

* Container unable to start
* Container cannot connect to PostgreSQL
* Port already in use
* Docker image unexpectedly large
* Permission denied
* DNS resolution failure
* EC2 instance unreachable
* Security Group blocking traffic
* RDS connection failure
* CI/CD pipeline failure
* Docker registry authentication failure
* Kubernetes pod crash
* Kubernetes readiness probe failure
* Deployment rollback

Each relevant issue should be documented using:

```text
Problem
    ↓
Symptoms
    ↓
Investigation
    ↓
Root Cause
    ↓
Solution
    ↓
Prevention
```

---

# 📚 Knowledge Notes

This repository also contains short technical notes about concepts encountered during the labs.

The focus is on understanding **why** something works rather than simply documenting commands.

Examples:

* Docker image vs container
* Container vs virtual machine
* TCP vs UDP
* Public vs private subnet
* Security Group vs Network ACL
* IAM User vs IAM Role
* CI vs CD
* Rolling deployment vs blue/green deployment
* Docker Compose vs Kubernetes
* Horizontal vs vertical scaling
* Logs vs metrics vs traces
* Stateful vs stateless applications

---

# 📈 Progress

| Area          | Status         | Target             |
| ------------- | -------------- | ------------------ |
| Linux         | 🟡 In progress | Advanced practical |
| Docker        | ⬜ Planned      | Professional       |
| CI/CD         | ⬜ Planned      | Professional       |
| AWS           | ⬜ Planned      | Professional       |
| Terraform     | ⬜ Planned      | Intermediate       |
| Observability | ⬜ Planned      | Intermediate       |
| Kubernetes    | ⬜ Planned      | Intermediate       |
| Project 01    | ⬜ Planned      | Complete           |
| Project 02    | ⬜ Planned      | Complete           |

---

# 🎯 Final Goal

By the end of this roadmap, I should be able to take a Node.js application from source code to a reproducible, observable deployment environment:

```text
                Source Code
                     │
                     ▼
                    Git
                     │
                     ▼
                   CI/CD
                     │
              ┌──────┴──────┐
              ▼             ▼
            Tests        Docker Build
                            │
                            ▼
                           ECR
                            │
                            ▼
                        Kubernetes
                            │
                 ┌──────────┼──────────┐
                 ▼          ▼          ▼
                API        API        API
                 │          │          │
                 └──────────┼──────────┘
                            │
                    ┌───────┴───────┐
                    ▼               ▼
                   RDS            Redis
                    │
                    ▼
                   S3

              Observability
                    │
             ┌──────┼──────┐
             ▼      ▼      ▼
           Logs   Metrics  Traces
```

The final objective is to develop the ability to **build, deploy, operate and troubleshoot modern web applications in cloud environments**, while maintaining a strong fullstack foundation.
