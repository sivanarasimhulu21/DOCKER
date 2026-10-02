# Docker Environment Setup and Spring Boot Application Deployment

This repository contains two guides that explain Docker fundamentals, setting up a Docker environment on AWS EC2, and containerizing and deploying a Spring Boot application.

The purpose of this repository is to demonstrate how Docker helps simplify application deployment and maintain consistency across different environments.

## 📚 Documentation

### 1. Docker Environment Setup on AWS EC2

**File:** `Docker-Environment-Setup-on-AWS-EC2.md`

This guide explains how to prepare an AWS EC2 instance for running Docker containers.

**Topics covered:**

* Creating an AWS account and launching an EC2 instance
* Configuring Ubuntu Server and security group ports
* Connecting to an EC2 instance using SSH
* Installing and managing Docker
* Creating a sample Dockerfile
* Building Docker images
* Tagging and pushing images to Docker Hub
* Common Docker commands for container and image management

🔗 **Read the guide:** [Docker Environment Setup on AWS EC2](https://github.com/sivanarasimhulu21/DOCKER/blob/main/Docker%20Environment%20Setup%20on%20AWS%20EC2.md)

### 2. Spring Boot Application Containerization and Deployment

**File:** `Spring-Boot-Application-Containerization-and-Deployment.md`

This guide demonstrates how to package a Spring Boot application into a Docker image and run it as a container.

**Problem Statement:**

ABC Private Limited has migrated its IT applications from a monolithic architecture to a microservices architecture. The organization needs a consistent and simplified deployment process. Docker containerization helps package applications and their runtime requirements into portable containers.

**Topics covered:**

* Creating a Spring Boot application using [Spring Initializr](https://start.spring.io/)
* Developing and building the application
* Uploading the project to GitHub
* Connecting to an AWS EC2 instance
* Writing a Dockerfile for a Spring Boot application
* Building a Docker image
* Pushing and pulling images through Docker Hub
* Running the application in a Docker container
* Accessing the application through a web browser

🔗 **Read the guide:** [Spring Boot Application Containerization and Deployment](https://github.com/sivanarasimhulu21/DOCKER/blob/main/Containerization%20and%20Deployment%20of%20Spring%20Boot%20%20Application.md)

## 🛠️ Technologies Used

* **Cloud Platform:** AWS
* **Virtual Server:** Amazon EC2
* **Operating System:** Ubuntu Server / Linux
* **Containerization:** Docker
* **Application Framework:** Spring Boot
* **Programming Language:** Java
* **Version Control:** Git and GitHub
* **Container Registry:** Docker Hub

## 🔄 Deployment Workflow

```text
Spring Boot Application
          |
          v
      Build JAR
          |
          v
      Dockerfile
          |
          v
    Build Docker Image
          |
          v
      Docker Hub
          |
          v
    AWS EC2 Instance
          |
          v
    Run Docker Container
          |
          v
   Access Application
    Using Web Browser
```

## 🎯 Learning Objectives

After exploring these guides, you should understand how to:

* Set up a Docker environment on a cloud virtual machine.
* Create Docker images using Dockerfiles.
* Run and manage Docker containers.
* Containerize a Java Spring Boot application.
* Publish and retrieve Docker images from Docker Hub.
* Deploy a containerized application on AWS EC2.
* Understand a basic application containerization and deployment workflow.

## 👨‍💻 Author

**Chittiboina Siva Narasimhulu**

* GitHub: [Sivanarasimhulu21](https://github.com/Sivanarasimhulu21)
* LinkedIn: [Connect with me](https://www.linkedin.com/in/sivanarasimhulu621/)

---

If you find this repository useful for learning Docker and application deployment, feel free to explore the documentation and experiment with the examples.

**Let's connect and build something useful!**
