# Enabling WinRM

This guide will use two separate methods to enable WinRM on a computer. This computer is usually a client computer.

# Method 1: Using PowerShell

1. Open PowerShell. Make sure you run PowerShell as an administrator. If the computer is part of an Active Directory domain, and is currently logged in to a regular user's account (meaning, the account has no elevated or administrative privileges, you will be prompted to enter in an administrator's account credentials in order to run PowerShell as an administrator).
![Step 1 (Client PS)](https://github.com/johnnyh209/Enabling-WinRM/assets/33064730/bd3b371f-38d2-4618-91cd-168ba798d355)

2. Enter in the following command: `Enable-PSRemoting`.
![Step 2 (Client PS)](https://github.com/johnnyh209/Enabling-WinRM/assets/33064730/ea6d636f-20eb-48ef-8352-820827803b24)

The `Enable-PSRemoting` commandlet will register PowerShell as an endpoint, and enable WInRM and have it be started automatically, and setup a firewall exception remoting traffic. 

# Method 2: Using Group Policy

1. In Server Manager on your Windows Server system, open `Group Policy Management` console located in the `Tools` dropdown menu. If it is not listed, you will have to install it using the `Add roles and features` wizard. Then, navigate the directory tree on the left hand side `(Forest: [your domain] > Domains > [your domain] > right-click on the group you want to assign the group policy to) > Create a GPU in this domain and link it here`.
![Step 1 (Group Policy) ](https://github.com/johnnyh209/Enabling-WinRM/assets/33064730/7b33c604-3e33-42ee-931c-86f48a75e56f)

2. A new window named `New GPO` should open up. In the `Name:` field, enter in a name for this group policy. I have chosen to use `WinRM` for simplicity. Click `OK` afterwards.
![Step 2 (Group Policy)](https://github.com/johnnyh209/Enabling-WinRM/assets/33064730/657ec5a7-3fce-4019-83eb-0cd84dd308ed)

You should see the GPO that you just created listed in the group you assigned the GPO to. Right-click the GPO listed and click on `Edit` to open the `Group Policy Management Editor`.

3. Follow the following navigation path: `Computer Configuration > Administrative Templates > Windows Components`. Inside of `Windows Components`, find `Windows Remote Management`. Open `Windows Remote Management` to find two items listed: WinRM Client and WinRM Service. Open up WinRM Service.
![Step 7 WinRM Service (Group Policy)](https://github.com/johnnyh209/Enabling-WinRM/assets/33064730/c75f06b9-644b-4e70-a158-78ce15816b99)

4. Double-click `Allow remote server management through WinRM` to open up a new window where you will enable WinRM. Click `OK` when finished to finalize the enabling of WinRM.
![Step 8 Double Click (Group Policy)](https://github.com/johnnyh209/Enabling-WinRM/assets/33064730/b28ae992-07b7-4080-9f70-7c27111d69f3)
![Step 9 Select Enabled (Group Policy)](https://github.com/johnnyh209/Enabling-WinRM/assets/33064730/cc05ba25-644f-4e52-b8e5-5f55f1e3cf60)

## Enabling WinRM in Group Policy to Automatically Start

1. Open `Group Policy Management` and navigate to the group of which the WinRM group policy has been assigned to. Right-click on your WinRM group policy and click `Edit`.
![Pc38VXDpEx](https://github.com/johnnyh209/Enabling-WinRM/assets/33064730/47aae4fa-0a59-409b-b720-abd04c56f780)

2. Follow the following navigation path: `Computer Configuration > Preferences > Control Panel Settings`.
![2  Control Panel Settings](https://github.com/johnnyh209/Enabling-WinRM/assets/33064730/acb7d51a-9478-4ab0-8fc7-1470c823e97a)

3. In `Control Panel Settings`, right-click on `Services`, select `New`, and then select `Service`. This opens the `New Service Properties` window.
![3](https://github.com/johnnyh209/Enabling-WinRM/assets/33064730/9021aefd-d897-4ade-9f22-a4c627fd4230)

4. In the `New Service Properties` window:
* Change `Startup` to **Automatic**,
* Assign a name
* Change `Service Action` to **Start service**
* Click `OK`
![4](https://github.com/johnnyh209/Enabling-WinRM/assets/33064730/695bf9dc-d51b-44e3-af58-e9c096273a0d)

## Enabling Windows Remote Shell

1.Open `Group Policy Management` and navigate to the group of which the WinRM group policy has been assigned to. Right-click on your WinRM group policy and click `Edit`.

2. In `Group Policy Management Editor` for the GPO, follow the navigation path: `Computer Configuration > Policies > Administrative Templates > Windows Components`. Look for `Windows Remote Shell` from the list of Windows Components and double-click.
![4  Windows Remote Shell (Double Click)](https://github.com/johnnyh209/Enabling-WinRM/assets/33064730/674537d3-00dc-4a11-bf17-f1ac1bc4cda1)

3. Click on the circle next to `Enabled` then click `OK` to enable Windows Remote Shell.
![6  Enabled](https://github.com/johnnyh209/Enabling-WinRM/assets/33064730/1d9141af-16fe-44d8-9f04-db32badbe339)

## Adding a Firewall Exception for Remote Management

1. In the `Group Policy Management Editor` for the GPO, follow this navigation (it is best to navigate on the left panel that contains the navigation tree): `Computer Configuration > Policies > Windows Settings > Security Settings > Windows Defender Firewall with Advanced Security`.
![3  navigate tree](https://github.com/johnnyh209/Enabling-WinRM/assets/33064730/a314ce0e-f022-4a36-83e3-a2a5bcf04658)

2. Right-Click `Inbound Rules` and click on `New Rule` to open the `New Inbound Rule Wizard`.
![4  Right click inbound rules, new rule](https://github.com/johnnyh209/Enabling-WinRM/assets/33064730/34d538be-8f8d-4357-b56b-d5219c0e1fb4)

3. In the `New Inbound Rule Wizard`, select **Predefined**. In the drop-down menu under **Predefined**, select `Windows Remote Management`. Then click `Next`.
![5](https://github.com/johnnyh209/Enabling-WinRM/assets/33064730/303eeba5-9e3d-4b00-9bbf-40fa4e8c938b)

4. Click `Next` on the `Predefined Rules` page.
![6  click next](https://github.com/johnnyh209/Enabling-WinRM/assets/33064730/d167ba73-bb2e-4be2-8478-faa0641ccf51)

5. Select `Allow the connection` and click finished.
![7  Allow the connection](https://github.com/johnnyh209/Enabling-WinRM/assets/33064730/11f7c25e-2c26-4f85-bd25-f84730829955)

## GPUdate

1. To ensure that the group policy has been applied to the systems, use the command line or PowerShell on each system that the group policy has been applied to and run the command `gpupdate /force`.
 ![8](https://github.com/johnnyh209/Enabling-WinRM/assets/33064730/2418fcf3-112c-4d41-8177-a75dda949de6)
