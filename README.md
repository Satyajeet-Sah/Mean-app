**MEAN Stack – DevOps Assignment**

This repository contains the MEAN stack application containerized, deployed on AWS EC2, and integrated with GitHub Actions for CI/CD.

**1. Project Overview**
This assignment demonstrates:
A) Containerizing Angular (frontend) and Node.js/Express (backend)
B) Running MongoDB using official Docker image
C)Deploying all services using Docker Compose on an EC2 Ubuntu VM
C) Nginx reverse proxy running on port 80
E) CI/CD pipeline using GitHub Actions (Build & Push successful)

**2. Architecture Diagram**
Browser → Nginx → Angular → Backend API → MongoDB
All services run inside Docker containers.

**3. Docker Images (Docker Hub)**
Service	Docker Hub Images:
1) Frontend	https://hub.docker.com/r/sahsatyajeet/ddtask-frontend
2) Backend https://hub.docker.com/r/sahsatyajeet/ddtask-backend
3) MongoDB - mongo:6
   
**4. Deployment Steps (Manual Deployment on EC2)**
SSH into EC2
ssh -i key.pem ubuntu@<EC2-IP>

Go to project folder
cd ~/ddtask

Pull the latest Docker images
docker compose pull

Start the application
docker compose up -d

Check running containers
docker ps

All 3 containers should be running:
ddtask-frontend-1
ddtask-backend-1
ddtask-mongo-1

**5. CI/CD Pipeline – GitHub Actions**
✔ Build & Push Job — SUCCESS

The pipeline:
Builds frontend Docker image
Builds backend Docker image
Pushes both to Docker Hub

✔ Deploy Job — Configured

SSH deployment requires additional permission setup.
Manual deployment works successfully and reliably.

**6. Screenshots**
A) GitHub Actions build screenshot
<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/2a1a7361-268e-425f-83df-d8e66e8b4737" />


B) Docker Hub images

C) EC2 Terminal (docker-compose pull, up, ps)

4) Working UI screenshot (http://<EC2-IP>/)

5) Nginx reverse proxy working

**7. Live Application URL**
http://72.31.3.181

**8. Notes**
MongoDB is running as a Docker container
Nginx serves Angular frontend on port 80
Backend accessible internally from frontend
EC2 VM will remain active for demonstration
