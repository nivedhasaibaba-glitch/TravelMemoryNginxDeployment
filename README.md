# TravelMemoryNginxDeployment
#  TravelMemory - MERN Stack Deployment on AWS EC2

##  Project Overview

TravelMemory is a full-stack MERN (MongoDB, React, Node.js) application that allows users to share and manage travel memories.

This project demonstrates deployment of a scalable, production-ready web application on AWS using EC2, NGINX, PM2, Load Balancer, MongoDB Atlas, and Cloudflare.

---

##  Live Architecture Flow
User → Cloudflare → AWS Load Balancer → Frontend EC2 → Backend EC2 → MongoDB Atlas

---

##  Technologies Used

- React.js (Frontend)
- Node.js (Backend)
- Express.js
- MongoDB Atlas (Database)
- AWS EC2 (Compute)
- AWS Application Load Balancer
- NGINX (Reverse Proxy)
- PM2 (Process Manager)
- Cloudflare (DNS + SSL + CDN)
- Git & GitHub

# STEP-BY-STEP DEPLOYMENT GUIDE
# STEP 1: Launch AWS EC2 Instance

1. Go to AWS Console → EC2
2. Launch Ubuntu 22.04 instance
3. Configure security group:

### Open Ports:
- 22 (SSH)
- 80 (HTTP)
- 443 (HTTPS)
- 3000 (Backend)
- 3001 (Frontend)

4. Download `.pem` key

 ## STEP 2: Connect to EC2
 
 ## STEP 3: Update Server
 sudo apt update && sudo apt upgrade -y
 
 ## STEP 4: Install Dependencies
 curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt install nodejs -y
sudo apt install git -y
sudo apt install nginx -y
sudo npm install -g pm2

## STEP 5: Clone Repository
git clone https://github.com/UnpredictablePrashant/TravelMemory.git
cd TravelMemory

## STEP 6: MongoDB Atlas Setup
Create cluster in MongoDB Atlas
Allow IP access (0.0.0.0/0)
Copy connection string


## STEP 7: Backend Setup
cd backend
npm install
nano .env

# Start backend:
pm2 start index.js --name backend
pm2 save
pm2 startup


## STEP 8: Frontend Setup

cd ../frontend/src
nano urls.js

# Build frontend:
cd ..
npm install
npm run build

# Run frontend:
sudo npm install -g serve
pm2 start "serve -s build -l 3001" --name frontend
pm2 save


## STEP 9: Configure NGINX
sudo nano /etc/nginx/sites-available/travelmemory
Add env file
# Enable:
sudo ln -s /etc/nginx/sites-available/travelmemory /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl restart nginx


## STEP 10: Load Balancer Setup

Create AWS Application Load Balancer
# Create Target Groups:
Frontend (3001)
Backend (3000)
Register multiple EC2 instances
Add routing rules:
/ → Frontend
/api → Backend


## STEP 11: Domain & Cloudflare Setup
Created Domain in Namecheap

Add domain to Cloudflare
Update nameservers

A Record → EC2 IP
CNAME → Load Balancer DNS

SSL Mode: FULL
Enable Always HTTPS

## STEP 12: Scaling
Launch multiple EC2 instances using AMI
Attach to Load Balancer
Enables high availability


## ARCHITECTURE
User
→ Cloudflare
→ Load Balancer
→ Frontend EC2
→ Backend EC2
→ MongoDB Atlas

## CONCLUSION

This project demonstrates a production-ready scalable MERN deployment using AWS cloud infrastructure with high availability, security, and performance optimization.

## AUTHOR
## Nivedha S




