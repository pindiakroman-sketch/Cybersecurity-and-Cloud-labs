# Search Skills | Cybersecurity Research Lab

- **Platform:** TryHackMe
- **Category:** Cybersecurity Fundamentals / OSINT
- **Difficulty:** Beginner
- **Tools:** Shodan, VirusTotal, CVE Databases, Linux `man` Pages, GitHub

---

## 1. Objective

Learn how to find and interpret technical information using specialised search engines, security intelligence platforms, vulnerability databases, technical documentation, and code repositories.

The room introduced research methods that help security professionals investigate internet-connected systems, examine suspicious files or indicators, identify known vulnerabilities, understand command-line tools, and find relevant technical implementations.

## 2. Tools & Methodology

### 2.1 Shodan

Shodan is a search engine for internet-connected devices and services. It can help identify exposed services and understand the externally visible attack surface of a system.

**Security relevance:** Security teams can use Shodan to investigate their organisation's internet-facing assets and identify potentially exposed services.

### 2.2 VirusTotal

VirusTotal aggregates information from multiple security engines and other analysis sources to help assess files, URLs, domains, and IP addresses.

**Security relevance:** Analysts can use it as one source of threat intelligence when investigating suspicious indicators. Results require context and do not independently prove that an item is malicious or safe.

### 2.3 Vulnerability Databases — CVE

Common Vulnerabilities and Exposures (CVE) provides identifiers for publicly disclosed cybersecurity vulnerabilities.

A CVE record helps researchers refer to a specific vulnerability consistently. Additional databases, such as the National Vulnerability Database (NVD), can provide enrichment including severity information and affected-product details.

**Security relevance:** Identifying relevant CVEs helps teams assess exposure, prioritise patching, and investigate vulnerable software.

### 2.4 Linux Manual Pages — `man`

Linux manual pages provide documentation for commands, configuration files, and system interfaces.

Example:

```bash
man ls
man grep
man ip
```

Manual pages commonly describe command syntax, available options, and usage details.

**Security relevance:** Reading documentation helps analysts use tools correctly and understand command behaviour instead of relying solely on copied commands.

### 2.5 GitHub

GitHub hosts source code, scripts, tools, and technical documentation. Security professionals can use it to research implementations, review code, and learn how tools work.

**Security relevance:** Code repositories can help analysts understand security tools and investigate potential vulnerabilities. Repository quality, maintenance status, and code safety should be assessed before running third-party software.

## 3. Findings

- Different research tools answer different types of technical questions.
- Shodan helps investigate internet-exposed services.
- VirusTotal provides security intelligence about files and network indicators.
- CVE records provide consistent identifiers for disclosed vulnerabilities.
- Linux manual pages offer authoritative local documentation for supported commands.
- GitHub enables code research and examination of tool implementations.
- Search results must be evaluated critically and verified using appropriate sources.

## 4. Practical Security Relevance

These skills support common cybersecurity activities:

- Researching exposed infrastructure.
- Investigating suspicious URLs, domains, IP addresses, or files.
- Identifying vulnerabilities affecting software in use.
- Learning command-line tools through their documentation.
- Reviewing scripts and tools before using them in an investigation.

Research must remain within authorised scope. Public visibility does not automatically grant permission to test or access a system.

## Key Takeaway

Effective cybersecurity work depends on more than knowing tools: it requires finding reliable information, understanding the evidence, and validating conclusions. Specialised search platforms and technical documentation help analysts investigate efficiently and make better-informed security decisions.

**Lab Status:** Completed — foundational cybersecurity research skills reviewed.
