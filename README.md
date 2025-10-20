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
ssh -i "my-key.pem" ubuntu@<EC2-PUBLIC-IP> ```

OR

 connect through **EC2 Instance Connect (Browser-based SSH Connection)**

 You are now inside your AWS EC2 instance.

## 3. Install Docker on EC2

1.```sudo yum update -y
sudo yum install docker -y```

2.Start Docker Service
```sudo service docker start```

3.Add Permissions
```sudo usermod -aG docker ec2-user
newgrp docker ```

4.Check Docker version
```docker --version```

#### Basic Docker Commands
Command	Description
```docker --version```	###Check Docker version###
```docker images```	###List available images###
```docker ps```	###List running containers###
```docker ps -a```	###List all containers###
```docker start <container_id>```	###Start a stopped container###
```docker stop <container_id>```	###Stop a running container###
```docker rm <container_id>```	###Remove a container###
```docker rmi <image_id>```	###Remove an image###
```docker exec -it <container_id>``` ###bash	Access container shell###
```docker logs <container_id>```	###Show container logs###
```docker system prune -a```	###Remove unused containers & images###
📝 6. Create a Dockerfile
Step 8: Create Project Directory
mkdir docker-demo
cd docker-demo

Step 9: Create a Dockerfile
nano Dockerfile


Add the following code:

# Use official OpenJDK image
FROM openjdk:11

# Copy app files
COPY . /app

# Set working directory
WORKDIR /app

# Compile or run the app
CMD ["java", "Hello"]


Save file → press Ctrl + O, Enter, then Ctrl + X

⚙️ 7. Build a Docker Image
docker build -t myapp:latest .


To verify:

docker images

▶️ 8. Run Docker Container
docker run -d -p 8080:8080 myapp:latest


-d: Run in detached mode

-p 8080:8080: Maps container port 8080 to EC2 port 8080

Check running containers:

docker ps


Stop container:

docker stop <container_id>


Remove container:

docker rm <container_id>

🌐 9. Access Application from Browser

Open in browser:

http://<EC2-Public-IP>:8080


You should see your app’s output.

🧹 10. Clean Up Docker Resources
docker stop $(docker ps -aq)
docker rm $(docker ps -aq)
docker rmi $(docker images -q)
docker system prune -a

🔁 11. Save Docker Image
Step 1: Tag image
docker tag myapp:latest your-dockerhub-username/myapp:latest

Step 2: Login to Docker Hub
docker login

Step 3: Push to Docker Hub
docker push your-dockerhub-username/myapp:latest

🧰 12. Pull Image from Docker Hub (Anywhere)
docker pull your-dockerhub-username/myapp:latest
docker run -p 8080:8080 your-dockerhub-username/myapp:latest

🧾 13. Common Troubleshooting
Issue	Fix
permission denied	Use sudo or add user to docker group
port already in use	Change port in docker run -p
Cannot connect to Docker daemon	Run sudo service docker start
Image not found	Check spelling or tag in docker build / pull
🏁 14. Summary of Commands
Task	Command
Start Docker	sudo service docker start
Build Image	docker build -t myapp .
Run Container	docker run -d -p 8080:8080 myapp
Stop Container	docker stop <id>
Remove Container	docker rm <id>
Remove Image	docker rmi <id>
Show Logs	docker logs <id>
💡 Bonus Tips

Use docker-compose to manage multiple containers.

Use Dockerfile best practices: small base images, fewer layers.

Keep your images versioned and pushed to Docker Hub.

🌍 References

Official Docker Docs

AWS EC2 User Guide

Would you like me to format this content in Markdown (README.md) and give you the ready-to-upload .md file for your GitHub repo?

You said:
ok but may be the sample helloworld image use it and docker reository login and push of image and pull of image from the docker repository u missed the two thing as per my knowledge
ChatGPT said:
Thought for 4 seconds

Good catch — thanks! ✅ I’ll add the missing pieces so your README (or guide) covers a complete Hello-World example plus Docker Hub login → tag → push → pull from start to finish. I’ll include both a generic placeholder YOUR_DOCKERHUB_USERNAME and a concrete example using your known username shimbu374 so you can copy/paste.

Quick: Hello-World example, build → run → login → push → pull
1. Create a tiny Hello-World app and Dockerfile

Make a new directory and files on your EC2 (or local machine):

mkdir hello-world-docker
cd hello-world-docker


server.js (Node example — responds with Hello World):

const http = require('http');
http.createServer((req, res) => {
  res.writeHead(200, {'Content-Type': 'text/plain'});
  res.end('Hello World from Docker!\n');
}).listen(8080, '0.0.0.0');
console.log('Server listening on 8080');


Dockerfile

FROM node:18-alpine
WORKDIR /app
COPY server.js .
EXPOSE 8080
CMD ["node", "server.js"]

2. Build image locally
docker build -t hello-world-app:1.0 .


Verify:

docker images


Run the container (test locally on EC2):

docker run -d -p 8080:8080 hello-world-app:1.0
# open http://<EC2-PUBLIC-IP>:8080 to see "Hello World from Docker!"

3. Docker Hub — login (required before push)

If you have 2FA, use a Personal Access Token instead of your password.

docker login
# Enter username (e.g. shimbu374 or YOUR_DOCKERHUB_USERNAME) and password/token


If successful, you’ll see Login Succeeded.

4. Tag the image for Docker Hub

Format: <dockerhub-username>/<repo-name>:<tag>

If your Docker Hub username is shimbu374 and the repo you created is hello-world:

docker tag hello-world-app:1.0 shimbu374/hello-world:1.0
# also tag latest if you want
docker tag hello-world-app:1.0 shimbu374/hello-world:latest


Or using placeholder:

docker tag hello-world-app:1.0 YOUR_DOCKERHUB_USERNAME/hello-world:1.0

5. Push the image to Docker Hub
docker push shimbu374/hello-world:1.0
# or for placeholder:
# docker push YOUR_DOCKERHUB_USERNAME/hello-world:1.0


You should see each layer upload and then a success message. Confirm on Docker Hub web UI under your repository Tags.

6. Pull the image on any other machine (or another EC2 / local PC)

On the other machine (no need to be logged in if the repo is public; for private repo you must docker login):

docker pull shimbu374/hello-world:1.0


Run it:

docker run -d -p 8080:8080 shimbu374/hello-world:1.0
# then open http://<that-machine-ip>:8080

7. Example: using latest tag and running
docker pull shimbu374/hello-world:latest
docker run -d -p 8080:8080 shimbu374/hello-world:latest

8. Helpful extra commands

List images: docker images

Remove local image: docker rmi shimbu374/hello-world:1.0

See push/pull history: check Docker Hub web UI → Repository → Tags

If push fails because repo missing: create repo on Docker Hub first (Repo name hello-world), or push will auto-create for your account if allowed.

9. If you use 2FA on Docker Hub

Create a Personal Access Token on Docker Hub and use that as the password with docker login.

Copy-paste snippet to add to your README.md
### Hello-World: build, push, pull example

1. Build:
   `docker build -t hello-world-app:1.0 .`

2. Tag:
   `docker tag hello-world-app:1.0 YOUR_DOCKERHUB_USERNAME/hello-world:1.0`

3. Login:
   `docker login`

4. Push:
   `docker push YOUR_DOCKERHUB_USERNAME/hello-world:1.0`

5. Pull on other machine:
   `docker pull YOUR_DOCKERHUB_USERNAME/hello-world:1.0`

6. Run:
   `docker run -d -p 8080:8080 YOUR_DOCKERHUB_USERNAME/hello-world:1.0`


If you want, I can:

Replace YOUR_DOCKERHUB_USERNAME with shimbu374 everywhere and produce a complete ready-to-commit README.md file, OR

Create that README.md and save it in your repository (I can give the file contents for you to paste).

Which would you prefer?

You said:
ok creation of the repository and projects readme file once remeber me i forgotten
ChatGPT said:

Perfect 👍 — here’s a clear reminder of how to create a GitHub repository and add your README.md file (Docker setup project) step-by-step.

🧭 1. Create a New Repository on GitHub

Go to 👉 https://github.com/new

Fill out details:

Repository name: docker-setup-environment (or any name you like)

Description: Complete Docker setup guide for AWS EC2, including build, run, push, and pull steps.

Visibility: Public (recommended for learning)

✅ Check “Add a README file”

Click Create repository.

💻 2. Clone the Repository to Your Local System or EC2
git clone https://github.com/<your-username>/docker-setup-environment.git
cd docker-setup-environment


Example for you:

git clone https://github.com/shimbu374/docker-setup-environment.git
cd docker-setup-environment

📝 3. Create or Update README.md

Create or open the file:

nano README.md


Paste this content (this is the final version, including AWS setup + Docker install + HelloWorld image build → push → pull):

# 🚀 Docker Setup Environment on AWS EC2

This guide helps you **set up Docker on AWS EC2**, create a **sample Hello World app**, build an image, run a container, and push/pull it from **Docker Hub**.

---

## 🧩 Step 1: AWS Account Setup

1. Go to [https://aws.amazon.com/](https://aws.amazon.com/)
2. Click **Create an AWS Account**.
3. Complete the signup process using your email, password, and payment method (free tier available).
4. Log in to the AWS **Management Console** → search for **EC2**.
5. Launch a new **EC2 Instance**:
   - OS: Ubuntu (recommended)
   - Type: t2.micro (Free Tier)
   - Storage: Default (8–10 GB)
   - Key Pair: Create/Download `.pem` file
6. Connect to the instance:
   ```bash
   chmod 400 my-key.pem
   ssh -i my-key.pem ubuntu@<ec2-public-ip>

🐳 Step 2: Install Docker on EC2
sudo apt update -y
sudo apt install docker.io -y
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -aG docker ubuntu


Logout and re-login to apply permissions.

Check:

docker --version
docker ps

🧱 Step 3: Create a Hello World App
mkdir hello-world-docker
cd hello-world-docker


server.js

const http = require('http');
http.createServer((req, res) => {
  res.writeHead(200, {'Content-Type': 'text/plain'});
  res.end('Hello World from Docker!\n');
}).listen(8080, '0.0.0.0');
console.log('Server running on port 8080');


Dockerfile

FROM node:18-alpine
WORKDIR /app
COPY server.js .
EXPOSE 8080
CMD ["node", "server.js"]

🧰 Step 4: Build and Run Docker Image
docker build -t hello-world-app:1.0 .
docker images
docker run -d -p 8080:8080 hello-world-app:1.0


Check in browser:

http://<EC2-PUBLIC-IP>:8080

🧾 Step 5: Docker Hub Login and Push

Log in to Docker Hub: https://hub.docker.com/

Create a repository named hello-world.

Then in terminal:

docker login
docker tag hello-world-app:1.0 shimbu374/hello-world:1.0
docker push shimbu374/hello-world:1.0


Check repository on Docker Hub → it should show your image.

🔁 Step 6: Pull and Run Image Anywhere

On another machine or EC2 instance:

docker pull shimbu374/hello-world:1.0
docker run -d -p 8080:8080 shimbu374/hello-world:1.0


Open:

http://<machine-public-ip>:8080

⚙️ Step 7: Common Docker Commands
Command	Description
docker ps	Show running containers
docker ps -a	Show all containers
docker images	List images
docker stop <container_id>	Stop container
docker rm <container_id>	Remove container
docker rmi <image_id>	Remove image
docker logs <container_id>	View logs
docker exec -it <container_id> /bin/sh	Access container shell
🧹 Step 8: Clean Up
docker stop $(docker ps -q)
docker rm $(docker ps -aq)
docker rmi $(docker images -q)

✅ Summary

You learned how to:

Set up AWS EC2 and install Docker

Create and build a Docker image

Run containers and test in browser

Push and pull images using Docker Hub

Use common Docker commands efficiently

Author: Narasimha SL (@shimbu374
)
Project: Docker Setup Environment on AWS


---

## 📤 4. Commit and Push to GitHub

```bash
git add README.md
git commit -m "Added complete Docker setup guide with AWS and Docker Hub steps"
git push origin main


Now your GitHub repository will show a full, step-by-step Docker setup guide.
Would you like me to include screenshots section placeholders (like “Attach EC2 instance image”, “Docker Hub repository screenshot”) in the README too? It makes it look more professional if you’re submitting it for training or internship purposes.
