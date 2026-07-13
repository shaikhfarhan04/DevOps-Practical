This is a solid foundation, but a few parts are outdated or can cause issues on current Windows 11 and Amazon Linux 2023. Here's an updated and more practical DevOps lab setup that I would recommend.

---

# DevOps Lab Environment Setup Guide (Windows 11 + AWS EC2)

## Objective

Prepare a complete DevOps lab environment for learning and practicing:

* Linux Administration
* Git & GitHub
* Python
* Docker
* Kubernetes
* Jenkins CI/CD
* Terraform
* AWS CLI
* Ansible
* Grafana
* Infrastructure as Code
* Monitoring

---

# Prerequisites

### Windows

* Windows 10/11 (64-bit)
* Administrator privileges
* Stable Internet
* AWS Account
* Visual Studio Code
* Docker Desktop

### AWS

* AWS Account
* Amazon Linux 2023 EC2
* t3.medium or larger (recommended for Jenkins + Grafana)

---

# Part 1 – Install Visual Studio Code

Install VS Code.

Recommended Extensions

* HashiCorp Terraform
* YAML
* Docker
* Kubernetes
* GitLens
* Ansible
* AWS Toolkit
* Python

---

# Part 2 – Install WSL2

Open PowerShell as Administrator.

```powershell
wsl --install
```

Install Ubuntu

```powershell
wsl --install -d Ubuntu
```

Restart Windows.

Verify

```powershell
wsl --status
```

---

# Part 3 – Install Chocolatey

Open PowerShell as Administrator.

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force
```

Then install Chocolatey using the official installation command from the Chocolatey website.

Verify

```powershell
choco --version
```

---

# Part 4 – Install Development Tools

## Git

```powershell
choco install git -y
```

Verify

```powershell
git --version
```

---

## Python

```powershell
choco install python -y
```

Verify

```powershell
python --version
pip --version
```

---

## AWS CLI

```powershell
choco install awscli -y
```

Verify

```powershell
aws --version
```

Configure

```powershell
aws configure
```

---

## Terraform

```powershell
choco install terraform -y
```

Verify

```powershell
terraform --version
```

---

## kubectl

```powershell
choco install kubernetes-cli -y
```

Verify

```powershell
kubectl version --client
```

---

## Minikube

```powershell
choco install minikube -y
```

Start

```powershell
minikube start --driver=docker
```

Verify

```powershell
minikube status
```

---

# Part 5 – Install Docker Desktop

Install Docker Desktop.

After installation

* Enable WSL2 backend
* Enable Ubuntu integration

Verify

```powershell
docker --version
```

```powershell
docker ps
```

---

# Part 6 – Install PowerShell 7

Install PowerShell 7.

Verify

```powershell
pwsh
```

---

# AWS EC2 Setup

Launch

* Amazon Linux 2023
* t3.medium
* 20 GB storage

---

## Security Group

| Port | Purpose |
| ---- | ------- |
| 22   | SSH     |
| 80   | Web     |
| 443  | HTTPS   |
| 3000 | Grafana |
| 8080 | Jenkins |

---

# Update System

```bash
sudo dnf update -y
```

---

# Install Basic Packages

```bash
sudo dnf install -y \
git \
python3 \
python3-pip \
docker \
wget \
curl \
tar \
make \
zip \
unzip \
jq
```

> **Note:** Amazon Linux 2023 uses `dnf`. While `yum` still works as a compatibility wrapper, using `dnf` is recommended.

---

# Configure Git

```bash
git config --global user.name "Your Name"
```

```bash
git config --global user.email "you@example.com"
```

Verify

```bash
git config --global --list
```

---

# Docker

Enable

```bash
sudo systemctl enable docker
```

Start

```bash
sudo systemctl start docker
```

Allow current user

```bash
sudo usermod -aG docker ec2-user
```

Reconnect via SSH.

Verify

```bash
docker --version
```

```bash
docker run hello-world
```

---

# Install Java 21

```bash
sudo dnf install java-21-amazon-corretto -y
```

Verify

```bash
java -version
```

---

# Install Jenkins

Add repository

```bash
sudo wget -O /etc/yum.repos.d/jenkins.repo \
https://pkg.jenkins.io/redhat-stable/jenkins.repo
```

Import key

```bash
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
```

Install

```bash
sudo dnf install jenkins -y
```

Enable

```bash
sudo systemctl enable jenkins
```

Start

```bash
sudo systemctl start jenkins
```

Check

```bash
sudo systemctl status jenkins
```

Get password

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

Open

```
http://EC2-Public-IP:8080
```

---

# Install Terraform

Add repository

```bash
sudo dnf config-manager addrepo \
--from-repofile=https://rpm.releases.hashicorp.com/AmazonLinux/hashicorp.repo
```

Install

```bash
sudo dnf install terraform -y
```

Verify

```bash
terraform --version
```

---

# Install AWS CLI (if needed)

```bash
aws --version
```

If missing

```bash
sudo dnf install awscli -y
```

---

# Install Grafana

Repository

```bash
sudo tee /etc/yum.repos.d/grafana.repo <<EOF
[grafana]
name=Grafana
baseurl=https://rpm.grafana.com
repo_gpgcheck=1
enabled=1
gpgcheck=1
gpgkey=https://rpm.grafana.com/gpg.key
sslverify=1
EOF
```

Install

```bash
sudo dnf install grafana-enterprise -y
```

Enable

```bash
sudo systemctl enable grafana-server
```

Start

```bash
sudo systemctl start grafana-server
```

Verify

```bash
grafana-server -v
```

Open

```
http://EC2-Public-IP:3000
```

Default login

```
admin
admin
```

---

# Install Ansible

```bash
sudo dnf install ansible -y
```

Verify

```bash
ansible --version
```

---

# Verify Software

## Windows

```powershell
git --version
python --version
pip --version
aws --version
docker --version
terraform --version
kubectl version --client
minikube status
```

---

## Amazon Linux

```bash
git --version
python3 --version
pip3 --version
aws --version
docker --version
terraform --version
java -version
ansible --version
grafana-server -v
```

---

# Verify Services

Docker

```bash
sudo systemctl status docker
```

Jenkins

```bash
sudo systemctl status jenkins
```

Grafana

```bash
sudo systemctl status grafana-server
```

---

# Lab Outcome

You will have a complete DevOps lab including:

* VS Code
* WSL2 Ubuntu
* Git
* Python
* AWS CLI
* Docker Desktop
* Minikube
* Kubernetes (kubectl)
* Terraform
* Jenkins
* Grafana Enterprise
* Ansible

---

## Recommended Learning Order

1. Linux Basics
2. Git & GitHub
3. Python Basics
4. Docker
5. Kubernetes (Minikube)
6. AWS (EC2, IAM, S3, VPC)
7. Terraform
8. Jenkins CI/CD
9. Ansible
10. Prometheus & Grafana
11. Amazon EKS
12. Helm
13. Argo CD (GitOps)

This sequence builds each skill on top of the previous one and is well suited for hands-on DevOps practice.
