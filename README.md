#  Docker Environment Setup on AWS EC2
This document explains how to set up Docker on an **AWS EC2 instance**, from account creation to container execution. 

## 1: Create and Log in to Your AWS Account
1. Go to [https://aws.amazon.com/](https://aws.amazon.com/).
2. Click **Create an AWS Account**.
3. Enter your email, password, and billing details.
4. Once logged in, go to **AWS Management Console**.
5. Search for **EC2** → **Launch Instance**.

### Instance Configuration:
- **Name:** Docker-Setup
- **AMI (OS):** Ubuntu Server 22.04 LTS
- **Instance Type:** t2.micro (Free Tier)
- **Storage:** 8 GB (default)
- **Key Pair:** Create and download `.pem` file
- **Security Group:** Allow ports `22` (SSH) and `8080` (for web app access)
Click **Launch Instance** 


## 2: Connect to EC2 Instance
From your terminal:
```bash
chmod 400 my-key.pem
ssh -i "my-key.pem" ubuntu@<EC2-PUBLIC-IP>
 ```

OR

 connect through **EC2 Instance Connect (Browser-based SSH Connection)**

 You are now inside your AWS EC2 instance.

## 3. Install Docker on EC2
1.For Install Docker
```sudo yum update -y
sudo yum install docker -y
```

2.Start Docker Service
```sudo service docker start
```

3.Add Permissions
```sudo usermod -aG docker ec2-user
newgrp docker
```
4.Check Docker version
```docker --version
```
-------------------------------------------------------------------------------
| **Command**                           | **Description**                   |
| ------------------------------------- | --------------------------------- |
| `docker --version`                    | Check Docker version              |
| `docker images`                       | List available images             |
| `docker ps`                           | List running containers           |
| `docker ps -a`                        | List all containers               |
| `docker start <container_id>`         | Start a stopped container         |
| `docker stop <container_id>`          | Stop a running container          |
| `docker rm <container_id>`            | Remove a container                |
| `docker rmi <image_id>`               | Remove an image                   |
| `docker exec -it <container_id> bash` | Access container shell            |
| `docker logs <container_id>`          | Show container logs               |
| `docker system prune -a`              | Remove unused containers & images |
-------------------------------------------------------------------------------
## 4 Sample Docker  file creation
```
FROM ubuntu
MAINTAINER Shimbu<Shimbu@123.com>
RUN echo "Hi, i am run - 1"
RUN echo "Hi, i am run - 2"
RUN echo "Hi, i am run - 3"

CMD echo "Hi, i am CMD-1"
CMD echo "Hi, i am CMD-2"
CMD echo "Hi, i am CMD-3"
```
=> 1 Create Project Directory
```mkdir docker-demo
cd docker-demo
```
=> Create a file (filename: Dockerfile)
` vi Dockerfile`

=> Copy above sample docker file content and keep in docker file  (Esc + :wq)

=> Create docker image using Dockerfile

`docker build -t <image-name> `

=> login into docker hub account from docker machine
` docker login`

**Note:** Enter your docker hub account credentials.
	
=> tag docker image
` docker tag <image-name> <tagname>`

**Ex :**  ` docker tag myimg1 ashokit/myimg1`

=>Push Docker image

` docker push <Tag-name>`

=> we  can use user defined name for Dockerfile 
` docker build -f <filename> -t <imagename> `




