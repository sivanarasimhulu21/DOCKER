# Statement:
**An organization ABC  Private Limited has recently transformed their IT application from Monolithic to Microservice Architecture. Now they have been struggling  with deployment in such a complex infrastructure and inconsistency across the system.
The organization has hired you to help them with simplifying their deployment process by containerizing their applications. They are using spring boot to develop their microservices. So we need to deploy our application in a container.**
<br><br>
## Step 1 : Create or  download a Spring Boot application with Spring initializer.
=> Creation or instialling the project from the offical spring boot web site[https://start.spring.io/]
<br>
## Step 2: Customize the application as per your needs and make a complete application.
=>Write the Some thing to display in the page. you  can use the HTML or any thing that must display the some thing in the screen.
=>This application we are going to containerize.
<br>
## step 3:upload the project into the Github  
  Go into the project directory then follow the commands
  Before follow this commands create a GitRepository then follow
  ```
git clone https://github.com/your-username/your-repo.git

git branch
git branch -M main
Git init
git add .
git commit -m "This is discreption you can add any thing"
git push -u origin main
```
# if you have installed the docker in your local Machine then this is optional for you (skip)  

<br>

### 2.Login into the AWS account  
By Entering the valied details Login into AWS Account

<br>


### 3.Start the EC2 instance and then connect the instance(virtual OS)  
Connect to the Ec2 Instance

<br>

## Step 4.clone the project from the git hub 
git clone
or  
if want the direct project link than the above one is useful that without creation of the project directly Containerization and Deployment of the project  
 
#### After getting of the project into your repository follow the steps 


```mvn clean package 
ls -l target
 docker ps
```

<br>

<br>

## Step 5 : Write a Dockerfile for containerizing our application.
Add this  file into the same folder of the Application 
```
FROM openjdk:17-jdk-slim

WORKDIR /usr/app

COPY target/*.jar app.jar

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app.jar"]
```

<br>

<br>

## Step 6: Create a Docker image from the Dockerfile.
`docker build -t springbootapp .`  


<br>

<br>

## Step 7 : Push the Docker image to Dockerhub.(if You Want)
After successfully creation of the Image then you can push the image in the dockerhub by following the give steps  
First login into the dockerhub  
 `docker login`
 
 Enter your docker hub account credentials.  
  Now tag docker image    
 Tag the local image correctly
`docker tag <image name> <username>/<tag-name>:latest`

 Push to Docker Hub
 
`docker push <user name>/<tag- name>:latest`


This is the Uploading the docker image into docker hub by using the pull command you can directly run this image in you instance  
`docker pull <user-name>/<tag-name>:latest`

<br>

<br>

 
## Step 8 : make your containerized application in the runnable state.
` docker run -d -p 8080:8080 springbootapp`
<br><br><br><br><br><br>


Congratulations! By following this documentation, you’ve successfully explored the complete lifecycle of a Spring Boot application — from   development to containerized deployment using Docker.  <br><br><br>



This project not only showcases practical implementation but also equips you with the skills to adapt, extend, and scale applications efficiently.   Every step has been designed to ensure clarity, consistency, and reliability across environments.  <br><br><br>


  
We encourage you to experiment, innovate, and make this project your own. If you have any questions, ideas, or need guidance, don’t hesitate to   reach out — your curiosity and feedback are always welcome!  <br><br><br>


 
Thank you for taking the time to go through this guide. We hope you found it insightful, inspiring, and easy to follow.  <br><br><br>



**Author:** Chittiboina Siva Narasimhulu  
**Project:** Spring boot Application creation and Deployment  
