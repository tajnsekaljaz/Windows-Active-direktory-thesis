# Windows-Active-direktory-thesis

#install active directory
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass

Install-windowsfeature AD-domain-services

Import-Module ADDSDeployment

#set up domain
Install-ADDSForest -CreateDnsDelegation:$false -DatabasePath "C:\\Windows\\NTDS" -DomainMode "7" -DomainName "skypia.org" -DomainNetbiosName "skypia" -ForestMode "7" -InstallDns:$true -LogPath "C:\\Windows\\NTDS" -NoRebootOnCompletion:$false -SysvolPath "C:\\Windows\\SYSVOL" -Force:$true

#pull file from git change last line to the same as the DomainName
Invoke-WebRequest -Uri https://raw.githubusercontent.com/WaterExecution/vulnerable-AD-plus/master/vulnadplus.ps1 -OutFile 'vulnadplus.ps1'

# set up and run skript
Import-Module vulnadplus.ps1

Invoke-WebRequest -Uri "https://raw.githubusercontent.com/wazehell/vulnerable-AD/master/vulnad.ps1"



Invoke-VulnAD -UsersLimit 200 -DomainName "skypia.org"
kali
sudo nano /etc/network/interfaces

#dodaj v mapo 

# Static IP for eth0
auto eth0
iface eth0 inet static
    address 192.168.56.108
    netmask 255.255.255.0
    gateway 192.168.56.1


#restart
sudo systemctl restart networking






