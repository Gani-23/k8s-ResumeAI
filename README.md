# ResumeAI
## Overview
This projects overviews on how to deploy MEAN Application using Kubernetes K8's

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

## Steps

- Create AWS Cluster using EKS
  
![Cloud Formation](Formation.png)

- Set cluster current context to created cluster

![Set Cluster ](config.png)

- Describe the cluster using the command

![Describe Cluster ](describe.png)

- Apply the kubernetes files and get load balancer of Backend and put it on url of Angular API route

![Set Route ](API.png)

- Now apply frontend as well now you would see this working

![Frontend Media ](Frontend.png)


