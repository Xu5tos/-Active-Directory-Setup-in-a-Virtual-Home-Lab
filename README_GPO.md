# Implementing Group Policy Objects (GPOs) in a Windows Server Home Lab

## Overview
This document outlines the implementation of several key Group Policy Objects (GPOs) in a Windows Server 2022 home lab environment. These GPOs enhance security, usability, and standardization across domain-connected client machines.

---

## Prerequisites
- Windows Server 2022 with Active Directory Domain Services (AD DS) and Group Policy Management Console (GPMC) installed
- At least one domain-joined Windows client

---

## GPOs Created & Configured

### 1. Password Policy GPO
**Purpose**: Enforce strong password practices
- **Settings Applied**:
  - Minimum password length: 12 characters
  - Password must meet complexity requirements
  - Maximum password age: 60 days
  - Minimum password age: 1 day
  - Enforce password history: 5 previous passwords
- **Scope**: Linked to the domain root

### 2. Drive Mapping GPO
**Purpose**: Automatically map network drive on user login
- **Configuration**:
  - User Configuration  Preferences  Windows Settings  Drive Maps
  - New Mapped Drive: \\SERVER\Shared
  - Drive Letter: Z:
  - Action: Update
- **Scope**: Applied to specific OU (e.g., USA > Users)

### 3. Desktop Wallpaper GPO
**Purpose**: Standardize desktop appearance across user accounts
- **Configuration**:
  - User Configuration  Policies  Administrative Templates  Desktop  Desktop
  - Enable Desktop Wallpaper setting
  - Wallpaper path: \\SERVER\wallpapers\company.jpg
  - Wallpaper Style: Fill
- **Scope**: Applied to user-based OUs

### 4. Restrict Control Panel GPO
**Purpose**: Limit user access to sensitive system settings
- **Configuration**:
  - User Configuration  Policies  Administrative Templates  Control Panel
  - Enable: Prohibit access to Control Panel and PC settings
- **Scope**: Applied to general user OU

### 5. Disable USB Storage GPO
**Purpose**: Block access to USB storage devices
- **Configuration**:
  - Computer Configuration  Policies  Administrative Templates  System  Removable Storage Access
  - All Removable Storage classes: Deny all access
- **Scope**: Applied to all domain computers

---

## Bonus Activity: Account Lockout Policy
**Objective**: Prevent brute-force attacks via account lockout
- **Configuration Path**:
  - Computer Configuration  Policies  Windows Settings  Security Settings  Account Policies  Account Lockout Policy
- **Settings Applied**:
  - Account lockout threshold: 5 invalid attempts
  - Account lockout duration: 15 minutes
  - Reset account lockout counter: 15 minutes
- **Status**: Created, linked to domain root, tested using dummy accounts

---

## Implementation Tips
- Use Group Policy Modeling to preview GPO impacts
- Apply GPOs to specific OUs for better management granularity
- Regularly update documentation with GPO changes

---

## Suggested Repository Structure
/GPO_Implementation_Home_Lab

 screenshots
    gpo-settings-example.png
 README.md
 docs
     GPO_Configuration_Guide.pdf
