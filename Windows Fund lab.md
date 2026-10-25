# TryHackMe: Windows Fundamentals 2 - Lab Report

## 📌 Executive Summary
This repository contains my personal lab report and technical walkthrough for the **Windows Fundamentals 2** room on TryHackMe. The objective of this lab is to understand advanced system configuration, security mechanisms (UAC), resource monitoring, and core administrative tools embedded within the Windows Operating System.

* **Platform:** [TryHackMe](https://tryhackme.com/)
* **Room Link:** [Windows Fundamentals 2](https://tryhackme.com/room/windowsfundamentals2x0x)
* **Difficulty:** Beginner / Foundational
* **Language:** English (For professional portfolio documentation)

---

## 🛠️ Lab Tasks & Technical Breakdown

### Task 1: Introduction
* Brief overview of the Windows administrative ecosystem and setting up the lab environment.

### Task 2: System Configuration and Advanced System Settings
* **Key Tools Used:** `msconfig.exe`, System Configuration Tool.
* **Core Concepts:** Investigating startup troubleshooting, managing services, and understanding boot configurations (Normal, Diagnostic, Selective startup). Exploring Advanced System Settings to manage virtual memory and paging files.
* **My Findings:** Learning how to identify hidden background services that impact machine performance or could indicate persistence in a compromised system.

### Task 3: Change UAC Settings
* **Key Tools Used:** User Account Control Settings (`UserAccountControlSettings.exe`).
* **Core Concepts:** Configuring the 4 notification levels of User Account Control (Always notify, Notify only when apps try to make changes, Notify without dimming, Never notify).
* **Security Impact:** Understanding the "Secure Desktop" feature (dimming screen) which prevents malicious scripts from automatically interacting with administrative prompts.

### Task 4: Computer Management
* **Key Tools Used:** Computer Management console (`compmgmt.msc`).
* **Core Concepts:** Combining several snap-ins such as Task Scheduler, Event Viewer, Shared Folders, Local Users and Groups, and Disk Management into a single view.
* **My Findings:** Inspected active network shares and discovered how to track automated system tasks (e.g., GoogleUpdateTaskMachineUA).

### Task 5: System Information
* **Key Tools Used:** System Information utility (`msinfo32.exe`).
* **Core Concepts:** Gathering extensive hardware specifications, system components, software environments, and analyzing environment variables (like ComSpec path).

### Task 6: Resource Monitor
* **Key Tools Used:** Resource Monitor (`resmon.exe`).
* **Core Concepts:** Real-time tracking of CPU, Memory, Disk, and Network resources.
* **Security Context:** Crucial for detecting abnormal outbound network traffic (C2 beacons) or unauthorized heavy disk reads (Ransomware encryption activity).

### Task 7: Command Prompt
* **Key Tools Used:** `cmd.exe`
* **Core Concepts:** Utilizing native CLI commands to verify system state:
  * `whoami` - Checking current user context.
  * `hostname` - Identifying the system name.
  * `ipconfig /all` - Enumerating detailed network adapter data and DNS configuration.

### Task 8: Registry Editor
* **Key Tools Used:** Registry Editor (`regedt32.exe` / `regedit.exe`).
* **Core Concepts:** Exploring the central hierarchical database where Windows and applications store low-level configurations. Navigating through Registry Hives (HKLM, HKCU).
* **Security Context:** Analyzing common persistence mechanisms where malware modifies "Run" keys to start automatically on boot.

### Task 9: Conclusion
* Summary of the foundational knowledge gained regarding built-in Windows utilities essential for both IT Administration and Blue Team (Security Analyst) roles.

---

## 📈 Key Takeaways for Security Professionals
1. **Malware Persistence Auditing:** Mastering tools like `msconfig` and the Registry Editor allows an analyst to discover where malware hides to survive system reboots.
2. **Incident Response Readiness:** Utilities like `resmon` and `cmd` (`ipconfig`, `netstat`) provide immediate, native insight into a compromised host without needing external tools.
3. **Privilege Isolation:** Understanding UAC levels is critical for implementing the Principle of Least Privilege across enterprise endpoints.

---
*Note: Flags and direct answers have been omitted or sanitized to comply with TryHackMe's write-up guidelines and to demonstrate ethical reporting.*
