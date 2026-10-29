# Linux Bash Scripting - Log Analyzer Project

This project shows my practical skills with the Linux command line and basic Bash scripting. I created and fixed a script during a lab challenge on TryHackMe to automate searching through system logs.

## 🎯 Project Goals
* Navigate the Linux file system using the terminal.
* Fix a broken Bash script template and make it work.
* Learn how to use `sudo` and change file permissions with `chmod`.
* Use the `grep` command to find specific text hidden inside log files.

---

## 🛠️ Commands and Tools Used
* **OS:** Linux (Ubuntu environment)
* **Shell:** Bash
* **Editor:** Nano
* **Commands:** `cd`, `ls`, `pwd`, `cat`, `sudo`, `chmod`, `grep`, `basename`

---

## 💻 Step-by-Step Process & Troubleshooting

### 1. Navigating the System
First, I needed to find where the script was located. I used these commands to explore the directories:
* `pwd` – Checked my current folder (`/home/user`).
* `ls` – Listed the files and found the script named `flag_hunt.sh`.

### 2. Fixing Permission Issues
When I tried to edit and run the script, I ran into permission errors (`Permission denied` and `Operation not permitted`). I solved this by using admin privileges:
* **Editing with sudo:** I opened the file using `sudo nano flag_hunt.sh` because my regular user could not save changes to the file.
* **Making it executable:** I gave the script permission to run using this command:
  ```bash
  sudo chmod +x flag_hunt.sh
  ```

### 3. Debugging the Script
The original script template was not working because it was looking for `.log` files inside the wrong folder (`/home/user`), where no logs existed. System logs are actually stored in `/var/log`.

I opened the script in the Nano editor and fixed the path inside the `for` loop.

#### The broken line:
```bash
for file in "/home/user"/*.log; do
```

#### My fixed and final script:
```bash
#!/bin/bash 

# 1. Setting the correct log directory
directory="/var/log"

# 2. Setting the keyword we want to find
flag="thm-flag01-script"

echo "Flag search in directory: \$directory in progress..."

# 3. Loop through all .log files in /var/log
for file in "\$directory"/*.log; do

        # Search for the keyword silently (-q means quiet mode)
        if grep -q "flag" "file"; then
                # Print only the filename using 'basename'
                echo "Flag found in: (basename "file")"
        fi
done
```

### 4. Running the Script & Using a Faster Alternative
After saving the changes, I ran my script using:
```bash
./flag_hunt.sh
```

**Alternative Method:** I also learned that I could achieve the exact same result instantly without a script by using a single one-liner `grep` command in the terminal:
```bash
grep -rn "thm-flag01-script" /var/log/
```
*(Where `-r` looks inside all subfolders and `-n` shows the exact line number).*

---

## 📈 Final Results
Both my fixed Bash script and the manual `grep` command successfully scanned the system logs and discovered that the hidden keyword was located inside this specific file:
**`authentication.log`**

To print the actual secret flag on the screen without opening the whole huge log file, I used:
```bash
grep "thm-flag01-script" /var/log/authentication.log
```

## 🧠 What I Learned (My Skills)
* How to write and debug simple Bash scripts (using `variables`, `if/else` statements, and `for` loops).
* How Linux file permissions work (`chmod +x` and when to use `sudo`).
* How to analyze text and search through logs efficiently using `grep`.
