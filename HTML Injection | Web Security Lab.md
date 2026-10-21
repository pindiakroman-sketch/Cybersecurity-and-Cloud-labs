# HTML Injection | Web Security Lab

- **Platform:** TryHackMe
- **Category:** Web Security / Application Security
- **Difficulty:** Beginner
- **Tools:** TryHackMe, Web Browser, HTML, JavaScript

---

## 1. Objective

Understand how HTML Injection occurs when a web application displays untrusted user input without properly handling it.

The lab explored how user-controlled input can affect the HTML rendered by a browser, why input handling is important, and how developers can prevent injected markup from being interpreted as HTML.

## 2. Technical Investigation

### 2.1 How HTML Injection Works

HTML Injection occurs when an application inserts user-controlled input into a web page in a way that causes the browser to interpret the input as HTML.

For example, a website may ask a user for their name and display a greeting. If the submitted value is inserted into the page without safe handling, a user may be able to change the page's appearance.

Example test input:

```html
<h1>HTML Injection Test</h1>
```

If the application interprets this input as HTML, the browser renders a heading rather than displaying the literal tag.

### 2.2 HTML Link and User-Controlled Input

An HTML link can be created using the anchor (`<a>`) element.

Example:

```html
<a href="https://example.com">Visit website</a>
```

- `<a>` defines a hyperlink.
- `href` specifies the destination.
- `Visit website` is the clickable text.

If a vulnerable application interprets user-supplied HTML, an attacker may attempt to inject their own links into the page. Depending on the context, this could mislead users into visiting an untrusted destination.

A link by itself is normal HTML, not proof of a vulnerability. The security issue arises when the application handles untrusted input unsafely.

### 2.3 Root Cause

The underlying problem is improper handling of untrusted input when generating page content.

For example, JavaScript code that inserts input through `innerHTML` may cause the browser to parse that input as markup.

```javascript
output.innerHTML = userInput;
```

This pattern is unsafe when `userInput` contains untrusted data.

### 2.4 HTML Injection vs. Cross-Site Scripting (XSS)

HTML Injection can allow an attacker to alter page content or appearance. Cross-Site Scripting (XSS) occurs when attacker-controlled script executes in a victim's browser.

These vulnerabilities are related, but HTML Injection does not automatically mean that JavaScript execution is possible. The impact depends on the injection context and the application's behaviour.

## 3. Findings

- HTML Injection can occur when untrusted input is interpreted as HTML.
- Injected markup may change page content or introduce misleading links.
- The anchor (`<a>`) element creates hyperlinks, while the `href` attribute defines their destination.
- Unsafe use of `innerHTML` can cause input to be parsed as markup.
- HTML Injection and XSS are distinct vulnerabilities, although unsafe HTML handling can contribute to XSS.
- The core security principle is to treat user input as untrusted.

## 4. Remediation & Mitigation

- **Use safe DOM APIs:** Prefer `textContent` when displaying user input as plain text.
- **Apply context-appropriate output encoding:** Ensure user-supplied data is interpreted as data rather than executable markup.
- **Validate input:** Enforce expected formats and acceptable values.
- **Sanitise HTML when necessary:** If an application intentionally accepts HTML, use a reputable HTML sanitisation library.
- **Validate links:** Where user-submitted links are allowed, validate permitted URL schemes and apply appropriate destination restrictions.
- **Use defence in depth:** A Content Security Policy (CSP) can help reduce the impact of certain injection attacks, but does not replace fixing unsafe output handling.

## 5. Practical Demonstration & Validation

### Objective

Understand the difference between rendering user input as HTML and displaying it as plain text.

### Test Input

```html
<h1>HTML Injection Test</h1>
<a href="https://example.com">Visit website</a>
```

### Expected Results

- **Vulnerable handling:** The browser may interpret the input as HTML, rendering a heading and a hyperlink.
- **Secure handling:** The input is displayed as literal text instead of being interpreted as HTML.

### Secure JavaScript Example

```javascript
const output = document.getElementById("output");
const userInput = document.getElementById("name").value;

output.textContent = userInput;
```

Using `textContent` ensures the input is treated as text rather than parsed as HTML.

### Validation Checklist

- [ ] Understand how an HTML link is constructed.
- [ ] Identify why unsafe handling of user input can introduce HTML.
- [ ] Compare the expected behaviour of vulnerable and secure implementations.
- [ ] Verify that user input is displayed safely.
- [ ] Document the actual results with a screenshot, if available.

### Evidence

Add a screenshot of your actual lab result:

`![HTML Injection Lab Results](screenshots/html-injection-test.png)`

Replace the example path with the actual screenshot path in the repository.

## Key Takeaway

HTML Injection occurs when untrusted user input is interpreted as HTML. Understanding HTML elements, hyperlinks, DOM manipulation, and safe output handling provides a foundation for learning web application security and preventing injection vulnerabilities.

**Lab Status:** Foundational HTML Injection concepts reviewed.
