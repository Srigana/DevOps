# Day 04: Granting Executable Permissions to Backup Script

## Task Overview
The xFusionCorp Industries sysadmin team distributed a new automation script, `xfusioncorp.sh`, to all servers. However, on **App Server 1**, the script was uploaded without the necessary executable permissions. The requirement was to modify the permissions of `/tmp/xfusioncorp.sh` so that every user on the system has the capability to execute it.

## Implementation

### 1. Access the Target Server
I initiated an SSH connection to **App Server 1** (`stapp01`) from the jump host using the `tony` user credentials.

```bash
ssh tony@stapp01
```
### 2. Modify Permissions
I initially attempted to change the permissions using `chmod 755`, but the operation was denied because the file is owned by root. I then used `sudo` to apply the changes. The mode `755` (`rwxr-xr-x`) ensures the owner has full permissions, while the group and others have read and execute permissions.
```bash
sudo chmod 755 /tmp/xfusioncorp.sh
```
### 3. Verify Permission Changes
To confirm the changes were applied correctly, I used the `ls -l` command to inspect the file's permission string.
```bash
ls -l /tmp/xfusioncorp.sh
