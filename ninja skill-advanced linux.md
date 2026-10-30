# TryHackMe: Ninja Skills – Advanced Linux Forensics & Data Retrieval Labs

## 📌 Executive Summary & Repository Overview
This repository functions as my professional digital engineering notebook covering the **Ninja Skills** environment on TryHackMe. 

As an aspiring Cloud Security and SOC Analyst, my objective during this lab was to move beyond textbook theoretical knowledge and tackle a realistic file system enumeration problem. The lab presents a scenario where 12 distinct artifacts are obfuscated across the Linux directory hierarchy. 

Rather than manually brute-forcing my way through thousands of OS paths, I constructed automated **data processing pipelines** using Linux utilities and I/O redirection. This notebook documents the architectural logic behind these pipelines, the specific forensic techniques applied, and how these concepts translate directly into enterprise enterprise defense, incident response, and Cloud Security governance.

---

## 🏗️ Architectural Core: Pipeline Pipelines via Linux Pipes (`|`)

The foundational paradigm of advanced Linux systems engineering is the **UNIX Philosophy**: *Write programs that do one thing well, and chain them together using standard interfaces.*

In this lab, I relied heavily on the pipeline redirection character (**`|`**). The pipe operator intercepts the `STDOUT` (Standard Output) of a preceding process and injects it directly into the `STDIN` (Standard Input) of the succeeding process. 

### The Master Automated Forensics Pipeline:
```bash
find / -type f 2>/dev/null | grep -E "/(8V2L|bny0|c4ZX|D8B3|FHI1|oiMO|PFbD|rmfX|SRSq|uqyw|v2Vb|X1Uy)\$" | xargs <ANALYTICAL_COMMAND>
```

### Deep Dive Component Analysis:
1. **`find /`**: Initiates a global filesystem traversal starting at the root directory (`/`). 
2. **`-type f`**: A conditional filter that constrains the kernel search space exclusively to regular files (e.g., data arrays, logs, configuration binaries), pruning directories, sockets, symbolic links, and block devices.
3. **`2>/dev/null`**: **Crucial Junior Triaging Technique.** In Linux, File Descriptor 1 is `STDOUT` and File Descriptor 2 is `STDERR`. Running a global search as an unprivileged user triggers thousands of "Permission Denied" errors. By using `2>`, I redirected the `STDERR` stream away from my terminal monitor and dumped it into `/dev/null` (the OS bit-bucket device), ensuring a completely sterile data stream for the next stage.
4. **`| grep -E`**: Invokes the Global Regular Expression Print engine with Extended Regex capabilities (`-E`).
5. **`"/(...)\$"`**: This regular expression pattern uses the logical **OR** operator (`|`) enclosed in grouping parentheses to isolate our specific target filenames. The `\$` anchor binds the pattern match strictly to the end of the string line, eliminating false positives from parent directories that might share sub-string names.
6. **`xargs`**: The extended argument execution utility. Standard utilities like `ls`, `sha1sum`, or `wc` cannot natively process raw newline-separated lists from `STDIN`. `xargs` flattens the incoming data stream and passes it dynamically as discrete command-line arguments to the terminal program.

---

## 🔍 Forensic Investigation Modules & Practical Deep Dive

### Module 1: Privilege & Identity Attribution (Group Ownership)
* **Objective:** Identify which hidden artifacts are owned by a specific non-standard OS group (e.g., `best-group`).
* **Command:**
  ```bash
  find / -type f 2>/dev/null | grep -E "/(8V2L|bny0|c4ZX|D8B3|FHI1|oiMO|PFbD|rmfX|SRSq|uqyw|v2Vb|X1Uy)\$" | xargs ls -l 2>/dev/null
  ```
* **Forensic Output Analysis:**
  ```text
  -rw-rw-r-- 1 root       best-group 13545 Oct 23  2019 /home/v2Vb
  -rw-rw-r-- 1 new-user   best-group 13545 Oct 23  2019 /mnt/D8B3
  ```
* **SOC / Enterprise Context:** 
  In a real Identity & Access Management (IAM) audit or an incident response scenario, checking group ownership is essential. Group-based access control allows malicious actors who compromise a single service account to instantly inherit broader system privileges if they belong to a high-access group. Knowing how to map files back to group constructs lets an analyst evaluate the blast radius of an account compromise.

---

### Module 2: Log Triage & Pattern Matching (Extracting IPv4 Artifacts)
* **Objective:** Scan the payload of all 12 hidden text objects to locate embedded networking configurations (IPv4 addresses) without opening individual files manually.
* **Command:**
  ```bash
  find / -type f 2>/dev/null | grep -E "/(8V2L|bny0|c4ZX|D8B3|FHI1|oiMO|PFbD|rmfX|SRSq|uqyw|v2Vb|X1Uy)\$" | xargs grep -oE "[0-9]+\.[0-9]+\.[0-9]+\.[0-9]+" 2>/dev/null
  ```
* **Technical Parameter Breakdown:**
  * **`-o`**: Instructs `grep` to output *only* the exact matching string fragment, rather than printing out massive blocks of surrounding text or raw Base64 data arrays.
  * **`[0-9]+\.`**: Match one or more numbers between 0 and 9, immediately followed by a literal dot character (escaped via a backslash `\.`). This pattern repeats to match standard octet structures.
* **Forensic Output Analysis:**
  ```text
  /mnt/oiMO: 10.10.113.28
  ```
* **SOC / Enterprise Context:** 
  During a security incident (such as a ransomware outbreak or data exfiltration), an analyst must quickly extract Indicators of Compromise (IoCs). This regular expression filtering method allows a SOC team to parse millions of rows of Apache, Nginx, or cloud audit logs to pull malicious external IP addresses or Command and Control (C2) beacon patterns in milliseconds.

---

### Module 3: Cryptographic Integrity Verification (SHA1 Hashing)
* **Objective:** Find the single file that generates a matching cryptographic signature of `9d54da7584015647ba052173b84d45e9007eba94`.
* **Command:**
  ```bash
  find / -type f 2>/dev/null | grep -E "/(8V2L|bny0|c4ZX|D8B3|FHI1|oiMO|PFbD|rmfX|SRSq|uqyw|v2Vb|X1Uy)\$" | xargs sha1sum 2>/dev/null
  ```
* **Forensic Output Analysis:**
  ```text
  9d54da7584015647ba052173b84d45e9007eba94  /mnt/c4ZX
  ```
* **SOC / Enterprise Context:** 
  Filesystem integrity monitoring is a cornerstone of Security compliance (e.g., PCI-DSS, ISO 27001). Malware often tries to disguise itself by replacing system binaries (like `ssh` or `ls`) with malicious variants while keeping the file name identical. By generating a SHA1 or SHA256 checksum hash, an analyst can check it against known threat intelligence databases (like VirusTotal) to confirm if a file is authentic or a dangerous backdoor.

---

### Module 4: Quantitative Structure Analysis (Line Count Extraction)
* **Objective:** Enumerate the exact line structural volume for all files to identify an artifact containing precisely 230 lines of data.
* **Command:**
  ```bash
  find / -type f 2>/dev/null | grep -E "/(8V2L|bny0|c4ZX|D8B3|FHI1|oiMO|PFbD|rmfX|SRSq|uqyw|v2Vb|X1Uy)\$" | xargs wc -l 2>/dev/null
  ```
* **Forensic Output Analysis:**
  ```text
  230 /var/log/uqyw
  ```
* **SOC / Enterprise Context:** 
  Monitoring data structures via `wc -l` (Word Count - Lines) helps baseline standard operations. For example, if a localized firewall log file suddenly changes from its historic baseline of 200 lines a day to 50,000 lines, it signals an immediate anomaly—either an active network attack (Denial of Service) or a configuration error flooding the system.

---

### Module 5: Low-Level User ID Attribution (UID Mapping)
* **Objective:** Isolate the asset whose underlying kernel owner is designated by the numeric User ID (UID) of `502`.
* **Command:**
  ```bash
  find / -type f 2>/dev/null | grep -E "/(8V2L|bny0|c4ZX|D8B3|FHI1|oiMO|PFbD|rmfX|SRSq|uqyw|v2Vb|X1Uy)\$" | xargs ls -ln 2>/dev/null
  ```
* **Technical Parameter Breakdown:**
  * **`-n`**: Explicitly orders `ls` to stop mapping user IDs to their readable plaintext names (like `root`, `ubuntu`) through `/etc/passwd`. Instead, it forces the terminal to display the raw numerical UID and GID stored directly inside the file's inode metadata.
* **Forensic Output Analysis:**
  ```text
  -rw-rw-r-- 1 502 501 13545 Oct 23  2019 /X1Uy
  ```
* **SOC / Enterprise Context:** 
  Attackers often create hidden local backdoor users and manually delete their corresponding text entries from `/etc/passwd` to evade typical security logging tools. By scanning the system using raw numerical values (`-n`), an engineer can track down files owned by "ghost" accounts that don't map to any visible user on the system, exposing stealthy persistence mechanisms.

---

### Module 6: Discretionary Access Control Auditing (Global Executables)
* **Objective:** Review the POSIX permissions matrix across all items to pinpoint any executable artifact available to all users (`everyone`).
* **Command:** Analyzed through the primary permission bits produced via standard long listing formatting.
* **Forensic Output Analysis:**
  ```text
  -rwxrwxr-x 1 501 501 13545 Oct 23  2019 /etc/8V2L
  ```
* **Permissions Decoding Matrix:**
  * The leftmost string sequence `-rwxrwxr-x` is divided into three distinct privilege slots:
    1. `User (rwx)`: Owner can Read, Write, and **Execute** (`x`).
    2. `Group (rwx)`: Group members can Read, Write, and **Execute** (`x`).
    3. `Others (r-x)`: **Any generic user on the system can Read and Execute (`x`).**
