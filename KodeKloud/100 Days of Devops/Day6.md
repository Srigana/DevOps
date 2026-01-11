# Day 06: Automating Tasks with Cron Jobs

## Task Overview
The Nautilus system administration team required the deployment of a sample cron job across **all application servers** (stapp01, stapp02, and stapp03) in the Stratos Datacenter. The goal was to validate the automation environment by installing the `cronie` package, ensuring the service was active, and scheduling a recurring task for the root user.

## Implementation

### 1. Access the Application Servers
I performed the following steps on each server sequentially: **App Server 1** (`stapp01`), **App Server 2** (`stapp02`), and **App Server 3** (`stapp03`). 

```bash
ssh tony@stapp01
ssh steve@stapp02
ssh banner@stapp03
```
### 2. Install Cronie Package
On each server, I utilized the `yum` package manager to install the cronie package. This package contains the `crond` daemon which manages scheduled executions.

```bash
sudo yum install cronie -y
```

### 3. Start and Enable the Cron Service
After installation, I ensured the `crond` service was running and configured to start automatically upon system boot.

```bash
# Start the cron daemon
sudo systemctl start crond.service

# Enable the service for persistence
sudo systemctl enable crond

# Verify the service is active
sudo systemctl status crond
```
### 4. Schedule the Cron Job for Root
I accessed the crontab configuration for the root user on each server. I added the requested schedule: `*/5 * * * *`, which instructs the system to run the command every 5 minutes.

```bash
# Open root's crontab for editing
sudo crontab -e

# Inserted the following line:
# */5 * * * * echo hello > /tmp/cron_text
```

### 5. Verification
I verified that the cron job was successfully registered in the system by listing the active crontab entries for the root user.

```bash
sudo crontab -l
