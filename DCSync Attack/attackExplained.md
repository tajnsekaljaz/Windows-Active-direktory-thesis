# DC Sync Attack

## What Is a DC Sync Attack?

A DC Sync attack is a post-exploitation technique where an attacker impersonates a Domain Controller (DC) and requests **replication data** from another DC in an Active Directory (AD) environment.

The attacker can extract **password hashes** (including highly privileged accounts like `krbtgt` and `Administrator`) without directly accessing a Domain Controller.

---

## How Does It Work?

1. **Gain Privileged AD Access**:
   - The attacker needs replication rights in Active Directory.
   - This typically means compromising an account with:
     - `Replicating Directory Changes`
     - `Replicating Directory Changes All`
     - `Replicating Directory Changes In Filtered Set`

2. **Use Tools Like Mimikatz**:
   - The attacker uses Mimikatz with the `lsadump::dcsync` command to simulate replication behavior.
   - The tool tricks a real Domain Controller into sending password data for any user.

3. **Extract and Use Credentials**:
   - The attacker extracts NTLM hashes or Kerberos keys.
   - These can be used to:
     - **Pass-the-Hash**
     - Create **Golden Tickets**
     - Persist and escalate privileges in the domain

---

## Example Mimikatz Command

```powershell
lsadump::dcsync /domain:yourdomain.local /user:Administrator

