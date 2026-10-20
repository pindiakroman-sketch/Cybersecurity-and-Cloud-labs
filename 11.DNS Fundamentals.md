# DNS Fundamentals | Incident Report & Analysis

- **Platform:** TryHackMe
- **Category:** Networking / Cybersecurity
- **Difficulty:** Beginner
- **Tools:** TryHackMe DNS Query Tool, DNS Lookup Commands

---

## 1. Executive Summary

This lab explored the Domain Name System (DNS) and how DNS queries retrieve records associated with domain names.

Using a web-based DNS query tool, different DNS record types were examined, including CNAME, TXT, MX, and A records. The tool also displayed equivalent commands that could be executed locally to perform DNS lookups.

Understanding DNS is important for network troubleshooting, domain configuration, and cybersecurity investigations involving suspicious domains or DNS activity.

## 2. Technical Investigation

### 2.1 DNS Queries

DNS translates domain names into information required by network services. Depending on the query type, DNS can return an IP address, an alias, mail server information, or text data.

The lab used a web-based interface to query DNS records and inspect the returned values.

### 2.2 DNS Record Types

**A Record — IPv4 Address**

Maps a hostname to an IPv4 address.

- **Query:** `www.website.thm`
- **Result:** `10.10.10.10`

**CNAME Record — Canonical Name**

Creates an alias that points to another domain name.

- **Query:** `shop.website.thm`
- **Result:** `shops.myshopify.com`

A CNAME points to another hostname rather than directly providing an IP address.

**TXT Record — Text Data**

Stores text associated with a domain. TXT records can support domain verification, email security policies, and other administrative purposes.

- **Query:** `website.thm`
- **Result:** `THM{7012BBA60997F35A9516C2E16D2944FF}`

The returned value was the answer provided by the lab. TXT records can contain different kinds of text, and their purpose depends on the content and configuration.

**MX Record — Mail Exchange**

Specifies mail servers responsible for receiving email for a domain. MX records include a numerical priority value.

- **Query:** MX record for the lab domain
- **Result:** Priority value `30`

Lower numerical values indicate higher preference when selecting among MX records, assuming the relevant mail servers are available.

### 2.3 Performing DNS Lookups Locally

DNS queries can also be performed from a command line.

Examples using `nslookup`:

```bash
nslookup -type=A www.website.thm
nslookup -type=CNAME shop.website.thm
nslookup -type=TXT website.thm
nslookup -type=MX website.thm
```

These commands request specific DNS record types. Results depend on the DNS environment and the availability of the queried domain.

## 3. Findings

The lab confirmed the following DNS record values:

| Record Type | Query | Result |
|---|---|---|
| CNAME | `shop.website.thm` | `shops.myshopify.com` |
| TXT | `website.thm` | `THM{7012BBA60997F35A9516C2E16D2944FF}` |
| MX Priority | `website.thm` | `30` |
| A | `www.website.thm` | `10.10.10.10` |

Key observations:

- A records associate hostnames with IPv4 addresses.
- CNAME records point aliases to canonical hostnames.
- TXT records can store verification data and security-related configuration.
- MX records identify mail servers and their delivery priorities.
- DNS results can help analysts understand domain infrastructure, but individual records do not independently establish malicious activity.

## 4. Remediation & Mitigation

- **Validate DNS configuration:** Regularly review records for unexpected or unauthorised changes.
- **Investigate suspicious domains:** Examine relevant A, CNAME, MX, and TXT records when analysing potentially malicious infrastructure.
- **Protect DNS administration:** Restrict access to domain registrar accounts and DNS management platforms.
- **Monitor DNS activity:** Investigate unusual queries, unexpected domain resolutions, and suspicious changes where suitable logging is available.
- **Use DNS security controls:** Apply appropriate measures such as DNS filtering and DNSSEC validation where supported. DNSSEC helps validate DNS data authenticity and integrity but does not encrypt DNS queries.

### Key Takeaway

DNS records provide different types of information about a domain. Knowing how to query and interpret A, CNAME, TXT, and MX records is a fundamental skill for network troubleshooting and security analysis.

**Lab Status:** Completed — DNS record queries performed and results identified.
