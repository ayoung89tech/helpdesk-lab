# Help Desk Lab Documentation – AWS EC2 + Active Directory

## Overview
This lab demonstrates how to deploy a Windows Server environment in AWS, connect via RDP, install and configure Active Directory Domain Services (AD DS), and perform essential help desk administrative tasks such as creating users, groups, and resetting passwords.

## Environment Setup

### 1. Created an AWS Virtual Machine (EC2 Instance)
- Logged into the AWS Management Console.
- Navigated to EC2 and launched a new instance.
- Selected a Windows Server AMI (Amazon Machine Image).
- Chose an instance type (e.g., t2.micro or t3.medium).
- Configured network settings (default VPC and security group with RDP port 3389 allowed).

### 2. Generated Key Pair
- Created a .pem key pair for authentication.
- Downloaded the key pair securely for decrypting the Windows Administrator password.

### 3. Retrieved Administrator Credentials
- Waited for instance initialization.
- Used the PEM key pair to decrypt the Windows password from the EC2 console.

### 4. Connected via RDP
- Copied the instance’s public IPv4 address.
- Opened Remote Desktop Connection locally.
- Entered the IP and Administrator credentials.
- Successfully connected to the Windows Server EC2 instance.

## Active Directory Installation & Configuration

### 5. Installed Active Directory Domain Services (AD DS)
Inside the EC2 Windows Server:
- Opened Server Manager.
- Selected Add Roles and Features.
- Installed Active Directory Domain Services.
- Promoted the server to a Domain Controller.
- Created a new forest/domain: `labdomain.local`

### 6. Verified AD Installation
- Opened Active Directory Users and Computers (ADUC).
- Confirmed the domain and default organizational units (OUs).
- Ensured DNS services installed correctly.

## User & Group Management Tasks

### 7. Created New Users in Active Directory
Using ADUC:
- Right-clicked the appropriate OU → New → User.
- Created test accounts (e.g., John Doe, Sarah Smith).
- Assigned temporary passwords.
- Enabled “Password must be changed at next logon.”

### 8. Created a Security Group
- Navigated to an OU → New → Group.
- Created `HelpDesk_Team` as a Global Security Group.

### 9. Reset Passwords for a User
- Located a user inside ADUC.
- Right-clicked → Reset Password.
- Entered a new password following complexity requirements.
- Verified account status and unlocked if needed.

## Commands Used (Optional)
```powershell
# Check domain info
Get-ADDomain

# Create a user
New-ADUser -Name "Test User" -SamAccountName test.user -UserPrincipalName test.user@labdomain.local

# Reset a password
Set-ADAccountPassword test.user -Reset -NewPassword (ConvertTo-SecureString "NewPassword123!" -AsPlainText -Force)
```

## Verification & Testing
- Confirmed new user accounts appeared in ADUC.
- Verified group creation and membership.
- Successfully reset passwords.
- Validated domain functionality using created accounts.

## Summary / What I Learned
- Deploy and connect to a Windows Server EC2 instance.
- Install and configure Active Directory Domain Services.
- Manage users and groups within ADUC.
- Perform common help desk tasks like password resets.
- Gained hands-on experience with AWS, Windows Server, and AD.
