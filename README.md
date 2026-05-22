# Production-Grade DevSecOps CI/CD Pipeline on AWS

## Overview

This project demonstrates a production-style DevSecOps CI/CD pipeline designed for secure application delivery using AWS, Jenkins, Docker, Kubernetes, SonarQube, and Trivy.

The project automates:

- Secure code validation
- Static Application Security Testing (SAST)
- Container vulnerability scanning
- Docker image build and deployment
- Kubernetes deployment automation
- Secure container registry integration
- IAM and RBAC-based access control

This project simulates enterprise-grade DevSecOps workflows used in modern cloud-native environments.

---

# Architecture

## CI/CD Workflow

```text
Developer Push
       │
       ▼
    GitHub Repository
       │
       ▼
      Jenkins
       │
 ┌─────┼──────────────────────────────┐
 │     │                              │
 ▼     ▼                              ▼
SonarQube Scan              Trivy Security Scan
(SAST)                      (Filesystem + Image)
 │                                   │
 └──────────────┬────────────────────┘
                ▼
          Docker Build
                │
                ▼
           Amazon ECR
                │
                ▼
          Amazon EKS
                │
                ▼
      Kubernetes Deployment
```

---

# Tech Stack

| Technology | Purpose |
|---|---|
| AWS | Cloud Infrastructure |
| Jenkins | CI/CD Automation |
| GitHub | Source Code Management |
| Docker | Containerization |
| Kubernetes (EKS) | Container Orchestration |
| Amazon ECR | Private Container Registry |
| SonarQube | Static Code Analysis (SAST) |
| Trivy | Vulnerability & Image Scanning |
| IAM | Least Privilege Access Control |
| RBAC | Kubernetes Authorization |
| Linux | Server Environment |

---

# Key Features

## DevSecOps Security Pipeline

- Automated CI/CD workflow using Jenkins
- Static Application Security Testing (SAST)
- Dependency vulnerability scanning
- Docker image vulnerability scanning
- Kubernetes deployment automation
- Security quality gates
- Hardened container deployment

---

## AWS Cloud Integration

- Amazon Elastic Kubernetes Service (EKS)
- Amazon Elastic Container Registry (ECR)
- IAM least-privilege policies
- Kubernetes RBAC implementation

---

## Container Security

- Docker image scanning using Trivy
- Filesystem vulnerability detection
- Secure image deployment workflow
- Image validation before deployment

---

# Project Structure

```bash
Production-Grade-DevSecOps-CI-CD-Pipeline/
│
├── app/
│   ├── package.json
│   ├── server.js
│   └── Dockerfile
│
├── kubernetes/
│   ├── deployment.yaml
│   ├── service.yaml
│   ├── role.yaml
│   ├── rolebinding.yaml
│   └── serviceaccount.yaml
│
├── jenkins/
│   └── Jenkinsfile
│
├── security/
│   ├── iam-policy.json
│   └── trivy-config.yaml
│
├── docs/
│   ├── architecture-diagram.png
│   └── setup-guide.md
│
├── screenshots/
│   ├── jenkins-pipeline.png
│   ├── sonar-dashboard.png
│   ├── trivy-scan.png
│   └── kubernetes-deployment.png
│
├── docker-compose.yml
├── README.md
└── .gitignore
```

---

# CI/CD Pipeline Stages

## Stage 1 — Source Code Checkout

- Jenkins pulls source code from GitHub repository.

---

## Stage 2 — SonarQube SAST Scan

- Static code analysis performed using SonarQube
- Detects:
  - Code smells
  - Bugs
  - Security vulnerabilities
  - Maintainability issues

---

## Stage 3 — Trivy Filesystem Scan

- Trivy scans project dependencies and filesystem
- Detects:
  - Vulnerable packages
  - Misconfigurations
  - Dependency risks

---

## Stage 4 — Docker Image Build

- Application is containerized using Docker
- Hardened lightweight container images are created

---

## Stage 5 — Trivy Docker Image Scan

- Docker image scanned for:
  - CVEs
  - OS package vulnerabilities
  - Security risks

---

## Stage 6 — Push to Amazon ECR

- Secure Docker images pushed to Amazon Elastic Container Registry

---

## Stage 7 — Kubernetes Deployment on Amazon EKS

- Automated deployment to Kubernetes cluster
- Application exposed using Kubernetes LoadBalancer service

---

# Security Implementations

## SonarQube Security Analysis

Implemented static code analysis to identify:

- Vulnerable code patterns
- Security hotspots
- Maintainability issues
- Potential application weaknesses

---

## Trivy Vulnerability Scanning

Implemented:

- Filesystem scanning
- Docker image scanning
- Dependency scanning
- Misconfiguration detection

---

## IAM Least Privilege

Configured restricted AWS IAM permissions for:

- Amazon ECR access
- Amazon EKS deployment
- Limited AWS resource operations

---

## Kubernetes RBAC

Implemented Role-Based Access Control (RBAC) for:

- Deployment authorization
- Namespace isolation
- Secure Kubernetes operations

---

# Sample Jenkins Pipeline

```groovy
pipeline {
    agent any

    stages {

        stage('Clone Repository') {
            steps {
                git 'https://github.com/your-repository.git'
            }
        }

        stage('SonarQube Scan') {
            steps {
                sh 'sonar-scanner'
            }
        }

        stage('Trivy Filesystem Scan') {
            steps {
                sh 'trivy fs .'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t devsecops-app .'
            }
        }

        stage('Trivy Image Scan') {
            steps {
                sh 'trivy image devsecops-app'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f kubernetes/'
            }
        }
    }
}
```

---

# Dockerfile

```dockerfile
FROM node:18-alpine

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

EXPOSE 3000

CMD ["npm", "start"]
```

---

# Kubernetes Deployment

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: devsecops-app
spec:
  replicas: 2
  selector:
    matchLabels:
      app: devsecops-app
  template:
    metadata:
      labels:
        app: devsecops-app
    spec:
      containers:
      - name: devsecops-app
        image: IMAGE_URI
        ports:
        - containerPort: 3000
```

---

# Security Tools Used

| Tool | Function |
|---|---|
| SonarQube | Static Application Security Testing |
| Trivy | Container & Dependency Scanning |
| IAM | AWS Access Control |
| RBAC | Kubernetes Authorization |

---

# Local Setup (Optional)

This project can also be simulated locally using:

- Docker Compose
- Minikube
- Kind Kubernetes Cluster

This allows DevSecOps workflow testing without continuous AWS billing.

---

# Future Enhancements

Planned improvements:

- Terraform Infrastructure as Code
- ArgoCD GitOps Deployment
- Prometheus Monitoring
- Grafana Dashboards
- OWASP ZAP DAST Scanning
- Helm Charts
- Slack Notifications
- Blue-Green Deployment
- Canary Deployment
- Runtime Security using Falco

---

# Learning Outcomes

This project helped in understanding:

- Production-grade CI/CD workflows
- DevSecOps practices
- Kubernetes deployment automation
- Secure containerization
- Cloud-native application deployment
- AWS infrastructure integration
- Security-focused software delivery

---

# Resume Description

Built a production-grade DevSecOps CI/CD pipeline on AWS using Jenkins, SonarQube, Trivy, Docker, Amazon ECR, and Amazon EKS to automate secure application delivery. Implemented SAST, container vulnerability scanning, IAM least-privilege access control, and Kubernetes RBAC-based deployment automation following enterprise DevSecOps practices.

---

# Screenshots

Add screenshots here:

- Jenkins Pipeline Execution
- SonarQube Dashboard
- Trivy Scan Results
- Kubernetes Deployment
- Docker Build Logs
- EKS Cluster

---

# Author

Manish Thakur

Cloud | DevOps | DevSecOps | AWS | Kubernetes Enthusiast

---

# Disclaimer

This project was developed for educational and portfolio purposes to simulate production-grade DevSecOps workflows and enterprise cloud deployment practices.