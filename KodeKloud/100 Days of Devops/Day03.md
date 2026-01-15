# Day 03: Disable Direct SSH Root Login

## Task Overview
To comply with the new security protocols at xFusionCorp Industries, direct SSH root login had to be disabled on all application servers within the Stratos Datacenter. This reduces the attack surface by requiring users to log in with their individual accounts and elevate privileges using `sudo`.
## Implementation

### 1. Access the Application Servers
I accessed each application server (**stapp01**, **stapp02**, and **stapp03**) sequentially from the jump host using the assigned sudo user for each server.

```bash
ssh tony@stapp01
ssh steve@stapp02
ssh banner@stapp03
```
### 2. Modify SSH Configuration
On each server, I edited the SSH daemon configuration file `/etc/ssh/sshd_config`. I located the PermitRootLogin directive and changed its value from `yes` to `no`.
```bash
sudo vi /etc/ssh/sshd_config
# Changed 'PermitRootLogin yes' to 'PermitRootLogin no'
```
### 3. Validate Configuration Syntax
Before applying the changes, I ran a syntax check on the configuration file to ensure there were no errors that could potentially lock out SSH access.
```bash
sudo sshd -t
echo $?
# A return value of 0 indicates the configuration is valid
```
### 4. Apply Changes and Verify
I reloaded the sshd service to apply the new security settings without dropping current connections. Finally, I verified that the running configuration reflected the change.
```bash
# Reload the SSH service
sudo systemctl reload sshd

# Verify the active configuration for PermitRootLogin
sudo sshd -T | grep -i permitrootlogin
