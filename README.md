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
<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/4798c7b0-4d5c-453d-83da-6089b865aa15" />

C) EC2 Terminal (docker-compose pull, up, ps)
<img width="1352" height="199" alt="image" src="https://github.com/user-attachments/assets/4b9451a9-6883-4d4f-9e5e-17f9e323b1b7" />
<img width="1361" height="202" alt="image" src="https://github.com/user-attachments/assets/4c6f20fa-1cfa-44d8-9d8b-5427eec97527" />
<img width="1362" height="243" alt="image" src="https://github.com/user-attachments/assets/6a7d8093-c957-4a2a-80de-45f0b13339c4" />

D) Working UI screenshot
<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/6fd66c0a-8f9c-4ce6-9780-e9aa72f573dd" />


**7) Nginx reverse proxy working**
Nginx is used as a reverse proxy to route traffic to the Angular frontend and Node backend containers.
All user traffic goes through Nginx (port 80).
Angular UI is served from /usr/share/nginx/html.
API calls /api/* are forwarded internally to:
http://backend:8080
Nginx configuration file used in (frontend/nginx.conf):

server {
    listen 80;
    server_name _;
    root /usr/share/nginx/html;
    index index.html;
    location / {
        try_files $uri $uri/ /index.html;
    }
    location /api/ {
        proxy_pass http://backend:8080/;
    }
}

**7. Live Application URL**
http://43.204.147.18 (may not work if VM is stopped)

**8. Notes**
MongoDB is running as a Docker container
Nginx serves Angular frontend on port 80
Backend accessible internally from frontend
EC2 VM will remain active for demonstration
