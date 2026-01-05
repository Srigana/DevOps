# Level 02: Deploying Nginx Container on App Server 1

## Task Overview
As part of the Nautilus DevOps team's application deployment testing, I was required to deploy a specific web server container on **App Server 1**. The goal was to run an Nginx instance using a lightweight image and ensure it remained in a running state.

## Implementation Steps

### 1. Identify Requirements
The task specified the following parameters for the deployment:
* **Target Server:** App Server 1 (`stapp01`)
* **Container Name:** `nginx_1`
* **Image:** `nginx`
* **Tag:** `alpine`

### 2. Deploy the Container
I used the `docker run` command with the `-d` (detached) flag. This ensures the container runs in the background. I explicitly defined the name and the specific `alpine` tag to minimize the image footprint.

### 3. Verify Container Status
After deployment, I checked the list of active containers to confirm that `nginx_1` was created successfully, was using the correct image, and showed a status of `Up`.

---

## Commands Executed

```bash
# Deploy the Nginx container in detached mode
docker run -d --name nginx_1 nginx:alpine

# Verify that the container is running and check its status
docker ps
```
## Final Result
The container `nginx_1` was successfully deployed on App Server 1. The `docker ps` output confirmed the container is active and running on port 80/tcp, using the `nginx:alpine` image as requested.
