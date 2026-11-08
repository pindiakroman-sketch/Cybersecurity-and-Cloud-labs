# 🛠️ Tcpdump & Network Packet Filtering – Practical Cheat Sheet

This repository serves as a practical guide and a quick cheat sheet for working with `tcpdump` during network analysis. It is designed to provide immediate answers when analyzing network traffic (PCAP files) without digging through dense manual pages, focusing on clear logic and real-world examples.

## 📌 Core Command Syntax

| Command / Switch | Meaning |
| :--- | :--- |
| `tcpdump -r file.pcap` | **R**ead – Reads packets from a saved file instead of capturing live network traffic. |
| `tcpdump -n` | **N**umeric – Displays raw IP addresses and port numbers. Disables reverse DNS resolution (e.g., shows `8.8.8.8` instead of `dns.google`), saving time. |
| `tcpdump -e` | **E**thernet – Prints the link-layer headers, revealing the physical **MAC addresses** of the sender and receiver. |

---

## ⚡ Filtering Expressions

Filters are appended to the end of the command. If a filter contains special characters, brackets, or operators, it must be wrapped in quotes `""`.

### 1. Filtering by Packet Size
Essential for detecting data exfiltration, tunneling, or non-standard protocol behavior.
* `greater LENGTH` – Filters packets with a length greater than or equal to the specified bytes.
* `less LENGTH` – Filters packets with a length less than or equal to the specified bytes.

*Example:* Finding the sender of unusually large packets:
```bash
tcpdump -r traffic.pcap -n greater 15000
```
> 💡 **Output Analysis:** Look for the format `IP SOURCE > DESTINATION`. For a line like `IP 185.117.80.53.443 > 10.10.1.5.51234`, the host sending the large packet is `185.117.80.53` (on port `443`).

### 2. Filtering ARP Traffic (Address Resolution Protocol)
ARP is used by network devices to map an IP address to a physical MAC address.
* `arp` – Restricts the output entirely to ARP requests and replies.

*Example:* Finding the MAC address of a host that broadcasted a specific request:
```bash
tcpdump -r traffic.pcap -n -e arp
```
> 💡 **Output Analysis:** 
> `52:54:00:7c:d3:5b > ff:ff:ff:ff:ff:ff ... Request who-has 192.168.124.137`
> The direction pointer `>` isolates the sender on the left side. The MAC address that initiated the request is `52:54:00:7c:d3:5b`.

---

## 🧠 Advanced TCP Flag Filtering Logic

Inside the TCP header, a single byte (8 bits) is dedicated to **TCP Flags** (`SYN`, `ACK`, `RST`, `FIN`, etc.). Each bit acts as an independent toggle switch (`0` for off, `1` for on). We interact with this byte using `tcp[tcpflags]`.

To filter successfully, it is critical to understand the difference between an **Exact Match** and a **Bitwise Mask**.

```text
[ CWR | ECE | URG | ACK | PSH | RST | SYN | FIN ]  <-- The 8-bit flag layout (Switches)
```

### A) Exact Match (`==`) – Finding "ONLY this flag"
Used when you want to isolate packets where **one specific flag is active and all other 7 flags are strictly unset**.

```bash
tcpdump -r traffic.pcap "tcp[tcpflags] == tcp-rst"
```
* **Why it works:** The system checks the entire byte value. If the packet has *only* the `RST` bit flipped on, it matches. If a packet has both `RST` and `ACK` enabled, the exact match fails and the packet is ignored.

### B) Bitwise Mask (`& != 0`) – Finding "AT LEAST this flag"
Used when you only care about the status of a specific flag, regardless of what the other flags are doing. The bitwise `&` (AND) operator acts as a stencil, hiding the other bits.

```bash
tcpdump -r traffic.pcap "tcp[tcpflags] & tcp-syn != 0"
```
* **Why it works:** This filter captures pure `SYN` packets as well as combined `SYN-ACK` packets because it strictly verifies whether the `SYN` bit is turned on, ignoring the rest.

---

## 📊 Automated Packet Counting

Instead of manually reading thousands of lines in the terminal, we leverage the Linux pipe (`|`) to stream the `tcpdump` text output into a line counter (`wc -l`).

```bash
tcpdump -r traffic.pcap "tcp[tcpflags] == tcp-rst" | wc -l
```
1. `tcpdump` evaluates the file and outputs **exactly 1 line of text** for each packet matching the filter.
2. The pipe `|` redirects this text away from the screen and passes it to the next utility.
3. `wc -l` (Word Count - Lines) counts the incoming lines, instantly returning the precise number of packets.
