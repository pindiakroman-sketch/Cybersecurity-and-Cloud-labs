# 🛡️ Active Directory Basics: Practical Lab & Troubleshooting Case Study

This repository serves as complete documentation and a technical overview of the tasks I completed during my hands-on training in the **Active Directory Basics** room on the **TryHackMe** platform. This documentation details real-world administrative troubleshooting, network configuration, and Group Policy management.

---

## 🎯 Lab Environment
* **Domain:** `thm.local`
* **Target Machine IP:** `10.112.160.179`
* **Attack Station:** THM AttackBox (Linux / `xfreerdp`)

---

## 🛠️ Case Studies & Troubleshooting Logs

### 1. Fixing Object Search in Active Directory Users and Computers
* **Issue:** When trying to locate and rename the user `phillip` to `roman`, the Active Directory system reported that the object could not be found.
* **Root Cause:** Syntax error. The entire string, including the User Principal Name (UPN) in parentheses, was being pasted directly into the object name field: `Roman (roman@thm.local)`.
* **Resolution:** The AD Query filter requires the clean login name only (`roman`). After entering the clean username, clicking **Check Names** successfully resolves the identity. Alternatively, the **Advanced -> Find Now** menu can be used to browse the directory structure.

### 2. Protocol Misconfigurations: RDP vs. SSH on Windows Targets
* **Issue:** Attempts to connect to the target remote server using the command `ssh 10.112.160.179` from the AttackBox terminal kept failing.
* **Root Cause:** The target Windows environment does not run an SSH service by default. Network administration and access require the graphical **RDP (Remote Desktop Protocol)**.
* **Resolution:** Established a successful remote desktop session using the Linux-based RDP client `xfreerdp` with the following parameters:
  ```bash
  xfreerdp /u:phillip /p:Claire2008 /d:THM /v:10.112.160.179 /dynamic-resolution +clipboard
  ```

### 3. Bypassing the `ERRCONNECT_PASSWORD_MUST_CHANGE` Error (0x00020013)
* **Issue:** After enforcing a mandatory password reset for the user `sophie` using the PowerShell command `Set-ADUser -ChangePasswordAtLogon $true`, subsequent direct connection attempts via RDP failed, forcing the `xfreerdp` client to close with a `Connection reset by peer` error.
* **Root Cause:** A known global protocol incompatibility (bug) between the Network Level Authentication (NLA) encryption used by `xfreerdp` and the Windows interactive blue screen that demands an immediate password change prior to desktop initialization.
* **Resolution (Administrative Bypass):** 
  1. Re-established the RDP session using the administrator account (`phillip`).
  2. Forced an immediate password reset directly from the administrative PowerShell console to unlock the account profile:
     ```powershell
     Set-ADAccountPassword sophie -Reset -NewPassword (ConvertTo-SecureString "MojeNoveHeslo123!" -AsPlainText -Force)
     ```
  3. Disabled the blocking logon-reset attribute flag:
     ```powershell
     Set-ADUser -ChangePasswordAtLogon \$false -Identity sophie
     ```
  4. Successfully authenticated and launched Sophie's desktop profile via the AttackBox terminal:
     ```bash
     xfreerdp /u:sophie /p:MojeNoveHeslo123! /d:THM /v:10.112.160.179
     ```
  * **Result:** Unlocked access to Sophie's desktop and retrieved the target domain flag: `THM{thanks_for_contacting_support}`.

### 4. Validating Group Policy Object (GPO) Distribution
* **Issue:** The newly configured GPO successfully blocked access to the *Control Panel* for the domain user `Mark`. However, the security policy enforcing an automatic 5-minute inactivity screen lock did not appear to trigger.
* **Root Cause:** The active remote desktop session (`xfreerdp`) continuously sends keep-alive network packets and input signals to maintain the connection. Windows interprets this background traffic as active user interaction, thereby resetting the local screensaver and inactivity timers.
* **Validation:** Correct GPO deployment was verified locally on Mark's profile by forcing a policy pull and checking the sync status via PowerShell:
  ```powershell
  gpupdate /force
  ```
  The console confirmed: `Computer Policy update has completed successfully. User Policy update has completed successfully.` This proved that all GPO settings were correctly applied at the domain level.

---

## 🧠 Core Active Directory Concepts Learned

### What is an OU (Organizational Unit)?
An **Organizational Unit (OU)** is a logical container within the Active Directory schema used to group users, computers, groups, and other objects. Unlike default built-in system containers (such as the default `Users` folder), **GPOs can be directly linked to OUs**. Furthermore, OUs allow administrative permissions to be safely delegated (e.g., granting a helpdesk technician rights to reset passwords exclusively within `OU=IT`).

### Network Authentication Protocols: Kerberos vs. NetNTLM

#### 🎫 Kerberos (Default & Secure)
An authentication protocol based on time-sensitive cryptographic **tickets** managed by a central authority called the **KDC (Key Distribution Center)**.
* **TGT (Ticket Granting Ticket):** The primary ticket granted to a user by the KDC after initial authentication. It acts like an unforgeable security wristband.
* **TGS (Ticket Granting Service):** When a user needs to access a domain network resource (e.g., a file share), they present their TGT wristband to the KDC. In return, the KDC issues a TGS ticket specifically for that resource. The target service decrypts the TGS to verify access. Plaintext passwords are never sent over the wire.

#### 🔐 NetNTLM (Legacy & Insecure)
A legacy authentication protocol that uses a **Challenge-Response** handshake mechanism.
* The target server sends a random number (*Challenge*) to the client. The client encrypts this challenge with their NTLM password hash and returns the calculation (*Response*). The server forwards both variables to the Domain Controller for mathematical verification.
* **Security Risk:** NetNTLM responses transit across the network broadcast domain. Attackers can capture these responses to perform offline brute-force cracking or use them in *NTLM Relay* attacks to impersonate users on other servers.

#### 🤝 Cross-Domain Access
For a user residing within Domain A to authenticate and access a restricted network resource hosted inside Domain B, network administrators must establish **`a trust relationship`** between both independent Active Directory domains.
