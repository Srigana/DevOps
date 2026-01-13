# Level 06: Troubleshooting and Fixing Docker Container Issues

## Task Overview
A static website running in a Docker container named **nautilus** on **App Server 1** was reported as inaccessible. The task required investigating the container's volume mapping (host `/var/www/html` to container `/usr/local/apache2/htdocs`) and ensuring the website was reachable on host port **8080**.

## Implementation

### 1. Access the Target Server
I established an SSH connection to **App Server 1** (`stapp01`) using the `tony` user credentials.

```bash
ssh tony@stapp01
```
### 2. Investigate the Problem
I initially checked for running containers but found that nautilus was not active. By running docker ps -a, I discovered the container had exited. I then inspected the container's configuration to verify the volume and port bindings.

```bash
# Check all containers (including stopped ones)
docker ps -a

# Inspect container metadata
docker inspect d3fed2e1e1b0
```
- Findings: The volume mapping was correct `(/var/www/html:/usr/local/apache2/htdocs/)`, and the port binding was set to 8080:80. However, the container was in an exited state, causing the Connection refused error when running `curl`.

### 3. Resolution: Recreate the Container
To resolve the issue, I removed the non-functional container and recreated it using the correct parameters to ensure it remained running in detached mode.

```bash
# Remove the existing failed container
docker rm nautilus

# Run a new container with correct port and volume mappings
docker run -d --name nautilus -p 8080:80 -v /var/www/html:/usr/local/apache2/htdocs httpd:latest
```

### 4. Verification
I verified that the container was "Up" and then tested the website accessibility using `curl`.

```bash
# Verify container status
docker ps

# Test website accessibility
curl http://localhost:8080/
