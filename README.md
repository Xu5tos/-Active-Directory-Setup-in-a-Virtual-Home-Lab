# Active Directory Setup in a Virtual Home Lab

## Overview
This guide outlines a step-by-step process to set up an Active Directory (AD) environment using Windows Server 2022 within a virtualized lab environment. This hands-on lab is ideal for practicing Identity and Access Management (IAM), Domain Services configuration, Group Policy implementation, and User/Group provisioning.

---

## Prerequisites
- Windows PC with at least 8GB RAM and 100GB free disk space
- VMware Workstation Pro (free personal-use version)
- Windows Server 2022 ISO (downloaded from Microsoft Evaluation Center)

---

## Step-by-Step Instructions

### Step 1: Virtual Environment Setup
1. **Install VMware Workstation Pro**
   - Download from: https://www.vmware.com/products/workstation-pro.html
   - Follow the installation wizard instructions.

2. **Create a New Virtual Machine**
   - Launch VMware  Create a New Virtual Machine  Custom (advanced)
   - Use ISO image for Windows Server 2022
   - Assign resources (minimum: 2 CPUs, 4GB RAM, 40GB disk)

3. **Install Windows Server 2022**
   - Choose "Windows Server 2022 Standard (Desktop Experience)"
   - Set a strong administrator password

4. **Configure Initial Server Settings**
   - Set static IP address
   - Rename the computer (e.g., AD-Server)
   - Enable Remote Desktop (optional)

---

### Step 2: Install Active Directory Domain Services (AD DS)
1. **Launch Server Manager**  Manage  Add Roles and Features
2. **Select Role-based or feature-based installation**
3. **Select the server from the server pool**
4. **Add "Active Directory Domain Services"**
   - Also add Group Policy Management tools when prompted
5. **Complete the installation and reboot if necessary**

---

### Step 3: Promote Server to Domain Controller
1. After installation, open Server Manager  "AD DS"
2. Click on "Promote this server to a domain controller"
3. **Create a new forest**: Domain name `eastcharmer.local`
4. Set Directory Services Restore Mode (DSRM) password
5. Review selections and install
6. Server will reboot automatically after promotion

---

### Step 4: Configure Organizational Units (OUs)
1. Open **Active Directory Users and Computers** (ADUC)
2. Right-click the domain `eastcharmer.local`  New  Organizational Unit
3. Create top-level OUs:
   - USA
   - Europe
   - Asia
4. Under each region, create nested OUs:
   - Users
   - Computers
   - Servers

---

### Step 5: Create Security and Distribution Groups
1. In ADUC, right-click appropriate OU  New  Group
2. Group Naming Examples:
   - `IT_Department` (Security Group)
   - `DL_IT_Admins` (Distribution Group)
3. Understand group scopes:
   - Global: Cross-domain use
   - Domain Local: Within the same domain
   - Universal: Forest-wide use (requires GC and proper configuration)

---

### Step 6: Create User Accounts
1. Right-click the desired OU  New  User
2. Example user: `jdoe` in `USA > Users`
3. Set passwords and configure settings (e.g., password never expires, user must change password at next logon)
4. Add users to groups:
   - Right-click user  Add to group  `IT_Department`

---

### Step 7: Understand Manual vs Automated Provisioning
- Manual user creation is ideal for learning.
- In production environments, use PowerShell scripts or CSV import methods to automate user provisioning.

---

## Conclusion
You have now completed the setup of a basic Active Directory environment in a virtual home lab. This lab serves as a foundation for exploring more advanced topics like Group Policy Management, DNS, DHCP integration, AD Certificate Services, and PowerShell scripting for AD automation.

---

## Optional Enhancements
- Install DHCP and DNS roles for full network simulation
- Set up client VMs to join the domain
- Apply and test Group Policies (GPOs)
- Practice user login and permissions management

---


