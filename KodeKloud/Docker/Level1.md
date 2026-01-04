# Level 01: Install Docker and Docker Compose on App Server 1

## Task Overview
The Nautilus DevOps team required the installation and configuration of Docker and Docker Compose on **App Server 1** (`stapp01`) to begin containerizing applications. The goal was to ensure the Docker engine is installed, the service is enabled and running, and the installation is verified.

## Implementation Steps

### 1. Access the Target Server
I established an SSH connection from the jump host to **App Server 1** using the authorized user credentials.

### 2. Prepare the Repository
Since the server uses a RHEL-based system (CentOS Stream 9), I installed `yum-utils` to manage the software repositories. I then added the official Docker CE repository to the system.

### 3. Install Docker Packages
I installed the Docker community edition engine, the CLI, the containerd runtime, and the Docker Compose plugin.

### 4. Enable and Start Docker Service
I configured the Docker daemon to start automatically on boot and initiated the service immediately using the `systemctl` command.

### 5. Verification
I verified the installation by running a test `hello-world` container. This confirmed that the Docker daemon could pull images from Docker Hub and execute containers correctly.

---

## Commands Executed

```bash
# Connect to App Server 1
ssh tony@stapp01

# Install repository management tools
sudo yum install -y yum-utils

# Add the official Docker repository
sudo yum-config-manager --add-repo [https://download.docker.com/linux/rhel/docker-ce.repo](https://download.docker.com/linux/rhel/docker-ce.repo)

# Install Docker CE and Docker Compose
sudo yum install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# Enable and start the Docker service
sudo systemctl enable --now docker

# Verify the installation with a test container
sudo docker run hello-world
```
## Final Result
Docker and Docker Compose were successfully installed on App Server 1. The `hello-world` container executed successfully, displaying the "Hello from Docker!" confirmation message, indicating the environment is ready for containerized testing.
