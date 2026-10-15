3# Operating Systems Introduction | Technical Lab Report

## Lab Overview

- **Platform:** TryHackMe
- **Room:** Operating Systems Introduction
- **Category:** Operating Systems / IT Fundamentals
- **Difficulty:** Beginner
- **Tools:** TryHackMe AttackBox or lab environment, Operating System GUI, Command-Line Interface (CLI)
- **Focus:** Operating system architecture, privileges, user management, memory management, processes, hardware and filesystems

---

## 1. Executive Summary

This lab introduced the fundamental concepts of operating systems and their role in managing hardware, applications, and system resources. The learning objectives included understanding kernel space and user space, graphical and command-line interfaces, user privileges, memory management, processes, and filesystems. A practical exercise involved investigating an unfamiliar computer to identify information about its hardware and filesystem configuration.

## 2. Technical Investigation

### 2.1 Understanding Operating System Architecture

An operating system (OS) acts as an intermediary between applications and the underlying hardware. It manages system resources and provides services that allow applications to execute safely and efficiently.

The main responsibilities of an operating system include:

- Managing CPU and memory resources.
- Coordinating running processes.
- Managing users and access permissions.
- Organizing filesystems and storage devices.
- Providing interfaces for user interaction.

### 2.2 Kernel Space vs. User Space

Operating systems separate privileged system operations from regular application execution.

**Kernel Space**

Kernel space is the privileged execution environment where the operating system kernel operates. It provides controlled access to hardware and manages essential system resources.

**User Space**

User space is where ordinary applications and user processes execute with restricted privileges. This separation helps prevent applications from directly interfering with critical operating system components.

From a security perspective, privilege separation reduces the potential impact of application failures and unauthorized operations.

### 2.3 Graphical User Interface (GUI) vs. Command-Line Interface (CLI)

Operating systems provide different ways to interact with the system.

| Interface | Description | Typical Use |
|---|---|---|
| GUI | Visual interface consisting of windows, icons and menus | Navigating settings, files and applications |
| CLI | Text-based interface for executing commands | System administration, troubleshooting and automation |

The CLI is particularly valuable in IT administration and cybersecurity because it enables precise system inspection and efficient execution of repeatable tasks.

### 2.4 User Management and Privileges

User accounts and permissions control access to system resources.

The principle of least privilege means that users and applications should receive only the permissions required to perform their tasks.

Excessive privileges increase the potential impact of compromised accounts, malicious software, and accidental administrative changes.

### 2.5 Memory Management and Processes

An operating system allocates memory and CPU time to running processes.

A **process** is an instance of a running program. The operating system manages process execution, resource allocation, scheduling, and termination.

Memory management helps isolate applications and allocate available resources efficiently. Incorrect permissions or software vulnerabilities can nevertheless allow unauthorized access to resources.

### 2.6 Hardware and Filesystem Investigation

The practical exercise involved examining an unfamiliar computer to learn more about the hardware and filesystems managed by its operating system.

This type of investigation helps establish an understanding of:

- Available hardware resources.
- Storage devices and partitions.
- Filesystem types and mount points.
- The relationship between the operating system and physical or virtual hardware.

No specific hardware identifiers, filesystem outputs, or command results were retained in the available lab notes.

---

## 3. Findings and Key Concepts

- **Operating System:** Manages hardware, applications, and system resources.
- **Kernel Space:** Provides the privileged environment for core operating system operations.
- **User Space:** Hosts regular applications with restricted access to system resources.
- **GUI:** Enables interaction through visual elements.
- **CLI:** Enables command-based system administration and inspection.
- **User Management:** Controls identities, authentication, and permissions.
- **Memory Management:** Allocates and manages memory for processes.
- **Process Management:** Coordinates the execution of running programs.
- **Filesystem Management:** Organizes files, directories, and storage access.

The lab provided foundational knowledge relevant to Linux administration, Windows administration, and cybersecurity operations.

## 4. Security Recommendations

1. **Apply Least Privilege:** Avoid running everyday applications with unnecessary administrative or root privileges. Use elevated permissions only when required.
2. **Monitor Processes and Accounts:** Regularly review running processes, user accounts, and access permissions to identify suspicious activity or unauthorized changes.
3. **Maintain System Security:** Keep operating systems and applications updated, restrict unnecessary services, and apply appropriate filesystem permissions.

## 5. Key Takeaways

This room established a foundation for understanding how operating systems manage hardware, execute applications, allocate memory, and enforce access restrictions.

Understanding the relationship between kernel space, user space, processes, privileges, and filesystems is essential for progressing toward Linux and Windows administration, SOC analysis, and incident response.

---

**Status:** Introductory learning room completed.

**Evidence note:** This report summarizes the concepts covered in the room. Specific practical commands, hardware identifiers, and filesystem outputs were not retained in the available notes.
