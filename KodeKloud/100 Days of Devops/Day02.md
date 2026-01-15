# Day 02: Create Temporary User with Expiration Date

## Task Overview
The Nautilus project required a temporary user account for a developer named **anita** on **App Server 3**. To maintain security and automated access management, the account needed to be configured with a specific expiration date of **2024-02-17**.

## Implementation

### 1. Access the Target Server
The task required the account to be created specifically on **App Server 3** within the Stratos Datacenter. I established an SSH connection from the jump host to the application server using the authorized user.

```bash
ssh banner@stapp03
```
### 2. Create User with Expiration
I created the user account anita using the useradd command. I utilized the -e flag followed by the date in YYYY-MM-DD format to set the account expiry date. This ensures the account is automatically disabled by the system after the deadline.
```bash
sudo useradd -e 2024-02-17 anita
```
### 3. Verify Account Configuration
To confirm the expiration date was correctly applied to the system's account policy, I used the chage command with the -l flag to list the account's aging details.
```bash
sudo chage -l anita
```
## Final Result
The user anita was successfully created on App Server 3. The verification output confirmed that the Account expires field was set to Feb 17, 2024, ensuring the account will automatically lock after the developer's assignment ends.
