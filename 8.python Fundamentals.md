# Python Fundamentals | Incident Report & Analysis

- **Platform:** TryHackMe
- **Category:** Programming Fundamentals / Cybersecurity
- **Difficulty:** Beginner
- **Tools:** TryHackMe, Python 3

---

## 1. Executive Summary

This lab introduced three fundamental concepts used in imperative programming languages: variables, conditional statements, and loops.

The exercises demonstrated how a program stores information, makes decisions based on conditions, and repeats instructions while a condition remains true. These concepts form the foundation for writing scripts that automate tasks, process data, and support security investigations.

The lab also highlighted the importance of practice when learning to write programs and introduced JavaScript as another programming language with similar fundamental concepts.

## 2. Technical Investigation

### 2.1 Variables

Variables store values that a program can use and modify during execution.

Example:

```python
username = "analyst"
attempts = 3
```

- `username` stores a string.
- `attempts` stores an integer.
- Variables allow programs to work with changing data instead of relying on fixed values.

In cybersecurity, variables can store usernames, IP addresses, failed login counts, or other data being processed by a script.

### 2.2 Conditional Statements: `if` and `else`

Conditional statements allow a program to make decisions based on whether a condition is true or false.

Example:

```python
failed_attempts = 5

if failed_attempts >= 3:
    print("Investigate login activity")
else:
    print("No threshold reached")
```

- `if` executes a block of code when its condition is true.
- `else` executes an alternative block when the `if` condition is false.
- Comparison operators such as `==`, `!=`, `>`, `<`, `>=`, and `<=` are used to evaluate conditions.

Conditional logic can be used to identify suspicious activity, evaluate security thresholds, or determine which action a script should take.

### 2.3 Loops: `while`

A `while` loop repeatedly executes a block of code as long as its condition remains true.

Example:

```python
attempts = 0

while attempts < 3:
    print("Checking login attempt")
    attempts += 1
```

- The loop checks its condition before each iteration.
- `attempts += 1` increases the counter by one.
- When `attempts` reaches `3`, the condition becomes false and the loop terminates.

A loop must have a suitable termination condition. If the condition never becomes false, the program may enter an infinite loop.

### 2.4 Combining the Concepts

Variables, conditionals, and loops can be combined to automate simple tasks.

For example, a script could iterate through login events, count failed attempts, and flag accounts that exceed a predefined threshold.

This illustrates how basic programming logic can support log analysis and security automation. It is an illustrative example, not a result from a production security investigation.

## 3. Findings

- Variables allow programs to store and update data.
- `if` and `else` statements control program flow by evaluating conditions.
- `while` loops repeat instructions while a condition remains true.
- These three concepts can be combined to automate repetitive tasks and process security-related data.
- Correct loop termination is important to prevent programs from running indefinitely.
- Understanding existing code is an important first step, but writing and debugging code independently requires practice.
- Python and JavaScript share fundamental programming concepts, although their syntax and runtime environments differ.

## 4. Remediation & Mitigation

To reinforce the concepts covered in this lab:

- **Practise variables:** Create variables containing usernames, IP addresses, and numeric counters.
- **Implement conditional logic:** Use `if` and `else` to classify values or check whether a threshold has been reached.
- **Practise loops:** Use `while` loops to repeat an operation a limited number of times.
- **Prevent infinite loops:** Ensure that loop conditions can eventually become false.
- **Read and modify existing code:** Change variable values and conditions to understand how program behaviour changes.
- **Apply the concepts to cybersecurity:** Build small scripts that process sample log entries or count failed login attempts.
- **Compare programming languages:** Explore how Python and JavaScript implement variables, conditionals, and loops.

### Key Takeaway

Variables store data, conditionals make decisions, and loops repeat operations. Together, these concepts form the foundation of imperative programming and are useful for scripting, automation, log analysis, and future cybersecurity work.

**Lab Status:** Foundational programming concepts reviewed.
