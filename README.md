# complete-devops-project

 🚀 Complete DevOps GitOps Pipeline Project

A complete end to end DevOps project demonstrating Infrastructure as Code (IaC), Continuous Integration (CI), Continuous Delivery (CD), and GitOps using Terraform, Docker, Kubernetes, GitHub Actions, Helm, and Argo CD. The project provisions a local Kubernetes cluster with Terraform, containerizes a Python Flask application, automatically builds and publishes Docker images, updates Helm deployment manifests, and deploys the latest application version to Kubernetes through Argo CD. Every push to the 'main' branch follows an automated GitOps workflow from source code to deployment.

 📌 Project Overview

This project demonstrates how modern DevOps tools work together to automate application delivery. Git acts as the 'single source of truth', GitHub Actions handles Continuous Integration, Helm manages Kubernetes manifests, and Argo CD continuously synchronizes Kubernetes with the desired state stored in Git. The result is a fully automated deployment pipeline that eliminates manual deployment steps and ensures infrastructure and application configurations remain consistent.

 🏗️ Architecture

flowchart

Developer
    │
    │ Git Push
    ▼
GitHub Repository
    │
    ▼
GitHub Actions
    │
    ▼
Build Docker Image
    │
    ▼
Push Image to Docker Hub
    │
    ▼
Update Helm values.yaml
    │
    ▼
Commit Updated Image Tag
    │
    ▼
GitHub Repository
    │
    ▼
Argo CD
    │ Auto Sync
    ▼
Minikube Kubernetes Cluster
    │
    ▼
Flask Application

 ✨ Features

- Provision Kubernetes infrastructure with Terraform
- Deploy a local Kubernetes cluster using Minikube
- Containerize a Python Flask application with Docker
- Automate Docker image builds using GitHub Actions
- Publish versioned images to Docker Hub
- Deploy Kubernetes resources with Helm
- Implement GitOps using Argo CD
- Automatically synchronize Kubernetes with Git
- Self heal configuration drift
- Version deployments using Git commit SHAs

 🛠️ Technology Stack

Infrastructure:  Terraform
Container Platform:  Docker
Orchestration:  Kubernetes (Minikube)
Application:  Python, Flask
CI(Continuous Integration):  GitHub Actions
GitOps:  Argo CD
Package Manager:  Helm
Registry:  Docker Hub
Version Control:  Git & GitHub

 📁 Repository Structure

├── .github/workflows/
│       └── ci.yaml
│
├── terraform-configs/
│   ├── main.tf
│   ├── provider.tf
│   ├── backend.tf
│   ├── variables.tf
│   └── argocd.tf
│
├── complete-devops-project-time-printer/
│   ├── Chart.yaml
│   ├── values.yaml
│   └── templates
│
├── app.py
├── Dockerfile
├── argocd-app.yaml
└── README.md

 📋 Prerequisites

Install the following before running the project:

- Terraform
- Docker Desktop
- Minikube
- kubectl
- Helm
- Git
- Python 3.x
- GitHub Account
- Docker Hub Account

 🚀 Getting Started

"bash"
# Clone the repository
- git clone https://github.com/<your-username>/complete-devops-project.git
- cd complete-devops-project

# Provision the Kubernetes cluster
- cd terraform-configs
- terraform init
- terraform apply

Verify the cluster:
kubectl get nodes

# Build the Docker image
docker build -t <dockerhub-username>/complete-devops-project

 🔐 Required GitHub Secrets

Configure these repository secrets before running the CI pipeline.

Secret=====================Description
-------------------------------------------------------
DOCKERHUB USERNAME=========Docker Hub username
DOCKERHUB TOKEN============Docker Hub Personal Access Token

 🔄 CI/CD & GitOps Workflow

Every push to the 'main' branch automatically triggers the GitHub Actions workflow.

The pipeline performs the following steps:

1. Checks out the repository.
2. Generates a short Git commit SHA.
3. Builds a Docker image.
4. Authenticates with Docker Hub.
5. Pushes the image to Docker Hub.
6. Updates the Helm 'values.yaml' with the new image tag.
7. Commits the updated Helm configuration back to GitHub.
8. Argo CD detects the change and synchronizes the Kubernetes cluster.

Using Git commit SHAs as Docker image tags ensures every deployment is uniquely versioned and directly traceable to a specific code revision.

 ✅ Verification

After deployment, verify each stage of the pipeline.

# Kubernetes
kubectl get nodes
kubectl get pods -A
kubectl get svc -A
# Access Argo CD
kubectl port-forward svc/argocd-server -n argocd 8081:443

Open this "https://localhost:8081" on your local browser

Retrieve the initial admin password:
kubectl get secret argocd-initial-admin-secret -n argocd -o jsonpath="{.data.password}" | base64 -d
# Access the Application
kubectl port-forward pod/<pod-name> 8080:8080 -n default

Visit "http://localhost:8080" on your local browser

The application returns the current server time, confirming a successful deployment.


 🚧 Challenges Encountered

Building this project involved solving several real world DevOps challenges, including:

- Configuring Docker Desktop and Minikube on Windows.
- Installing and configuring Helm and the Argo CD CLI.
- Debugging GitHub Actions workflow failures.
- Automating Helm image tag updates during the CI pipeline.
- Configuring Terraform providers for Kubernetes and Helm.
- Troubleshooting Kubernetes and GitOps deployment issues.

Resolving these challenges strengthened my understanding of CI/CD pipelines, Infrastructure as Code, Kubernetes, and GitOps principles.

 📄 License

This project is licensed for educational and portfolio purposes.

You are welcome to fork, modify, and extend this project for learning or experimentation.