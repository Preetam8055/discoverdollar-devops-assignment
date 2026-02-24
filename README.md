# DevOps Assignment — Containerized Full Stack Deployment

## Project Overview

This project demonstrates an end-to-end DevOps workflow:

* Run the application locally
* Containerize using Docker
* Configure multi-container setup using Docker Compose
* Deploy to AWS EC2
* Prepare for CI/CD automation

The objective is to make the application production-ready and publicly accessible.

---

## Tech Stack

| Layer            | Technology                             |
| ---------------- | -------------------------------------- |
| Frontend         | UI Provided                            |
| Backend          | Node.js (Express)                      |
| Database         | MySQL / MongoDB (update accordingly)   |
| Containerization | Docker & Docker Compose                |
| Cloud            | AWS EC2                                |
| Automation       | GitHub Actions / Jenkins (in progress) |

---

## Deployment Steps Performed

### 1. Run Application Locally

Installed dependencies and started the backend server.

```
npm install
npm start
```

Verified that the application UI loads in the browser.

---

### 2. Dockerization

Created a Dockerfile to containerize the backend:

* Used Node base image
* Copied package files
* Installed dependencies
* Exposed application port
* Started server

Build and run:

```
docker build -t app .
docker run -p 3000:3000 app
```

---

### 3. Multi-Container Setup (Docker Compose)

Configured application and database containers.

```
docker-compose up --build
```

---

### 4. Cloud Deployment (AWS EC2)

Steps performed:

1. Launched EC2 instance
2. Installed Docker and Docker Compose
3. Pulled project from GitHub
4. Started containers
5. Configured Security Group ports

Application accessible at:

```
http://<EC2-Public-IP>:3000
```

---

## Issue Faced

### Problem

The application UI loaded successfully but submitted data was not stored in the database.

The issue occurred in:

* Local environment
* Docker containers
* Cloud deployment

---

## Root Cause

The backend could not communicate correctly with the database due to incorrect connection configuration.

Containers were running correctly, but the database host configuration caused failed insert operations.

---

## Solution Implemented

1. Added request logging to verify API call:

```
console.log(req.body);
```

2. Verified database connection status

3. Corrected database host configuration:

```
localhost  -> incorrect inside container
db         -> correct Docker service name
```

4. Restarted containers:

```
docker-compose down -v
docker-compose up --build
```

After fix:

* Data stored successfully
* Working locally
* Working in Docker
* Working in EC2

---

## CI/CD (In Progress)

Next steps:

* Build Docker image automatically
* Push image to registry
* Deploy automatically to EC2

---

## Current Status

| Stage              | Status      |
| ------------------ | ----------- |
| Local Run          | Completed   |
| Dockerized         | Completed   |
| Cloud Deploy       | Completed   |
| Functional Testing | Completed   |
| CI/CD Automation   | In Progress |

---

## Conclusion

This project validates practical DevOps skills including debugging deployment issues, container networking, and preparing an application for automated production deployment.

---
