# Enabling WinRM

This guide will use two separate methods to enable WinRM on a computer. This computer is usually a client computer.

# Method 1: Using PowerShell

1. Open PowerShell. Make sure you run PowerShell as an administrator. If the computer is part of an Active Directory domain, and is currently logged in to a regular user's account (meaning, the account has no elevated or administrative privileges, you will be prompted to enter in an administrator's account credentials in order to run PowerShell as an administrator).
![Step 1 (Client PS)](https://github.com/johnnyh209/Enabling-WinRM/assets/33064730/bd3b371f-38d2-4618-91cd-168ba798d355)

2. Enter in the following command: `Enable-PSRemoting`.
![Step 2 (Client PS)](https://github.com/johnnyh209/Enabling-WinRM/assets/33064730/ea6d636f-20eb-48ef-8352-820827803b24)

# Method 2: Using Group Policy

1. In Server Manager on your Windows Server system, open `Group Policy Management` console located in the `Tools` dropdown menu. If it is not listed, you will have to install it using the `Add roles and features` wizard.
