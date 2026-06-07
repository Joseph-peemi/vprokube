# Kubernetes Definitions - Multi-Service Application

Production-ready Kubernetes manifests for a **multi-service microservices application**. This repository contains YAML definitions (Deployments, Services, Ingress, PVC, Secrets, etc.) designed for GitOps workflows.

![Kubernetes](https://img.shields.io/badge/Kubernetes-%23326CE5.svg?style=for-the-badge&logo=kubernetes&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)
![GitOps](https://img.shields.io/badge/GitOps-%231A1A1A.svg?style=for-the-badge&logo=argo&logoColor=white)
![YAML](https://img.shields.io/badge/YAML-%23F7B93B.svg?style=for-the-badge&logo=yaml&logoColor=black)

## Overview

This repo serves as the **GitOps source of truth** for deploying a multi-tier application on Kubernetes. It includes separate components for:

- Main Application
- Database
- RabbitMQ (Message Queue)
- Additional Microservice
- Supporting resources (Ingress, Secrets, PersistentVolumeClaim)

These manifests are intended to be used with tools like **ArgoCD**, **Flux**, or Jenkins-based GitOps pipelines.

## Project Structure
.
└── kubedefs/

├── appdeploy.yaml          # Main application Deployment

├── appservice.yaml         # Application Service

├── appingress.yaml         # Ingress configuration

├── dbdeploy.yaml           # Database Deployment

├── dbservice.yaml          # Database Service

├── dbpvc.yaml              # Persistent Volume Claim for DB

├── rmqdeploy.yaml          # RabbitMQ Deployment

├── rmqservice.yaml         # RabbitMQ Service

├── mcdep.yaml              # Microservice Deployment

├── mcservice.yaml          # Microservice Service

├── secret.yaml             # Kubernetes Secrets
└── ...
text## Components

| File                | Resource Type     | Purpose                              |
|---------------------|-------------------|--------------------------------------|
| `appdeploy.yaml`    | Deployment        | Main Spring Boot / Java application  |
| `appservice.yaml`   | Service           | Exposes the main app                 |
| `appingress.yaml`   | Ingress           | External HTTP routing                |
| `dbdeploy.yaml`     | Deployment        | Database (e.g., MySQL/PostgreSQL)    |
| `dbpvc.yaml`        | PersistentVolumeClaim | Persistent storage for DB         |
| `rmqdeploy.yaml`    | Deployment        | RabbitMQ message broker              |
| `mcdep.yaml`        | Deployment        | Additional microservice              |
| `secret.yaml`       | Secret            | Credentials and sensitive data       |

## Features

- **Multi-service architecture** support
- Production best practices (resource requests/limits, probes, labels)
- Persistent storage for stateful services
- Ingress configuration for external access
- Secret management
- Ready for GitOps continuous deployment

## Usage

### Apply All Manifests

```bash
kubectl apply -f kubedefs/
Apply Individually
Bashkubectl apply -f kubedefs/appdeploy.yaml
kubectl apply -f kubedefs/appservice.yaml
# ... etc 
## Recommended Order

Secrets & PVCs
Databases & Message Queues
Microservices
Ingress

## Integration
This repository is designed to work as part of a larger CI/CD ecosystem:

CI: Builds and pushes Docker images (see related repos)
CD: Jenkins or ArgoCD updates image tags and syncs these manifests

## Prerequisites

Kubernetes cluster (EKS, GKE, Minikube, etc.)
kubectl configured
(Optional) ArgoCD or Flux for GitOps
Helm (if using Helm charts alongside)
