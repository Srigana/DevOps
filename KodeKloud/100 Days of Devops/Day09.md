# Day 09: Troubleshooting and Fixing MariaDB Database Connectivity Issues

## Task Overview
There is a critical issue going on with the Nautilus application in Stratos DC. The production support team identified that the application is unable to connect to the database. After digging into the issue, the team found that mariadb service is down on the database server.
Look into the issue and fix the same.

### 1. Access the Database Server
I logged into the database server via SSH using the peter account to diagnose the service failure.

```bash
ssh peter@stdb01
```
### 2. Verify Service Status
I checked the current status of the MariaDB service to confirm it was inactive and to identify error codes.
```bash
sudo systemctl status mariadb
```
This confirmed the service was inactive (dead). Initial attempts to start it failed with an exit-code, indicating a filesystem or permission issue.

### 3. Analyze Service Logs
I inspected the journal logs to find the specific reason the MariaDB process was failing to initialize.
```bash
sudo journalctl -xeu mariadb --no-pager
```
The logs showed status=1/FAILURE, suggesting the service could not access its data directory or was blocked by existing process IDs.

### 4. Correct Directory Ownership
I updated the ownership of the MariaDB data directory to the correct service user.
```bash
sudo chown -R mysql:mysql /var/lib/mysql
```
This ensures the mysql user owns all database files, granting the service the necessary rights to read and write data.

### 5. Set Directory Permissions
I applied strict permissions to the data directory to satisfy service security requirements.
```bash
sudo chmod 700 /var/lib/mysql
```
This restricts access so only the mysql user can enter the directory, which is a prerequisite for the MariaDB daemon to start securely.

### 6. Remove Stale Lock Files
I deleted the socket and PID files left behind from the previous service crash.
```bash
sudo rm -f /var/lib/mysql/*.sock /var/lib/mysql/*.pid
```
These files act as "locks." Removing them prevents the service from incorrectly assuming another instance is already running.

### 7. Start and Verify the Service
I restarted the MariaDB service and verified that it reached a running state.
```bash
sudo systemctl start mariadb
sudo systemctl status mariadb
```
With the environment repaired, the service successfully transitioned to active (running).
