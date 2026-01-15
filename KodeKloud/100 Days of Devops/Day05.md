# Day 05: SELinux Installation and Configuration

## Task Overview
In response to a security audit at xFusionCorp Industries, the security team decided to implement SELinux across application servers. For the initial phase on **App Server 2**, the requirement was to install the necessary SELinux management packages but ensure the system remains in a **disabled** state following the next scheduled reboot.

## Implementation

### 1. Access the Target Server
I attempted to log into App Server 1, but due to a host key verification failure, I proceeded to **App Server 2** (`stapp02`) as per the specific task requirements. I connected via SSH using the `steve` user account.
```bash
ssh steve@stapp02
```
### 2. Identify Operating System
I checked the `/etc/os-release` file to confirm the package manager requirements. The server is running CentOS Stream 9, which uses `yum` (or dnf) for package management.
```bash
cat /etc/os-release
```
### 3. Install SELinux Packages
I installed the essential SELinux policy and management tools. These packages are necessary for defining security contexts and managing policies once the team is ready to enforce them.
```bash
sudo yum install -y selinux-policy selinux-policy-targeted policycoreutils
```
### 4. Configure SELinux Policy
To meet the requirement of keeping SELinux disabled after the scheduled maintenance reboot, I edited the `/etc/selinux/config` file. I modified the `SELINUX=` directive from its default value to `disabled`.
```bash
sudo vi /etc/selinux/config
# Set SELINUX=disabled
```
### 5. Verification
I verified the configuration change by searching for the active `SELINUX=` line in the configuration file to ensure it was saved correctly.
```bash
grep SELINUX= /etc/selinux/config
```
