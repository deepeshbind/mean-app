# MEAN Stack CRUD Application — Containerized Deployment

A full-stack CRUD application built with **MongoDB, Express, Angular, and Node.js**, containerized with Docker, deployed on an AWS Ubuntu VM, and automated with a GitHub Actions CI/CD pipeline. Nginx is used as a reverse proxy to serve everything through port 80.

---

## Table of Contents

- [Architecture Overview](#architecture-overview)
- [Prerequisites](#prerequisites)
- [Local Development Setup](#local-development-setup)
- [Deployment on AWS VM](#deployment-on-aws-vm)
- [Screenshots](#screenshots)

---

## Architecture Overview

```
Browser
   │
   ▼
[Nginx :80]  ← Angular static files served here
   │
   │  /api/* requests → strips /api/ prefix
   ▼
[Express :8080]
   │
   ▼
[MongoDB :27017]  ← internal Docker network only
```

All services run as Docker containers on a single Ubuntu VM, connected via a Docker Compose internal network. Only port 80 is exposed publicly.

---

## Prerequisites

- [Docker](https://docs.docker.com/get-docker/) & Docker Compose
- [Node.js](https://nodejs.org/) v18+
- A [Docker Hub](https://hub.docker.com/) account
- An AWS (or any cloud) Ubuntu VM
- A GitHub repository with Actions enabled

---

## Local Development Setup

```bash
# Clone the repository
git clone https://github.com/your-username/your-repo.git
cd your-repo

# Run with Docker Compose
docker compose up --build

# App will be available at http://54.221.49.71
```

---

## Deployment on AWS VM

### 1. Provision the VM
- Launch an Ubuntu 22.04 EC2 instance
- Open inbound ports: **22** (SSH) and **80** (HTTP)

### 2. Install Docker on the VM

```bash
sudo apt update
sudo apt install -y docker.io docker-compose-plugin
sudo usermod -aG docker ubuntu
newgrp docker
```

### 3. Add SSH Key to GitHub Secrets
Copy your private key and add it as `VM_SSH_KEY` in your GitHub repository secrets.

### 4. Push to main
Every push to `main` triggers the pipeline which builds, pushes, and redeploys automatically.

---

## Screenshots

### CI/CD Pipeline Execution

![CI/CD Pipeline](./screenshots/cicd-pipeline.png)

### Docker Image Build & Push

![Docker Hub Images](./screenshots/docker-hub.png)

### Application UI

![Application UI](./screenshots/app-ui.png)

### Nginx & Infrastructure

![Infrastructure](./screenshots/infrastructure.png)

