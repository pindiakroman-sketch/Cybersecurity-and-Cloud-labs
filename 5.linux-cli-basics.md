# Linux CLI Basics | System Investigation & Analysis

## Lab Overview

- **Platform:** TryHackMe
- **Category:** Linux Administration / Security Fundamentals
- **Difficulty:** Beginner
- **Tools:** Linux CLI, Bash
- **Focus:** Filesystem navigation, file discovery, system enumeration, configuration file analysis

---

## 1. Executive Summary

This lab focused on using the Linux command-line interface to navigate the filesystem, locate files, inspect system information, and examine configuration files. These techniques form the foundation of Linux system administration and security investigations, where command-line tools are used to identify system properties, locate relevant artifacts, and investigate potential misconfigurations.

## 2. Technical Investigation

### 2.1 Filesystem Navigation

Linux filesystem navigation allows analysts to inspect directories and identify relevant system locations.

Common commands include:

```bash
pwd
ls -la
cd /etc
```

- `pwd` displays the current working directory.
- `ls -la` lists directory contents, including hidden files and file permissions.
- `cd` changes the current directory.

### 2.2 File Discovery

File search capabilities are essential when locating configuration files, logs, and other system artifacts.

Example:

```bash
find /etc -type f
```

This command searches for regular files under `/etc`, a directory commonly used for system-wide configuration.

To locate files by name:

```bash
find /etc -type f -name "*.conf"
```

Search scope and file permissions affect which results are returned.

### 2.3 System Enumeration

Basic system enumeration helps establish the operating system environment and current user context.

```bash
whoami
id
uname -a
```

These commands provide information about the current user, identity and group memberships, and kernel and system details.

### 2.4 Configuration File Inspection

Linux configuration files can reveal how system services and applications are configured.

Example:

```bash
cat /etc/os-release
```

This displays operating system identification information, including the distribution name and version where provided.

For longer files, `less` can be used to inspect content interactively:

```bash
less /etc/os-release
```

Configuration files should be inspected with appropriate permissions, and sensitive information must be handled carefully.

## 3. Findings

- Practiced navigating the Linux filesystem using the CLI.
- Reviewed methods for locating files and filtering search results.
- Explored commands for identifying the current user and inspecting system information.
- Examined the role of Linux configuration files in system administration.
- Established foundational skills for investigating Linux systems through command-line tools.

**Evidence limitation:** The available notes do not contain the exact mission answers, commands executed during the room, target system details, or captured command output. The commands above are representative examples and are not claimed as recorded lab evidence.

## 4. Security Recommendations

1. **Review File Permissions:** Apply least-privilege permissions to sensitive configuration files and restrict access to authorized users.
2. **Protect Sensitive Configuration Data:** Avoid exposing credentials, API keys, and other secrets in configuration files or shell output.
3. **Improve Investigation Readiness:** Familiarize yourself with important system directories and preserve relevant logs and system information when investigating suspicious activity.

## 5. Key Takeaways

Linux CLI skills are essential for system enumeration, troubleshooting, and security analysis. The ability to navigate filesystems, search for artifacts, inspect system details, and read configuration files provides a foundation for more advanced topics such as permissions, process analysis, user management, log investigation, and incident response.

---

**Status:** Learning room completed.

**Evidence note:** This report documents the concepts covered based on the available room summary. Example commands are included for technical reference; their execution during the lab has not been independently verified.
