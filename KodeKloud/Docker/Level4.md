# Level 4: Copying Files Between Docker Host and Container

## Task Overview
The objective was to transfer an encrypted file, `nautilus.txt.gpg`, from the local filesystem of **App Server 2** to a specific directory within a running Docker container named `ubuntu_latest`. A critical requirement was ensuring data integrity verifying that the file remained unchanged during the transfer.

## Implementation

### 1. Access the Target Server
I logged into **App Server 2** (`stapp02`) via SSH from the jump host to access the Docker environment where the container was running.
```bash
ssh steve@stapp02
```
### 2. Identify the Target Container
I used the `docker ps` command to confirm the container `ubuntu_latest` was active and to retrieve its Container ID for the copy operation.
```bash
docker ps
```
### 3. Copy the Encrypted File
I utilized the `docker cp` command to move the file from the host's `/tmp/` directory to the `/home/` directory inside the container. This command facilitates bidirectional file transfer between the host and containers.
```bash
docker cp /tmp/nautilus.txt.gpg ubuntu_latest:/home/nautilus.txt.gpg
```
### 4. Verify File Integrity
To ensure the file was not modified during the copy, I compared the SHA256 checksum of the file on the host against the checksum of the file now residing inside the container. Matching hashes confirm a perfect transfer.
```bash
# Check hash on the host
sha256sum /tmp/nautilus.txt.gpg

# Check hash inside the container
docker exec ubuntu_latest sha256sum /home/nautilus.txt.gpg
