# MLOps - Production-Ready Machine Learning Project

## Table of Contents
- [Project Overview](#project-overview)
- [Setup Instructions](#setup-instructions)
- [Workflow](#workflow)
- [Deployment on AWS](#deployment-on-aws)
- [GitHub Actions Setup](#github-actions-setup)

## Project Overview
This project focuses on building a production-ready Machine Learning pipeline using MLOps principles.

Resources

Anaconda: https://www.anaconda.com/

VS Code: https://code.visualstudio.com/download

Git: https://git-scm.com/

Flowchart Tool: https://whimsical.com/

MLOps Tool (EvidentlyAI): https://www.evidentlyai.com/

MongoDB: https://account.mongodb.com/account/login

Dataset (Kaggle EasyVisa): https://www.kaggle.com/datasets/moro23/easyvisa-dataset

## Setup Instructions

### Git Commands
To manage your code with Git:
```bash
git add .
git commit -m "Updated"
git push origin main
```

### How to Run Locally
Follow these steps to set up and run the project:
1. Create a Conda environment:
   ```bash
   conda create -n visa python=3.8 -y
   ```
2. Activate the environment:
   ```bash
   conda activate visa
   ```
3. Install required packages:
   ```bash
   pip install -r requirements.txt
   ```

### Environment Variables
Export the following environment variables:
```bash
export MONGODB_URL="mongodb+srv://<username>:<password>...."
export AWS_ACCESS_KEY_ID=<AWS_ACCESS_KEY_ID>
export AWS_SECRET_ACCESS_KEY=<AWS_SECRET_ACCESS_KEY>
```

## Workflow
The project workflow is structured as follows:
- `constants`
- `entity`
- `components`
- `pipeline`
- `Main file`

## Deployment on AWS - CICD with GitHub Actions

### Description
This section outlines the deployment process using AWS and GitHub Actions:
1. Build a Docker image of the source code.
2. Push the Docker image to Amazon Elastic Container Registry (ECR).
3. Launch an EC2 instance.
4. Pull the Docker image from ECR onto the EC2 instance.
5. Launch the Docker image in EC2.

### AWS Setup
1. **Login to AWS console.**
2. **Create IAM user for deployment** with specific access:
   - EC2 access (Virtual Machine)
   - ECR access (Elastic Container Registry to save your Docker image in AWS)
   - **Policy:**
     - `AmazonEC2ContainerRegistryFullAccess`
     - `AmazonEC2FullAccess`
3. **Create ECR repository** to store/save Docker images.
   - Save the URI (e.g., `315865595366.dkr.ecr.us-east-1.amazonaws.com/visarepo`)
4. **Create EC2 machine (Ubuntu).**
5. **Open EC2 and Install Docker:**
   ```bash
   sudo apt-get update -y
   sudo apt-get upgrade -y
   curl -fsSL https://get.docker.com -o get-docker.sh
   sudo sh get-docker.sh
   sudo usermod -aG docker ubuntu
   newgrp docker
   ```

### GitHub Actions Setup
1. **Configure EC2 as a self-hosted runner:**
   - Navigate to `Settings > Actions > Runners > New self-hosted runner`.
   - Choose your OS and follow the commands provided to set up the runner.
2. **Set up GitHub Secrets:**
   - `AWS_ACCESS_KEY_ID`
   - `AWS_SECRET_ACCESS_KEY`
   - `AWS_DEFAULT_REGION`
   - `ECR_REPO`