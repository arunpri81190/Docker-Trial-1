# Docker + Apache Static Website on AWS EC2

## Objective
Deploy a multi‑page static website (Home, About, Contact) using Docker and Apache on an AWS EC2 instance.  
Demonstrate containerization, file transfer, and port mapping as part of a DevOps workflow.

---

## Environment Setup
- **Platform:** AWS EC2 (Ubuntu)
- **Tools:** Docker, Apache (`httpd` base image)
- **Access:** SSH with `.pem` key
- **Networking:** Security Group temporarily set to allow **ALL TCP** for testing

---

## Project Structure
/home/ubuntu/mywebsite/
  - Dockerfile
  - index.html
  - about.html
  - contact.html
  - style.css
  - script.js
  - Docker Project Documentation.docx
  - images
      - logo.png
---

## File Transfer
From Windows → EC2 using SCP:
scp -i path/to/key.pem "C:\Users\aruns\OneDrive\Desktop\logo.png" ubuntu@<public-ip>:/home/ubuntu/mywebsite/images/

Fix ownership if folder created by root:
sudo chown -R ubuntu:ubuntu /home/ubuntu/mywebsite/images

Fix ownership if folder created by root:
sudo chown -R ubuntu:ubuntu /home/ubuntu/mywebsite/images

Docker File:
FROM httpd:latest
COPY . /usr/local/apache2/htdocs/
EXPOSE 80

Build and Run:
Build Image:
cd /home/ubuntu/mywebsite
docker build -t arunweb:site .
Run Image:
docker run -itd --name webserver-site -p 8010:80 arunweb:site

Access:
- Home → http://<public-ip>:8010
- About → http://<public-ip>:8010/about.html
- Contact → http://<public-ip>:8010/contact.html

Troubleshooting Notes
- Permission denied (SCP): Fixed by correcting folder ownership (chown)
- Container name conflict: Resolved by stopping/removing old container (docker rm)
- Port already allocated: Identified with docker ps, freed by stopping/removing container or using a new port

Portfolio Evidence
- Screenshot of site running in browser
- docker ps output showing container and port mapping
- Dockerfile and project structure
- SCP transfer commands and permission fix

Outcome
Successfully deployed a multi‑page static website on Docker + Apache inside AWS EC2.

Demonstrated:
- Containerization workflow
- File transfer and permission management
- Port mapping and networking setup
- Integration of multiple pages with consistent navigation
