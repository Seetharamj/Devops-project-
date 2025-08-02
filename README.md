# 🚀 DevOps CI/CD Project: Jenkins + Docker + Terraform

This project automates a CI/CD pipeline for a Node.js application using **Jenkins**, **Docker**, and **Terraform**.  
It builds a Docker image, pushes it to Docker Hub, and deploys it to an EC2 instance provisioned by Terraform.

---

## 🔧 Tech Stack

- 🐳 Docker
- ⚙️ Jenkins
- ☁️ AWS EC2 (via Terraform)
- 📦 Docker Hub
- 💻 GitHub

---

## 📁 Project Structure

Devops-project-/
├── jenkins/
│ └── Jenkinsfile # CI/CD pipeline definition
├── terraform/
│ ├── main.tf # AWS infrastructure (VPC, EC2, etc.)
│ └── variables.tf # Terraform variables
├── app/
│ ├── Dockerfile # Docker image for Node.js app
│ └── index.js # Sample Node.js app
└── README.md 

---

## 🛠️ How It Works

1. **Terraform** provisions:
   - A VPC
   - Public subnet
   - Security group
   - EC2 instance (Ubuntu)

2. **Jenkins Pipeline**:
   - Clones GitHub repo
   - Builds Docker image
   - Pushes image to DockerHub
   - SSH into EC2 & deploys container

---

