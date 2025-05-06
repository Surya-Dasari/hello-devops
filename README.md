# Hello DevOps - A Simple Java Web App

This is a simple **Java** web application built with **Maven**, **Docker**, and deployed on **Minikube** using **Kubernetes**. It showcases a **CI/CD pipeline** with **Jenkins** and a **multistage Dockerfile** for building and deploying the app.

## Project Overview

The app prints the following message to the console:
Hello World – where development meets reality


## Technologies Used

- **Java**: Language for the web application
- **Maven**: Build automation tool
- **Docker**: Containerization of the application
- **Minikube**: Local Kubernetes cluster for deployment
- **Jenkins**: CI/CD pipeline for automation
- **GitHub**: Version control and repository hosting

## Folder Structure

hello-devops/
│
├── k8s/ # Kubernetes Deployment & Service files
│ ├── deployment.yaml
│ └── service.yaml
├── src/ # Java source code
│ └── main/
│ └── java/
│ └── com/
│ └── example/
│ └── HelloApp.java
├── target/ # Compiled Java artifacts
├── Dockerfile # Dockerfile to containerize the app
├── Jenkinsfile # Jenkins pipeline configuration
├── pom.xml # Maven project configuration
└── README.md # This README file


## Setup Instructions

### Prerequisites

- **Docker** installed and running
- **Minikube** for Kubernetes local development
- **Jenkins** for CI/CD pipeline
- **Git** and **GitHub** for version control

### Steps to Run Locally

1. **Clone the repository**:
    ```bash
    git clone https://github.com/Surya-Dasari/hello-devops.git
    cd hello-devops
    ```

2. **Build Docker Image**:
    ```bash
    eval $(minikube docker-env)  # Use Minikube Docker
    docker build -t hello-devops:1.0 .
    ```

3. **Deploy on Minikube**:
    ```bash
    kubectl apply -f k8s/deployment.yaml
    kubectl apply -f k8s/service.yaml
    ```

4. **Access the app**:
    ```bash
    minikube service hello-devops-service --url
    ```

5. **Enjoy the app**: Open the URL in a browser or use `curl`:
    ```bash
    curl $(minikube service hello-devops-service --url)
    ```

### Jenkins CI/CD Pipeline

The project includes a **Jenkinsfile** that automates the following stages:

- **Checkout**: Fetches the source code from the repository.
- **Build with Maven**: Packages the Java application into a JAR file.
- **Docker Build**: Builds a Docker image of the application.
- **Docker Run & Test**: Runs the container and tests it.
- **Push to Registry**: Pushes the Docker image to a registry (optional, uncomment in Jenkinsfile).

### Kubernetes Deployment

- The **deployment.yaml** file deploys the Dockerized app on **Minikube** Kubernetes.
- The **service.yaml** file exposes the app using a **NodePort**.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.


