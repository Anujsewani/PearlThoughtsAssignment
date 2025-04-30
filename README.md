# DevOps Assessment – Yii2 + Docker Swarm + CI/CD + Ansible

This project showcases a full DevOps pipeline to deploy a sample **PHP Yii2 application** using **Docker Swarm**, **Ansible**, and **GitHub Actions** on an **AWS EC2** instance. It uses **host-based NGINX** as a reverse proxy.


## Setup Instructions

### 1. Prerequisites

- AWS EC2 instance (Ubuntu 22.04+)
- SSH access 
- Docker Hub account
- Install Ansible
- GitHub repository with the following secrets:
  - `EC2_HOST` – EC2 public IP or DNS
  - `EC2_SSH_KEY` – Private SSH key (as a GitHub Secret)
  - `DOCKERHUB_PASSWORD` – Your Docker Hub password
  - `DOCKERHUB_USERNAME` – Your Docker Hub username


---

### 2. Provision EC2 with Ansible

```bash
git clone https://github.com/Anujsewani/PearlThoughtsAssignment
cd PearlThoughtsAssignment/ansible
ansible-playbook -i inventory.ini playbook.yml
```
### 3. Assumptions

I am running ansible on local machine and deploying infrastrucure on aws instance 

### 4. How to test deployment

Run cicd pipeline and see if it runs successfully, you can make changes in repo and push to github as it will trigger pipeline


