# TryHackMe: Linux Fundamentals Part 3 - Lab Documentation

## 📌 Project Overview
This repository contains the official documentation for my hands-on laboratory work completed during the **Linux Fundamentals Part 3** room on TryHackMe. This advanced foundational lab focuses on critical Linux administration skills, package management, process monitoring, automation, and defensive log analysis (Blue Teaming). 

By documenting these tasks, I demonstrate a strong command of the Linux CLI, system persistence, and networking utilities essential for a role in **Cloud Security** and **Security Operations Center (SOC) environments**.

---

## 🛠️ Technologies & Tools Used
* **Operating System:** Linux (Ubuntu/Debian-based distributions), Bash CLI
* **Network & Utilities:** Python3 HTTP Server, Wget, Curl, SSH (Secure Shell)
* **Text Editors:** Nano, Vim
* **Process & Automation:** Systemd (`systemctl`), `ps`, `kill`, Crontab, `apt` package manager
* **Log Analysis:** Text processing tools (`grep`, `cat`, `awk`), `/var/log` directory

---

## 🚀 Step-by-Step Task Breakdown

### Task 1: Introduction
* **Objective:** Understand the scope of the room, focusing on advanced utilities, process management, automation, and reviewing system logs to maintain machine health and security.

### Task 2: Deploy Your Linux Machine
* **Objective:** Establish a secure remote connection to the target enterprise Linux instance.
* **Action:** Initialized the TryHackMe AttackBox and connected via **SSH** to the deployed instance:
  ```bash
  ssh tryhackme@10.113.158.123
  ```

### Task 3: Terminal Text Editors
* **Objective:** Master command-line text editors for modifying configuration files without a Graphical User Interface (GUI).
* **Action:** Practiced creating and editing configuration scripts using terminal-based editors like **Nano** and **Vim**, learning vital keyboard shortcuts to save, exit, and navigate text files under pressure.

### Task 4: General/Useful Utilities
* **Objective:** Learn how to serve files over a network and download content dynamically.
* **Action:** Created a dedicated environment and spawned a lightweight Python web server on port `8000` to simulate file hosting:
  ```bash
  mkdir webserver && cd webserver
  python3 -m http.server 8000
  ```
* Used `wget` and `curl` from a secondary terminal instance to fetch hidden configuration layers (`.flag.txt`) securely across the internal network.

### Task 5: Processes 101
* **Objective:** Understand how Linux manages applications via processes and how to identify suspicious background behavior.
* **Action:** Used process monitoring utilities to list, track, and filter running programs:
  ```bash
  ps aux | grep THM
  ```
* Practiced service termination and signal management using the `kill` command to stop non-responsive or unauthorized background binaries.

### Task 6: Maintaining Your System: Automation
* **Objective:** Automate repetitive administration tasks and maintain system persistence.
* **Action:** Explored the **Cron** daemon (`crontab -e`) to schedule automated backups and health-checks at specific intervals. 
* Configured system services to boot automatically upon OS startup using the system initialization manager:
  ```bash
  systemctl enable myservice
  ```

### Task 7: Maintaining Your System: Package Management
* **Objective:** Learn how to securely install, update, and remove software repositories within Debian/Ubuntu systems.
* **Action:** Utilized the Advanced Package Tool (**APT**) to manage system binaries safely, adding trusted GPG keys and updating software repositories securely via the CLI.

### Task 8: Maintaining Your System: Logs
* **Objective:** Perform forensic log analysis to trace user activity and investigate an active security incident.
* **Action:** Navigated to the core Linux logging directory `/var/log` and audited the Apache web server infrastructure logs (`/var/log/apache2/access.log`).
* **Findings:** Successfully traced an external visitor signature, uncovering the exact malicious IP address (**`10.10.212.98`**) and identifying the precise file exfiltrated from the platform (**`cats.jpg`**).

---

## 📈 Current Progress & Metrics
* **TryHackMe Global Rank:** Currently positioned within the **TOP 5% - 8%** globally among millions of users.
* **Next Career Milestone:** Blending this practical Linux core with enterprise cloud engineering by studying for the **Microsoft Azure Administrator (AZ-104)** certification.
