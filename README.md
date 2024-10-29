# devops-qoala-assignment-Divyansh-Bansal-20DEC004
Assignment for Qoala DevOps Internship.

# DevOps Internship Assignment Report

## Overview
This report documents the debugging and setup process for the DevOps internship assignment. The goal was to successfully configure, debug, and deploy a Dockerized application. Below is a chronological list of issues encountered, followed by their respective resolutions.

---

## Issues Identified and Resolution Steps

### Step 1: Cloning the Repository and Setting up Docker

1. **Warning about `version` Attribute in `docker-compose.yml`**:
   - **Issue**: When running `docker-compose up`, a warning message appeared: `the attribute version is obsolete, it will be ignored, please remove it to avoid potential confusion`.
   - **Resolution**: Removed the `version: '3.8'` line from `docker-compose.yml` as it was no longer needed.

### Step 2: Building Docker Images

1. **Python Application Dockerfile Errors**:
   - **File**: `Python/Dockerfile`
   - **Issues**:
     - `WORKDIR /appp` should be `WORKDIR /app`.
     - `COPY appy.py /app` should be `COPY app.py /app`.
     - `RUN pip install flask netiface` should be `RUN pip install flask netifaces`.
     - `EXPOSE "eight thousand"` should be `EXPOSE 8000`.
     - `CMD ["pythn", "app.py"]` should be `CMD ["python", "app.py"]`.
   - **Resolution**: Corrected each typo in `Python/Dockerfile` to ensure proper paths, ports, and command syntax.

2. **Nginx Dockerfile Errors**:
   - **File**: `nginx/Dockerfile`
   - **Issues**:
     - `FROM nginx:latests` should be `FROM nginx:latest`.
     - `COPY nginix.conf /etc/nginx/nginx.conf` should be `COPY nginx.conf /etc/nginx/nginx.conf`.
     - `COPY ./html /usr/share/nginx/htmll` should be `COPY ./html /usr/share/nginx/html`.
     - `EXPOSE "eighty"` should be `EXPOSE 80`.
     - `CMD ["nginx", "-g", "daemon of;"]` should be `CMD ["nginx", "-g", "daemon off;"]`.
   - **Resolution**: Corrected all typos in `nginx/Dockerfile` to ensure compatibility with Docker.

3. **docker-compose.yml File Errors**:
   - **File**: `docker-compose.yml`
   - **Issues**:
     - `"eighty:80"` in ports should be `80:80`.
     - `./nginx/nginx.conf:/etc/nginx/nginx.confi` should be `./nginx/nginx.conf:/etc/nginx/nginx.conf`.
     - `"eight thousand"` in `expose` should be `8000`.
     - `driver: bridg` should be `driver: bridge`.
     - `compelex_option` is misspelled and unnecessary.
   - **Resolution**: Corrected the ports, file paths, and syntax errors in `docker-compose.yml` for accurate container configuration.

### Step 3: Running the Containers with Docker Compose

1. **Nginx Configuration Error in `nginx.conf`**:
   - **File**: `nginx/nginx.conf`
   - **Issue**: When starting the containers, the Nginx container exited with the error `unknown directive "worker_process" in /etc/nginx/nginx.conf:1`.
   - **Resolution**: Updated `nginx.conf` to correct syntax errors:
     - Changed `worker_process` to `worker_processes`.
     - Fixed typos such as `mime.typess` to `mime.types` and `default_typ` to `default_type`.
   - After making these corrections, the Nginx container started without issues.

### Step 4: Accessing the Application and Testing

1. **Verifying Application in Browser**:
   - **Issue**: None. Accessing `http://localhost` in the browser displayed the application interface as expected.
   - **Resolution**: Confirmed that the application displayed the IP address, MAC address, username, and timestamp, indicating successful deployment.

2. **Checking Nginx Logs for Request Confirmation**:
   - **Issue**: None. However, logs needed to be verified to confirm that Nginx was processing requests.
   - **Resolution**: Ran `docker logs <nginx_container_id>` to check the logs for incoming requests. Verified that the requests to `http://localhost` were logged by Nginx, confirming successful proxying to the Python application.

---

## Final Notes

All identified issues were resolved, and the application was deployed successfully. The application is accessible on `http://localhost`, with Nginx and the Python application functioning as intended.

### Summary of Steps
1. Set up Docker and Docker Compose.
2. Corrected errors in `docker-compose.yml`, `Python/Dockerfile`, `nginx/Dockerfile`, and `nginx.conf`.
3. Verified the application through the browser and confirmed Nginx logs.

This README serves as documentation of the debugging process and confirms that the assignment has been completed successfully.




---
---



# Assignment :

# DevOps Assignment: Debugging and Running a Dockerized Application

Welcome to your DevOps assignment! Your goal is to debug and deploy a Dockerized application. The steps below outline the tasks you’ll complete, including setup, debugging, running, testing, and submitting your work.

## Assignment Overview

In this assignment, you’ll:
1. Set up Docker and Docker Compose.
2. Build Docker images and launch containers.
3. Debug and resolve intentional errors in the code to ensure the application runs correctly.
4. Verify the application in your browser.
5. Document your process and submit your work.

---

## Requirements

**Tools Needed:**
- **System:** Use any laptop, PC, or cloud server.
- **Tools:** Docker and Docker Compose must be installed and configured.

---

## Steps

### 1. Initial Setup
1. **Clone the GitHub Repository:**
   - Start by cloning the provided GitHub repository, which contains the `Dockerfiles`, `docker-compose.yml` file, and the application code.
   
2. **Build Docker Images:**
   - Build each Docker image locally using the provided Dockerfiles.
   - Tag each image appropriately to be referenced by the `docker-compose.yml` file.

### 2. Running the Docker Compose File
1. **Start the Containers:**
   - Use the provided `docker-compose.yml` file to launch all containers.
   - **Note:** There are intentional errors in the code. Part of your assignment is to identify and fix these errors so the application runs correctly.

### 3. Debugging and Testing
1. **Identify Issues:**
   - Check the logs for any errors while building and running containers.
   - Examine the application code, Dockerfiles, and `docker-compose.yml` file to identify intentional errors.

2. **Resolve Errors:**
   - Document the issues and explain your debugging steps.
   - Apply necessary changes to the code, Dockerfiles, or configuration to resolve these errors.

3. **Verify Website Access:**
   - Open a web browser and access the application on `http://localhost` (or `http://<server-IP>` if hosted on a cloud server) to confirm it is running correctly.
   - Check Nginx or other web server logs to confirm requests are being logged as expected.

### 4. Submitting the Assignment
1. **GitHub Repository:**
   - Create a new GitHub repository and name it in this format: `devops-qoala-assignment-<name>-<rollnumber>`.
   - Upload all relevant files (including the modified code, Dockerfiles, `docker-compose.yml`, and other configurations) to this repository.
   - Grant access to `devops@qoala.id`. **Note:** Submissions without access granted will not be considered.

2. **Screenshots:**
   - Take a screenshot of the application running in the browser.
   - Include a screenshot showing Nginx (or web server) access logs that confirm a successful request.

3. **Report:**
   - Write a concise, one-page report that includes:
     - **Issues Identified:** Summarize any errors encountered during image building, container setup, or application testing.
     - **Resolution Steps:** Describe each action taken to resolve the issues and ensure the application runs correctly.

---

## Bonus Points

### Cloud Deployment
- For extra credit, deploy the application on a cloud server (AWS, GCP, or Azure) and provide an accessible endpoint, such as an IP address or DNS record.
- This will allow your work to be verified through the shared endpoint.

---

## Summary Checklist
- Set up Docker and Docker Compose.
- Clone and build Docker images.
- Debug and fix issues in code, Dockerfiles, or `docker-compose.yml`.
- Start containers and verify application accessibility on port 80.
- Upload files to a new GitHub repository and grant access to `devops@qoala.id`.
- Submit screenshots and a concise report of issues and solutions.
- (Bonus) Deploy on a cloud provider and share endpoint details.

---
