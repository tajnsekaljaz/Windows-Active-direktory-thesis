# Hardening your SMB Configuration

## Initial State
When running the command:
```bash
smbclient -L 192.168.56.107 -U ""
```
We received a full list of user groups and shares.  
This happened because **SMBv1** is outdated and insecure, making it easy to enumerate shares.

## Disable SMBv1
Disabling SMBv1 prevents older clients and tools from connecting using vulnerable methods.

Run the following PowerShell commands:
```powershell
Disable-WindowsOptionalFeature -Online -FeatureName SMB1Protocol -Remove
Set-SmbServerConfiguration -EnableSMB2Protocol $true
```

## Enable SMB Signing
SMB signing helps prevent tampering and man-in-the-middle attacks.

Enable it using:
```powershell
Set-SmbServerConfiguration -RequireSecuritySignature $true
Set-SmbServerConfiguration -EnableSecuritySignature $true
```

## Disable Anonymous Access to File Shares
Navigate to:
`Security Settings > Local Policies > Security Options`

Modify the following:

- **Network access: Restrict anonymous access to Named Pipes and Shares**  
  From: Disabled → **Enabled**

- **Network access: Shares that can be accessed anonymously**  
  From: `C:\Common` → **Empty**

- **Network access: Named Pipes that can be accessed anonymously**  
  From: `netlogon, samr, Isarpc` → **Empty**

- **Accounts: Guest account status**  
  From: Enabled → **Disabled**

- **Network access: Let everyone permissions apply to anonymous users**  
  → **Disabled**

- **Network access: Do not allow anonymous enumeration of SAM accounts and shares**  
  → **Disabled**

---

## Results

### Before:
```bash
smbclient -L 192.168.56.107 -U ""
Password for [WORKGROUP\]:

        Sharename       Type      Comment
        ---------       ----      -------
        ADMIN$          Disk      Remote Admin
        C$              Disk      Default share
        Common          Disk      
        IPC$            IPC       Remote IPC
        NETLOGON        Disk      Logon server share 
        SYSVOL          Disk      Logon server share 
Reconnecting with SMB1 for workgroup listing.
do_connect: Connection to 192.168.56.107 failed (Error NT_STATUS_RESOURCE_NAME_NOT_FOUND)
Unable to connect with SMB1 -- no workgroup available
```

### After:
```bash
smbclient -L 192.168.56.107 -U ""
Password for [WORKGROUP\]:
session setup failed: NT_STATUS_LOGON_FAILURE
```
---

Security has been significantly improved by disabling outdated protocols and blocking anonymous access.
