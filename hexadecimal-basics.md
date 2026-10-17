# Hexadecimal Basics | Incident Report & Analysis

- **Platform:** TryHackMe
- **Category:** IT Fundamentals / Cybersecurity
- **Difficulty:** Beginner
- **Tools:** TryHackMe, Hexadecimal Conversion
- **Focus:** Number systems, binary representation, hexadecimal-to-decimal conversion

---

## 1. Executive Summary

This lab covered the fundamentals of hexadecimal notation and its relationship to the decimal number system. The objective was to understand hexadecimal place values, convert hexadecimal values into decimal numbers, and recognize the relevance of hexadecimal representation in cybersecurity and low-level system analysis.

## 2. Technical Investigation

### Step 1: Understanding the Hexadecimal System

The hexadecimal number system uses base 16 and consists of 16 symbols:

- `0–9` represent decimal values 0–9.
- `A–F` represent decimal values 10–15.

Unlike the decimal system, which uses powers of 10, hexadecimal uses powers of 16.

| Position | Place Value |
|---|---:|
| Second digit from the right | \(16^1 = 16\) |
| First digit from the right | \(16^0 = 1\) |

### Step 2: Converting Hexadecimal to Decimal

To convert a two-digit hexadecimal value into decimal, multiply the first digit by 16 and add the second digit.

**Example: Convert `AB` to decimal.**

1. Convert the hexadecimal symbols into decimal values:
   - `A = 10`
   - `B = 11`

2. Apply the place values:

   \[
   AB_{16} = (10 \times 16) + (11 \times 1)
   \]

3. Calculate the result:

   \[
   160 + 11 = 171
   \]

**Result:** `AB` in hexadecimal equals `171` in decimal.

### Step 3: Additional Conversion Examples

| Hexadecimal | Calculation | Decimal |
|---|---|---:|
| `2F` | \(2 \times 16 + 15\) | 47 |
| `3C` | \(3 \times 16 + 12\) | 60 |
| `AC` | \(10 \times 16 + 12\) | 172 |
| `D4` | \(13 \times 16 + 4\) | 212 |
| `FF` | \(15 \times 16 + 15\) | 255 |

A single hexadecimal digit represents four bits. Two hexadecimal digits can represent one byte, with values ranging from `00` to `FF` (decimal 0–255).

### Step 4: Understanding Cybersecurity Applications

Hexadecimal notation is commonly used in technical environments, including:

- **Network analysis:** Inspecting packet contents in tools such as Wireshark.
- **Digital forensics:** Examining file contents and binary data through hexadecimal dumps.
- **Data representation:** Reading byte values and understanding how information is represented at a low level.

These applications provide context for learning hexadecimal conversion, although this lab focused on the underlying number system rather than performing a full security investigation.

## 3. Findings

- Identified hexadecimal as a base-16 number system.
- Learned the decimal equivalents of hexadecimal symbols `A–F`.
- Practiced converting hexadecimal values into decimal numbers.
- Confirmed that `AB` hexadecimal equals `171` decimal.
- Learned that two hexadecimal digits represent one byte, with a maximum value of `255`.
- Reviewed the relevance of hexadecimal notation to network analysis and digital forensics.

## 4. Recommended Security Practices (Remediation & Mitigation)

1. **Develop Binary Data Literacy:** Understand hexadecimal and byte representation to improve the interpretation of network packet captures, file headers, and forensic artifacts.
2. **Use Appropriate Analysis Tools:** Use tools such as Wireshark and hexadecimal viewers when inspecting raw data instead of relying on manual interpretation alone.
3. **Validate Technical Findings:** When investigating suspicious data, correlate hexadecimal observations with file metadata, protocol specifications, logs, and other available evidence before drawing conclusions.

---

**Status:** Foundational learning exercise completed.

**Key Takeaway:** Understanding hexadecimal notation makes it easier to interpret low-level data encountered in network analysis, digital forensics, and cybersecurity investigations.
