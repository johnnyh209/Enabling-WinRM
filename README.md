# Enabling WinRM

This guide will use two separate methods to enable WinRM on a computer. This computer is usually a client computer.

# Method 1: Using PowerShell

1. Open PowerShell. Make sure you run PowerShell as an administrator. If the computer is part of an Active Directory domain, and is currently logged in to a regular user's account (meaning, the account has no elevated or administrative privileges, you will be prompted to enter in an administrator's account credentials in order to run PowerShell as an administrator).
![Step 1 (Client PS)](https://github.com/johnnyh209/Enabling-WinRM/assets/33064730/bd3b371f-38d2-4618-91cd-168ba798d355)

2. Enter in the following command: `Enable-PSRemoting`.
![Step 2 (Client PS)](https://github.com/johnnyh209/Enabling-WinRM/assets/33064730/ea6d636f-20eb-48ef-8352-820827803b24)

# Method 2: Using Group Policy

1. In Server Manager on your Windows Server system, open `Group Policy Management` console located in the `Tools` dropdown menu. If it is not listed, you will have to install it using the `Add roles and features` wizard. Then, navigate the directory tree on the left hand side `(Forest: [your domain] > Domains > [your domain] > right-click on the group you want to assign the group policy to) > Create a GPU in this domain and link it here`.
![Step 1 (Group Policy) ](https://github.com/johnnyh209/Enabling-WinRM/assets/33064730/7b33c604-3e33-42ee-931c-86f48a75e56f)

2. A new window named `New GPO` should open up. In the `Name:` field, enter in a name for this group policy. I have chosen to use `WinRM` for simplicity. Click `OK` afterwards.
![Step 2 (Group Policy)](https://github.com/johnnyh209/Enabling-WinRM/assets/33064730/657ec5a7-3fce-4019-83eb-0cd84dd308ed)

You should see the GPO that you just created listed in the group you assigned the GPO to. Right-click the GPO listed and click on `Edit` to open the `Group Policy Management Editor`.

3. Follow the following navigation path: `Computer Configuration > Administrative Templates > Windows Components`. Inside of `Windows Components`, find `Windows Remote Management`. Open `Windows Remote Management` to find two items listed: WinRM Client and WinRM Service. Open up WinRM Service.
![Step 7 WinRM Service (Group Policy)](https://github.com/johnnyh209/Enabling-WinRM/assets/33064730/c75f06b9-644b-4e70-a158-78ce15816b99)

4. Double-click `Allow remote server management through WinRM` and 
