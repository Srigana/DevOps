# Day 08: Configuring Ansible as a Configuration Management Solution
## Task Overview
To streamline configuration management and automation across the Stratos Datacenter, the Nautilus DevOps team selected Ansible for its agentless architecture. The requirement was to set up the Jump Host as the Ansible controller by installing Ansible version `4.10.0` using `pip3`. The installation had to be global to ensure all system users could execute Ansible commands.

## Implementation
### 1. Environment Verification
I first verified the operating system and the available Python environment. The Jump Host is running `CentOS Stream 9`, and pip was confirmed to be associated with `Python 3.9`.

```bash
# Check OS release
cat /etc/os-release

# Verify pip3 version and path
python3 -m pip -V
```
### 2. Global Installation of Ansible
To ensure the binary is available globally (in `/usr/local/bin/`) and accessible to all users, I performed the installation using sudo. I specified the exact version `4.10.0` to match the team's requirements.

```bash
# Install specific Ansible version globally
sudo pip3 install 'ansible==4.10.0'
```

### 3. Verification of Binary Availability
After the installation completed, I verified that the ansible binary was correctly installed in a global path and that the version matched the request.

```bash
# Check Ansible version and executable location
ansible --version
```
- Executable Location: `/usr/local/bin/ansible`
- Python Version: 3.9.18
- Ansible Core: 2.11.12 (packaged within Ansible 4.10.0)
