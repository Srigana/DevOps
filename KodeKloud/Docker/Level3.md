# Level 03: Remove Stale Docker Container

## Task Overview
A developer from the Nautilus project had previously deployed a testing container named **kke-container** on **App Server 2**. Since the testing phase was completed, the security team requested the permanent removal of this container to free up system resources and maintain environment hygiene.

## Implementation

### 1. Access the Target Server
The container was located on **App Server 2** (`stapp02`) in the Stratos Datacenter. I accessed the server via SSH from the jump host using the `steve` user account.

```bash
ssh steve@stapp02
```
### 2. Identify the Target Container
I used the `docker ps` command to list all active containers. This allowed me to confirm that `kke-container` was running and to retrieve its specific Container ID.
```bash
docker ps
```
### 3. Stop and Remove the Container
To safely remove a running container, it must first be stopped to allow processes to terminate gracefully. Once stopped, I executed the removal command.
```bash
# Stop the running container
docker stop 153a165f2bce

# Permanently remove the container
docker rm 153a165f2bce
```
### 4. Verification
I performed a final check of the container list to ensure that `kke-container` was no longer present on the system.
```bash
docker ps
```
