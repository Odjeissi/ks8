# End-to-End AWS EKS GitOps Deployment with Observability

This project demonstrates a complete CI/CD, GitOps, and observability workflow for deploying a containerized Python Flask application to Amazon EKS.

It uses **GitLab CI/CD, Docker, Amazon ECR, Terraform, Kubernetes, Argo CD, Kustomize, ExternalDNS, External Secrets Operator, Prometheus, and Grafana**.

## Architecture

```text
Developer
   |
   v
GitLab CI/CD
   |
   +--> Run Tests
   |
   +--> Build Docker Image
             |
             v
        Amazon ECR
             |
             v
      Update GitOps Repo
             |
             v
          Argo CD
             |
             v
        Amazon EKS
             |
      +------+------+
      |             |
      v             v
  Flask App     Kubernetes
      |
      | /metrics
      v
  Prometheus
      |
      v
    Grafana
      |
      v
Monitoring Dashboards
```

GitLab CI/CD builds and pushes the application image to Amazon ECR, then updates the image tag in the GitOps repository.

Argo CD watches the repository and automatically synchronizes the desired Kubernetes configuration with Amazon EKS.

Prometheus collects application and runtime metrics from the Flask application, and Grafana visualizes them through monitoring dashboards.

## Repositories

- [code_source_eks](https://github.com/Odjeissi/code_source_eks) — Flask application and GitLab CI/CD pipeline
- [iac-eks](https://github.com/Odjeissi/iac-eks) — AWS infrastructure provisioned with Terraform
- [ks8](https://github.com/Odjeissi/ks8) — Kubernetes, GitOps, monitoring, and observability configuration

## Key Features

- Automated CI pipeline with GitLab CI/CD
- Docker image build and push to Amazon ECR
- Amazon EKS infrastructure provisioned with Terraform
- GitOps deployments with Argo CD
- Kubernetes environment management with Kustomize
- Automated DNS management with ExternalDNS and Route 53
- Secret management with External Secrets Operator
- Prometheus application and runtime metrics
- Grafana dashboards for application health and performance

## Monitoring & Observability

The Flask application exposes Prometheus metrics through a `/metrics` endpoint.

Prometheus collects metrics including:

- Request throughput
- HTTP status codes
- Error rate
- Requests in progress
- Request duration
- Latency percentiles: p50, p90, p95, and p99
- Pod/process uptime
- CPU usage
- Memory usage
- Open file descriptors
- Python garbage collection metrics

Grafana uses Prometheus as its data source to visualize these metrics.

## Repository Structure

```text
ks8/
├── argocd/
├── kustomize/
├── ExternalDNS/
├── eso/
├── policies/
├── monitor/
├── app_dashboard/
├── screenshots/
└── .gitignore
```

## Deployment Flow

```text
Code Push
   ↓
GitLab CI/CD
   ↓
Tests
   ↓
Docker Build
   ↓
Amazon ECR
   ↓
GitOps Repository Update
   ↓
Argo CD Sync
   ↓
Amazon EKS
   ↓
Prometheus Metrics
   ↓
Grafana Dashboards
```

## Tools Used

- AWS EKS
- Amazon ECR
- Terraform
- Kubernetes
- Docker
- GitLab CI/CD
- Argo CD
- Kustomize
- ExternalDNS
- External Secrets Operator
- Prometheus
- Grafana
- Python / Flask
- GitHub

## What This Project Demonstrates

This project shows how CI/CD, GitOps, Kubernetes, cloud infrastructure, secret management, DNS automation, and observability can work together in a modern DevOps workflow.
