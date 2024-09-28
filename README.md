# Project Name: ResumeAI
## Overview
This project is a fork of [ResumeAI](https://github.com/UnpredictablePrashant/ResumeAI) that demonstrates how to set up a Dockerized application with CI/CD pipelines, Kubernetes deployments, and AWS ECR integration.

## Features
- Dockerfile for the application
- Docker Compose for multi-container orchestration
- CI/CD pipeline using Jenkins
- Deployment on local Minikube
- Deployment on AWS EKS

## Requirements
- Docker
- Docker Compose
- Jenkins
- Minikube
- AWS CLI
- kubectl

## Getting Started

### 1. Fork the Project
- Create a fork of the ResumeAI project and rename it to your desired project name.

### 2. Write Dockerfile
- Create a `Dockerfile` in the root of your project. Below is an example:
    ```Dockerfile
    # Use the official image as a parent image
    FROM node:14

    # Set the working directory
    WORKDIR /usr/src/app

    # Copy package.json and package-lock.json
    COPY package*.json ./

    # Install dependencies
    RUN npm install

    # Copy the rest of the application code
    COPY . .

    # Expose the port
    EXPOSE 3000

    # Command to run the application
    CMD ["npm", "start"]
    ```

### 3. Write Docker Compose File
- Create a `docker-compose.yml` file:
    ```yaml
    version: '3.8'
    services:
      app:
        build: .
        ports:
          - "3000:3000"
    ```

### 4. Push Images to ECR
- Authenticate to ECR and push your Docker images. Replace `<your-repo-name>` with your ECR repository name:
    ```bash
    aws ecr get-login-password --region <your-region> | docker login --username AWS --password-stdin <your-account-id>.dkr.ecr.<your-region>.amazonaws.com
    docker tag your-image:latest <your-account-id>.dkr.ecr.<your-region>.amazonaws.com/<your-repo-name>:latest
    docker push <your-account-id>.dkr.ecr.<your-region>.amazonaws.com/<your-repo-name>:latest
    ```

### 5. Create a CI/CD Pipeline with Jenkins
- Set up Jenkins and create a new pipeline job. Use the following example pipeline script:
    ```groovy
    pipeline {
        agent any
        stages {
            stage('Build') {
                steps {
                    script {
                        sh 'docker build -t your-image .'
                    }
                }
            }
            stage('Test') {
                steps {
                    script {
                        // Add your test commands here
                    }
                }
            }
            stage('Deploy') {
                steps {
                    script {
                        // Deploy to EKS or Minikube
                    }
                }
            }
        }
    }
    ```

### 6. Deploy Using Minikube
- Start Minikube:
    ```bash
    minikube start
    ```
- Deploy your application:
    ```bash
    kubectl apply -f k8s/deployment.yml
    kubectl apply -f k8s/service.yml
    ```

### 7. Deploy Using EKS
- Create an EKS cluster using the AWS CLI or EKS console.
- Update your Kubernetes configurations and deploy:
    ```bash
    kubectl apply -f k8s/deployment.yml
    kubectl apply -f k8s/service.yml
    ```

## Submission Instructions
- Ensure your assignment is fully completed.
- Push your code to a GitHub repository.
- Share the repository link by including it in a text, Word, or PDF file format.
- Submit the file/text containing the repository link via Vlearn.

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
