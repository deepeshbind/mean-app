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

<img width="1470" height="879" alt="Screenshot 2026-02-24 at 6 26 48 PM" src="https://github.com/user-attachments/assets/58a7099f-dc4e-4df7-9d97-60062811aeb5" />
<img width="1470" height="879" alt="Screenshot 2026-02-24 at 6 27 10 PM" src="https://github.com/user-attachments/assets/06e99aef-3d73-4157-b12d-c14f136a57dd" />

### Docker Image Build & Push

<img width="1470" height="918" alt="Screenshot 2026-02-24 at 6 28 35 PM" src="https://github.com/user-attachments/assets/27fb6b81-dc49-4c21-9cb6-c7b3a49fd90d" />

### Application UI

<img width="1470" height="881" alt="Screenshot 2026-02-24 at 8 43 37 PM" src="https://github.com/user-attachments/assets/dec677aa-a1aa-49d0-aa68-5e1ab380f49e" />

### Nginx & Infrastructure

<img width="736" height="459" alt="Screenshot 2026-02-24 at 6 29 59 PM" src="https://github.com/user-attachments/assets/2270f33c-a069-4bef-9cd7-8d6f4d27e7c4" />
<img width="1470" height="956" alt="Screenshot 2026-02-24 at 6 31 08 PM" src="https://github.com/user-attachments/assets/c0479cb4-10c1-4e44-9467-7cc92065a5ac" />


