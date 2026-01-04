# Day 01: Linux User Setup With Non-Interactive Shell

## Task Overview
The system admin team at xFusionCorp Industries required a user account to be created on **App Server 1**. This user is intended for a backup agent, meaning it must be restricted from interactive logins or shell access. The required username for this task was **kirsty**.

## Implementation Steps

### 1. Server Access
I identified that the task must be performed directly on **App Server 1** rather than the jump host. I established an SSH connection to the server using the appropriate credentials.

### 2. Environment Verification
Before applying changes, I verified the hostname to ensure I was operating on the correct target server.

### 3. User Creation
I created the user account with a specific flag to assign a non-interactive shell. By setting the shell to `/sbin/nologin`, the account is functional for system services but prevents any human user from obtaining a terminal prompt.

### 4. Final Verification
I checked the system's password database to confirm the user was created successfully and that the shell attribute was correctly applied.

---

## Commands Executed

```bash
# Connect to App Server 1
ssh tony@stapp01

# Verify the current hostname
hostname

# Create user with a non-interactive shell
sudo useradd -s /sbin/nologin kirsty

# Confirm user details and shell assignment
getent passwd kirsty
```
## Final Result
The user kirsty was successfully created on App Server 1. The verification command confirmed the login shell is set to /sbin/nologin, ensuring the account is restricted to service-only use as requested.
