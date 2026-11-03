# Network Protocols & Security Analysis Lab

A hands-on laboratory demonstrating network engineering fundamentals, protocol analysis, and security auditing. This repository contains analysis workflows, capture breakdowns, and core takeaways from investigating Layer 2 through Layer 7 protocols in both plaintext and secure environments.

## 🛠️ Lab Environment & Core Scope

The objective of this lab is to map out and analyze automated configuration protocols, address resolution mechanics, session management, and the crucial distinction between insecure legacy protocols and TLS/SSH alternatives.

*   **Analysis Tools Used:** `Wireshark`, `tshark`, `tcpdump`, `telnet`, `ftp-client`
*   **Target Architectures:** Subnetting environments (Classless Inter-Domain Routing / RFC 1918), local Ethernet topologies, and gateway translation nodes.

---

## 🔬 Core Lab Modules & Technical Breakdowns

### Module 1: Automated Infrastructure Configuration (DHCP & NAT)
This module examines how a host automatically configures its IP stack upon joining an untrusted local network without manual intervention.

#### The DORA Process (UDP Ports 67 & 68)
1.  **DHCP Discover:** The unconfigured client (`0.0.0.0`) broadcasts a request to `255.255.255.255` at the link layer (`ff:ff:ff:ff:ff:ff`) to locate available configuration servers.
2.  **DHCP Offer:** The active DHCP server responds with an available IP lease.
3.  **DHCP Request:** The client broadcasts its formal intent to accept the leased parameters.
4.  **DHCP Acknowledge (ACK):** The server commits the lease and delivers the network payload: the assigned **IPv4 Address/Subnet Mask**, the **Default Gateway (Router)**, and the local **DNS Server** addresses.

```text
# Packet analysis snippet captured via tshark:
1   0.000000      0.0.0.0 → 255.255.255.255 DHCP 342 DHCP Discover - Transaction ID 0xfb92d53f
2   0.013904 192.168.66.1 → 192.168.66.133   DHCP 376 DHCP Offer    - Transaction ID 0xfb92d53f
3   4.115318      0.0.0.0 → 255.255.255.255 DHCP 342 DHCP Request  - Transaction ID 0xfb92d53f
4   4.228117 192.168.66.1 → 192.168.66.133   DHCP 376 DHCP ACK      - Transaction ID 0xfb92d53f
```

#### Network Address Translation (NAT) & Resource Limits
To scale internal networks within the private **RFC 1918** address spaces (`10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`), a NAT gateway was utilized:

*   **PAT / NAT Overload:** The router translates internal private sockets (e.g., `192.168.0.129:15401`) into a single public-facing socket (e.g., `212.3.4.5:19273`).
*   **Hard Operational Limit:** Since TCP/UDP port numbers are constrained to a 16-bit value (usable range: 1–65535), a single public IP address can track a maximum of ~65,000 concurrent translated sessions regardless of hardware throughput.

---

### Module 2: Layer 3 to Layer 2 Mapping (ARP Mechanics)
Before any local data link frames can be transmitted across a physical Ethernet switch or wireless access point, the logical IP address must be bound to a hardware MAC address.

#### The Discovery Phase
*   When host `192.168.66.89` attempts connection to gateway `192.168.66.1`, it utilizes an **ARP Request**.
*   Because the target MAC is unknown, the frame destination is forced to the Layer 2 broadcast address: **`ff:ff:ff:ff:ff:ff`**.
*   **Encapsulation Insight:** ARP payloads are encapsulated **directly into the Ethernet frame**. They do not use an intermediate Layer 3 IP or Layer 4 UDP/TCP wrapper, ensuring raw speed and independence from IP status.

```text
# Low-level frame representation via tcpdump:
17:23:44.506615 ARP, Ethernet (len 6), IPv4 (len 4), Request who-has 192.168.66.1 tell 192.168.66.89, length 28
17:23:44.510182 ARP, Ethernet (len 6), IPv4 (len 4), Reply 192.168.66.1 is-at 44:df:65:d8:fe:6c, length 28
```
*   **Result:** The target hardware responds via unicast, mapping `192.168.66.1` definitively to `44:df:65:d8:fe:6c`, populating the host's volatile local ARP cache.

---

### Module 3: Protocol Interaction & Auditing Legacy Plaintext Sockets
This module replicates low-level manual interactions with application layer services to prove how exposed legacy protocols are to interception.

#### Manual HTTP Debugging via Telnet
By bypassing the web browser rendering engine, raw HTTP commands were issued to verify service availability and extract web resources (`flag.html` analysis):

```bash
telnet 10.112.137.127 80
```
*Manual payload injected:*
```http
GET /flag.html HTTP/1.1
Host: local-audit.thm

```
*   **Security Auditing Takeaway:** All structural components—headers, `GET`/`POST`/`PUT`/`DELETE` methods, and server architecture strings (`Server: Apache/2.x`)—are exposed in raw plaintext inside standard capture logs, failing the **Confidentiality** requirements of modern data protection.

#### Dual-Channel Multi-Connection Layout (FTP)
Testing legacy File Transfer Protocol (FTP) on port 21 highlighted an architecture that presents substantial edge routing challenges:

*   **Control Channel (Port 21):** Handles session initialization, text-based commands, and authentication (`USER anonymous`, `PASS`, `RETR`, `STOR`).
*   **Data Channel (Dynamic Ports):** For every file transmission or directory listing requested (`LIST`), a separate, completely isolated TCP socket is spawned.
*   **Vulnerability:** Unencrypted authentication strings are fully readable via standard packet inspection, presenting severe vulnerabilities to local network sniffers.

#### Mail Retrieval (POP3) Analysis
Analyzing e-mail extraction via POP3 on TCP Port 110:

```bash
telnet 10.112.137.127 110
USER linda
PASS Pa\$123
STAT
LIST
RETR 3
QUIT
```
*   **Operational Flow:** Using `STAT` to check message counts, `LIST` to map sizing parameters, and `RETR` to pull down cleartext SMTP message headers and data strings.

---

## 🛡️ Strategic Implementations: Migrating to Secure Layers

To counteract the lack of data integrity, confidentiality, and authenticity found during auditing, the following production upgrades are mandated:

| Insecure Legacy Protocol | Default Port | Target Secure Protocol | Default Port | Cryptographic / Operational Upgrade |
| :--- | :--- | :--- | :--- | :--- |
| **HTTP** | 80 | **HTTPS** | 443 | Layer 7 stream wrapped in **TLS (Transport Layer Security)**. Implements asymmetric encryption for handshakes and symmetric for data. |
| **POP3** | 110 | **POP3S** | 995 | TLS-encrypted session protecting mailbox metadata, user passwords, and message contents. |
| **SMTP** | 25 | **SMTPS** | 465 | End-to-end transport encryption preventing relay spoofing and intercepting mail-in-flight. |
| **TELNET** | 23 | **SSH** | 22 | Encrypted remote terminal streams providing strong public-key authentication and command integrity checking. |

### The Security Pillars Maintained by TLS/SSH Migration:
*   **Confidentiality:** Mitigates packet sniffing by ensuring data payloads read as high-entropy ciphertext to anyone without the session key.
*   **Integrity:** Uses cryptographic hashing (MAC/HMAC) to prevent **Man-in-the-Middle (MitM)** actors from altering packet payloads (e.g., tampering with payment parameters or transaction amounts) in transit.
*   **Authenticity:** Employs Asymmetric Digital Certificates to formally prove server identity before passing application credentials, eliminating malicious phishing or proxy endpoints.

---

## ☣️ Defensive Note: Living off the Land (LotL)

During our infrastructure defense monitoring, special attention is paid to **Living off the Land (LotL)** techniques.

*   **Mechanics:** Malicious actors attempt to bypass endpoint detection architectures (EDR) by writing zero unique binary payloads to disk. Instead, they hijack legitimate, signed system tools such as **PowerShell** or **WMI (Windows Management Instrumentation)**.
*   **Mitigation Strategy:** Traditional signature-based detection mechanisms fail here. Security teams must enforce behavioral telemetry logging, Constrained Language Mode (CLM) on PowerShell execution, and deep script-block logging policies to baseline administrative anomalies.
