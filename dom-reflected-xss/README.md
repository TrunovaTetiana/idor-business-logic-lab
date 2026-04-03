# 🔥 XSS Vulnerability Report (DOM + Reflected)

---

## 📌 Tester Information
- Name: Tatiana  
- Environment: Local Vulnerable Shop Lab  
- Target: http://192.168.1.48:8002  

---

## 🧠 Vulnerability Overview

During testing, multiple Cross-Site Scripting (XSS) vulnerabilities were identified:

- DOM-based XSS (via location.hash)
- Reflected XSS (via search.php)
- Multiple payload vectors confirmed (img, iframe, script)

The application fails to properly sanitize user-controlled input before rendering it in the DOM.

---

# 🔴 1. DOM-Based XSS

---

## 📍 Entry Point

User-controlled input is taken from the URL fragment:

location.hash

---

## ⚠️ Root Cause

var input = location.hash.substring(1);
document.getElementById("output").innerHTML = input;

The application uses innerHTML, which allows execution of arbitrary HTML/JavaScript.

---

## 💉 Payload

<img src=x onerror=alert(1)>

---

## 📸 Proof of Concept

### 1. Payload Injection
![Payload Injection](images/02_payload_injection.png)

---

### 2. DOM Source → Sink
![DOM Source Sink](images/03_dom_source_sink.png)

---

### 3. DOM Execution
![DOM Execution](images/04_dom_execution.png)

---

### 4. Alert Execution (Impact)
![Alert DOM](images/05_alert_dom.png)

---

### 5. Alternative Payload (iframe)

<iframe src=javascript:alert(1)>

![Iframe Payload](images/06_payload_iframe.png)

---

### 6. Burp Verification
![Burp Request](images/07_burp_request.png)

---

## ✅ Result

JavaScript execution confirmed in browser via DOM injection.

---

# 🔴 2. Reflected XSS

---

## 📍 Entry Point

GET /search.php?q=

---

## 💉 Payload

<script>alert(1)</script>

---

## 📸 Proof of Concept

### 1. Baseline Response
![Baseline](images/09_reflected_baseline.png)

---

### 2. Payload Injection
![Payload](images/10_reflected_payload.png)

---

### 3. Alert Execution
![Alert](images/11_reflected_alert.png)

---

## ✅ Result

User input is reflected in the response without sanitization, leading to script execution.

---

# 🔥 Security Impact

- Arbitrary JavaScript execution
- Session hijacking potential
- Credential theft
- DOM manipulation
- Phishing attacks

---

# 🛠️ Recommendations

Avoid:
- innerHTML
- document.write

Use:
- textContent
- innerText

Apply:
- Output encoding
- Input validation
- Content Security Policy (CSP)

---

# 🧾 Conclusion

The application is vulnerable to multiple XSS attack vectors due to improper handling of user input. Both DOM-based and Reflected XSS were successfully exploited.

---

🚀 This case demonstrates real-world exploitation scenarios and multiple injection techniques.
