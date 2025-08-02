🚀 DevOps CI/CD Project: Jenkins + Docker + Terraform
This project automates the CI/CD pipeline for a Node.js application using Jenkins, Docker, and Terraform.
It builds the app, pushes a Docker image to Docker Hub, and deploys it to an EC2 instance provisioned via Terraform.

🔧 Tech Stack
🐳 Docker

⚙️ Jenkins

☁️ AWS EC2 (Provisioned via Terraform)

📦 Docker Hub (Image Registry)

💻 GitHub (Source Code Repository)

📁 Project Structure
bash
Copy
Edit
Devops-project-/
│
├── jenkins/
│   └── Jenkinsfile             # CI/CD pipeline definition
│
├── terraform/
│   ├── main.tf                 # AWS infrastructure setup (VPC, EC2, SG)
│   └── variables.tf            # Terraform variables
│
├── app/
│   ├── Dockerfile              # Container image for Node.js app
│   └── index.js                # Sample Node.js app
│
└── README.md                   # You're here
🛠️ How It Works
Terraform provisions:

A VPC

Public subnet

Security group

EC2 instance (Ubuntu)

Jenkins Pipeline does:

Clone GitHub repo

Build Docker image

Push image to DockerHub

SSH into EC2 & deploy container

