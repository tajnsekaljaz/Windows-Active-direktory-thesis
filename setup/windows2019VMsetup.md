# Windows Server 2019 Setup Guide

## 1) Download Windows Server 2019 ISO
Download the Windows Server 2019 ISO from the official Microsoft website:
[Download Windows Server 2019](https://www.microsoft.com/en-us/evalcenter/download-windows-server-2019)

## 2) Setup Server in VirtualBox
### Configure Network Adapters:
- **Adapter 1: NAT**
  - The NAT adapter allows a virtual machine to access external networks by sharing the host system's network connection.
- **Adapter 2: Host-Only**
  - The Host-Only adapter creates a network that is only accessible between the virtual machine and the host system.

## 3) Setup Active Directory in PowerShell
Run PowerShell as Administrator and execute the following commands:
```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass

Install-WindowsFeature AD-Domain-Services

Import-Module ADDSDeployment
```

## 4) Set Up the Domain
Make sure to use the same domain name `skypia.org`:
```powershell
Install-ADDSForest -CreateDnsDelegation:$false -DatabasePath "C:\Windows\NTDS" -DomainMode "7" -DomainName "skypia.org" -DomainNetbiosName "skypia" -ForestMode "7" -InstallDns:$true -LogPath "C:\Windows\NTDS" -NoRebootOnCompletion:$false -SysvolPath "C:\Windows\SYSVOL" -Force:$true
```

## 5) Download the Script to Make Active Directory Vulnerable
Run the following command to pull the script:
```powershell
Invoke-WebRequest -Uri https://raw.githubusercontent.com/WaterExecution/vulnerable-AD-plus/master/vulnadplus.ps1 -OutFile 'vulnadplus.ps1'
```

## 6) Run the Script
Execute the script to make Active Directory vulnerable:
```powershell
Import-Module vulnadplus.ps1

Invoke-VulnAD -UsersLimit 200 -DomainName "skypia.org"
```

## 7) Install Recommended Tools in Server Manager
1. Open **Server Manager**
2. Navigate to **Manage → Add Roles and Features**
3. Under **Server Selection**, select **File and Storage Services**
4. Under **Features**, select:
   - **Remote Server Administration Tools**
   - **Role Administration Tools**
   - **AD DS and AD LDS Tools**
5. Click **Install**

