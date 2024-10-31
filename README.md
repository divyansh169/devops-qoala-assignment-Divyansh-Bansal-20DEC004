# devops-qoala-assignment-Divyansh-Bansal-20DEC004
Assignment for Qoala DevOps Internship.

Cloud Deployment Accessible Endpoint IP Address : http://34.68.254.225/

# DevOps Internship Assignment Report

## Overview
This report documents the debugging and setup process for the DevOps internship assignment. The goal was to successfully configure, debug, and deploy a Dockerized application. Below is a chronological list of issues encountered, followed by their respective resolutions.

---

## Issues Identified and Resolution Steps

### Step 1: Cloning the Repository and Setting up Docker

1. **docker-compose.yml File Errors**:
   - **File**: `docker-compose.yml`
   - **Issues**:
     - `"eighty:80"` in ports should be `80:80`.
     - `./nginx/nginx.conf:/etc/nginx/nginx.confi` should be `./nginx/nginx.conf:/etc/nginx/nginx.conf`.
     - `"eight thousand"` in `expose` should be `8000`.
     - `driver: bridg` should be `driver: bridge`.
     - `compelex_option` is misspelled and unnecessary.
   - **Resolution**:
     - Corrected the ports, file paths, and syntax errors in `docker-compose.yml` for accurate container configuration.
     - Used bridge for network and removed complex options unless needed.

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
     - Error of `COPY ./html /usr/share/nginx/html` command in the Nginx Dockerfile failing because the html folder is missing in the nginx directory.
   - **Resolution**:
     - Corrected all typos in `nginx/Dockerfile` to ensure compatibility with Docker.
     - Created a folder with name `html` inside the `nginx` folder.

### Step 3: Running the Containers with Docker Compose

1. **Warning about `version` Attribute in `docker-compose.yml`**:
   - **Issue**: When running `docker-compose up`, a warning message appeared: `the attribute version is obsolete, it will be ignored, please remove it to avoid potential confusion`.
   - **Resolution**: Removed the `version: '3.8'` line from `docker-compose.yml` as it was no longer needed.

2. **Nginx Configuration Error in `nginx.conf`**:
   - **File**: `nginx/nginx.conf`
   - **Issue**: When starting the containers, the Nginx container exited with the error `unknown directive "worker_process" in /etc/nginx/nginx.conf:1`.
   - **Resolution**: Updated `nginx.conf` to correct syntax errors:
     - Changed `worker_process` to `worker_processes`.
     - `worker_process auto` to `worker_processes auto;`
     - `worker_connection 1024;` to `worker_connections 1024;`
     - Fixed typos such as `mime.typess` to `mime.types` and `default_typ` to `default_type`.
   - After making these corrections, the Nginx container started without issues.

---
## Cloud Deployment Accessible Endpoint IP Address

### External IP Address : http://34.68.254.225/
---

## Commands Procedure Used (Sequentially)

Below is the list of commands used during the assignment in sequential order:

1. `docker --version`
2. `docker-compose --version`
3. `git clone https://github.com/qoala-engineering/devops-internship-challenge.git`
4. `cd devops-internship-challenge`
5. `docker build -t local-python-app ./Python`
6.  Created a folder with name `html` inside the `nginx` folder.
7. `docker build -t local-nginx ./nginx`
8. `docker images`
 ```
REPOSITORY         TAG       IMAGE ID       CREATED              SIZE
local-nginx        latest    cbd752383c30   About a minute ago   192MB
local-python-app   latest    bc3fbfe6dd89   11 minutes ago       1.01GB
 ```
9. `docker-compose down`
10. `docker-compose up`
11. Accessed `http://localhost` in the browser, which displayed the following details:
 ```
 IP Address: 172.18.0.3

 MAC Address: 00:00:00:00:00:00

 Username: Guest

 Timestamp: 2024-10-29 20:01:48

 Assignment completed successfully!
 ```
12. `docker ps`
 ```
CONTAINER ID   IMAGE              COMMAND                  CREATED          STATUS          PORTS                NAMES
26f31efc3073   local-nginx        "/docker-entrypoint.…"   13 minutes ago   Up 13 minutes   0.0.0.0:80->80/tcp   devops-internship-challenge-nginx-1
deb13ef18752   local-python-app   "python app.py"          13 minutes ago   Up 13 minutes   8000/tcp             python_app
 ```
13. `docker logs <nginx_container_id>` -> `docker logs 26f31efc3073`
14. **Logs confirmed** that Nginx was successfully handling requests, indicating a successful setup.
 ```
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
172.18.0.1 - - [29/Oct/2024:20:01:46 +0000] "GET / HTTP/1.1" 200 305 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/130.0.0.0 Safari/537.36"
172.18.0.1 - - [29/Oct/2024:20:01:48 +0000] "GET / HTTP/1.1" 200 305 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/130.0.0.0 Safari/537.36"
172.18.0.1 - - [29/Oct/2024:20:01:49 +0000] "GET /favicon.ico HTTP/1.1" 404 207 "http://localhost/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/130.0.0.0 Safari/537.36"
 ```

### Cloud Deployment

15. Compute Engine -> VM instances  
16. Name VM, `devops-docker-app`, zone `us-central1-f`, `e2-micro`, `Ubuntu`, Allow HTTP traffic and Allow HTTPS traffic  
17. Open SSH  
18. `sudo apt update`  
19. `sudo apt install -y docker.io`  
20. `sudo systemctl start docker`  
    `sudo systemctl enable docker`  
21. `docker --version`  
22. `sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose`  
23. `sudo chmod +x /usr/local/bin/docker-compose`  
24. `docker-compose --version`  

25. Open new SSH  
26. Click upload file and upload project zip file  
27. `unzip devops-internship-challenge.zip -d ~/app`  
28. `cd ~/app`  
29. `ls` (to verify)  
30. `cat docker-compose.yaml`  
31. Build and Start the Application  
    ```
    cd ~/app/nginx
    sudo docker build -t local-nginx .
    cd ~/app/Python
    sudo docker build -t local-python-app .
    cd ~/app
    ```
32. `sudo docker-compose up -d`  
33. `sudo docker-compose ps` (to check the status)  
    ```
    divyanshbansal169@devops-docker-app:~/app$ sudo docker-compose ps
       Name                  Command               State                Ports              
    ---------------------------------------------------------------------------------------
    app_nginx_1   /docker-entrypoint.sh ngin ...   Up      0.0.0.0:80->80/tcp,:::80->80/tcp
    python_app    python app.py                    Up      8000/tcp   
    ```

34. Accessible Endpoint: External IP address : `http://34.68.254.225/`
    ```
    IP Address: 172.18.0.2

    MAC Address: 00:00:00:00:00:00

    Username: Guest

    Timestamp: 2024-10-31 11:19:45

    Assignment completed successfully!
    ```


---

## Conclusion

All identified issues were resolved, and the application was deployed successfully. The application is accessible on `http://localhost`, with Nginx and the Python application functioning as intended. Accessing `http://localhost` in the browser displayed the application interface as expected. Confirmed that the application displayed the IP address, MAC address, username, and timestamp, indicating successful deployment. Ran `docker logs <nginx_container_id>` to check the logs for incoming requests. Verified that the requests to `http://localhost` were logged by Nginx, confirming successful proxying to the Python application. Also did the the cloud deployment at the Accessible Endpoint IP Address http://34.68.254.225/ .

### Summary of Steps
1. Set up Docker and Docker Compose.
2. Corrected errors in `docker-compose.yml`, `Python/Dockerfile`, `nginx/Dockerfile`, and `nginx.conf`.
3. Verified the application through the browser and confirmed Nginx logs.
4. Deployed the application on cloud.
5. Accessible Endpoint IP Address http://34.68.254.225/

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
