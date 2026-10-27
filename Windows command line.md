# My TryHackMe Lab: Windows Command Line for Beginners

Welcome to my repository! This serves as my personal documentation and practical lab workbook from the TryHackMe "Windows Command Line" room. Here, I practiced the fundamentals of navigating the Windows terminal (CMD), network troubleshooting, and managing files and processes.

---

## 📋 Room Structure & Covered Objectives
I successfully completed all 6 tasks in this educational module:
* **Task 1: Introduction** – Launching the command line and basic navigation principles.
* **Task 2: Basic System Information** – Querying OS configurations and system properties.
* **Task 3: Network Troubleshooting** – Running network diagnostic utilities and offline service lookups.
* **Task 4: File and Disk Management** – Working with folders, files, and disk integrity checkers.
* **Task 5: Task and Process Management** – Monitoring, filtering, and terminating active programs.
* **Task 6: Conclusion** – Final review and transitioning to the PowerShell ecosystem.

---

## 🛠️ Hands-on Scenarios & Practice

### 1. Network Diagnostics & Fixing SSH Connections
When connecting to the target machine, I originally mistyped the destination IP address. I quickly learned how to abort a frozen command using standard control interrupts.

* **Failed Attempt:** `ssh user@10.114.138.191` *(Connection frozen, used **Ctrl + C** to break)*
* **Successful Attempt:**
  ```bash
  ssh user@10.114.148.191
  ```
  *(Then accepted the fingerprint by typing `yes` and supplied the password `Tryhackme123!`)*

Other essential networking utilities tested in the lab:
```cmd
ipconfig /all      :: Displays IP configurations and Network Interface Card details
ping 10.10.0.1      :: Tests basic connectivity to the default gateway/router
tracert 10.10.0.1   :: Traces the hop-by-hop route packets take to the destination
```

### 🔍 2. Offline Service Enumeration (No Internet Lookup)
I learned that Windows maintains a local built-in database of standard ports and services. In isolated or air-gapped environments, you can map active ports to their service names by piping file contents into string search tools:

* **Checking Port 135 (RPC):** `type C:\Windows\System32\drivers\etc\services | findstr 135` 
  * *Resulting Output:* **`epmap`**
* **Checking Port 3389 (RDP):** `type C:\Windows\System32\drivers\etc\services | findstr 3389`
  * *Resulting Output:* **`ms-wbt-server`**
* **Checking Port 445 (SMB):** `type C:\Windows\System32\drivers\etc\services | findstr 445`
  * *Resulting Output:* **`microsoft-ds`**

### 📁 3. File System Manipulation & Volume Health Check
I practiced moving through different directories and running file system stability checks.

```cmd
cd C:\                       :: Change directory to the root of the C: drive
dir /a /s                    :: Recursively lists all files, including hidden system files
mkdir MyNewFolder            :: Creates a brand new workspace directory
type flag.txt                :: Prints the raw text contents of a file directly to the screen
chkdsk                       :: Verifies logical integrity of the hard drive volume
sfc /scannow                 :: Scans and repairs corrupted core Windows system files
```

### 🛑 4. Process Instrumentation & Power Automation
I learned how to identify stuck or unresponsive tasks, force-close them via CLI, and safely test system timer schedules.

```cmd
tasklist                     :: Displays all currently executing programs and their PIDs
taskkill /PID 1516           :: Forcefully terminates a program (e.g., Notepad) using its Process ID

shutdown /r /t 600           :: Schedules a system restart in 10 minutes (600 seconds)
shutdown /a                  :: EMERGENCY ABORT: Cancels any pending shutdown or restart timer
```

---

## 📊 Command Reference Cheat Sheet

| Command | Simple Explanation | Example Usage |
| :--- | :--- | :--- |
| `systeminfo` | Queries basic system parameters and OS build details. | `systeminfo` |
| `ipconfig` | Lists active local network adapters and assigned IP addresses. | `ipconfig /all` |
| `type` | Opens and reads text files directly within the terminal console. | `type flag.txt` |
| `findstr` | Filters specific text patterns or numbers from command outputs. | `type file.txt \| findstr 135` |
| `tasklist` | Works like a CLI Task Manager, displaying running processes. | `tasklist` |
| `taskkill` | Forces a running program or thread to shut down completely. | `taskkill /PID 1234` |
| `shutdown` | Automates system reboots or power downs using custom countdown timers. | `shutdown /r /t 600` |
| `shutdown /a` | Instantly revokes an active system shutdown countdown. | `shutdown /a` |
| `/?` | Built-in manual flag. Append it to any command to see the help menu. | `shutdown /?` |

---
*Documented by an entry-level Cyber Security / IT Systems Explorer via TryHackMe.*

