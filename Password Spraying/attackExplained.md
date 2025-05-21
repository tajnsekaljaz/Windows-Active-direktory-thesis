# Password Spraying Attack

## What Is Password Spraying?

Password spraying is a type of brute-force attack in which an attacker attempts to gain unauthorized access to many user accounts by trying a few common passwords (e.g., "Welcome123", "Password1") across multiple usernames.

Unlike traditional brute-force attacks, which try many passwords against one account (and often trigger account lockouts), password spraying spreads login attempts across multiple accounts to evade detection.

---

## How Does It Work?

1. **User Enumeration**:
   - The attacker gathers a list of valid usernames.
   - This can be done via OSINT, scraping company directories, or using naming conventions (e.g., j.doe@company.com).

2. **Password Selection**:
   - The attacker chooses 1–3 common passwords (e.g., "Winter2024", "Company@123").

3. **Login Attempts**:
   - The attacker attempts to log in using the selected passwords across all usernames.
   - These attempts are slow and spaced out to avoid triggering account lockout policies.

4. **Success & Access**:
   - If a user is using a weak or default password, the attacker gains access.
   - From there, lateral movement, privilege escalation, or data theft can occur.

---

## Why It Works

- Many organizations allow multiple failed login attempts before locking out accounts.
- Users often reuse weak, guessable passwords.
- Logging and monitoring may not detect low-and-slow brute-force behavior.

