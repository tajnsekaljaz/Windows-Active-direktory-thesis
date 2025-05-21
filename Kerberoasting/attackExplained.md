# Kerberoasting Attack

## What Is Kerberoasting?

Kerberoasting is a post-exploitation attack technique that targets **Kerberos service accounts** in Active Directory (AD). The attacker requests **service tickets (TGS)** for SPNs (Service Principal Names) and attempts to **crack them offline** to retrieve plaintext passwords.

This attack exploits the fact that Kerberos tickets are encrypted with the service account's password hash.

---

## How Does It Work?

1. **Domain Access**:
   - The attacker must have valid user credentials (even a low-privilege user).

2. **Enumerate SPNs**:
   - Use tools like `setspn.exe` or PowerShell to find accounts with registered SPNs.
   - These accounts often run services and may have high privileges.

3. **Request TGS Tickets**:
   - The attacker requests Kerberos service tickets for the SPNs.
   - These tickets are encrypted with the **NTLM hash** of the service account's password.

4. **Extract and Crack**:
   - The attacker extracts the tickets and exports them using tools like **Rubeus**, **Impacket**, or **Mimikatz**.
   - Offline password cracking tools (like **Hashcat**) are used to brute-force the password.

---

## Why It Works

- Kerberos does not limit how often TGS tickets can be requested.
- Offline cracking avoids detection and account lockouts.
- Many service accounts use weak or rarely changed passwords.

