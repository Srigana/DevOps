# Day 07: Configuring Password-less SSH Authentication

## Task Overview
To facilitate automated administrative scripts running from the jump host, xFusionCorp Industries required the setup of password-less SSH access. The goal was to allow the `thor` user on the jump host to connect to all application servers (**stapp01**, **stapp02**, and **stapp03**) through their respective sudo users without being prompted for a password.

## Implementation

### 1. Generate SSH Key Pair
On the jump host, I generated a new RSA key pair for the `thor` user. I left the passphrase empty to ensure that the automation scripts can establish connections without manual intervention.

```bash
ssh-keygen
# Saved to: /home/thor/.ssh/id_rsa
# Passphrase: None
```

### 2. Distribute Public Key to App Servers
I used the ssh-copy-id utility to transfer the public key to each application server. This command automatically appends the key to the authorized_keys file of the target user on each server.

For App Server 1 (tony):
```bash
ssh-copy-id tony@stapp01
```
For App Server 2 (steve):
```bash
ssh-copy-id steve@stapp02
```
For App Server 3 (banner):
```bash
ssh-copy-id banner@stapp03
```
### 3. Verification of Access
After copying the keys, I verified the configuration by initiating an SSH session to each server. Successful password-less login was confirmed when the shell prompt appeared immediately without a password challenge.
```bash
# Testing App Server 1
ssh tony@stapp01

# Testing App Server 2
ssh steve@stapp02

# Testing App Server 3
ssh banner@stapp03
