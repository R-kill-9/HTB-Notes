In Windows, privilege escalation involves exploiting vulnerabilities or misconfigurations to gain higher access, often from a standard user to administrative privileges. Several key components play a role in privilege escalation, such as **LSASS**, **SAM**, and related techniques. Below is an overview of these components and how they are involved in privilege escalation.

## LSASS (Local Security Authority Subsystem Service)

**LSASS** is a critical system process that handles authentication, user logins, and the management of security tokens. It validates user credentials during login and creates security tokens used to manage access rights.

To dump credentials from LSASS **Mimikatz** can be used:

```bash
mimikatz.exe "sekurlsa::logonpasswords"
```

## SAM (Security Accounts Manager)

**SAM** is a database file located at `C:\Windows\System32\Config` that stores user account information, including password hashes for local accounts.

To extract the SAM file (requires SYSTEM privileges):

```bash
reg save HKLM\SAM C:\path\to\sam.bak
```

## Security Tokens and Token Impersonation
When a user logs into Windows, **LSASS** creates a **security token**, which is a data structure that contains the user's privileges and access rights.

Using **Mimikatz**, you can impersonate a token:

```bash
mimikatz.exe "token::impersonate /user:Administrator"
```