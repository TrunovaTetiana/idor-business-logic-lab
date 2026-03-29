# 🛡️ IDOR & Business Logic Vulnerabilities Lab

## 📌 Overview
This project demonstrates practical exploitation of:
- IDOR (Insecure Direct Object Reference)
- Business Logic vulnerabilities

Tested in a custom vulnerable shop lab.

---

# 🔴 1. IDOR — Access to Other Users' Data

## ✅ Authorized request (baseline)
IDOR baseline

## ❌ Unauthorized access (IDOR)
IDOR attack

## 🔍 Intruder confirmation
IDOR intruder

---

# 💰 2. Price Manipulation

## ✅ Normal price submission
Price baseline

## ❌ Manipulated price
Price attack

## 🔍 Intruder fuzzing
Price intruder

---

# 🚚 3. Shipping Logic Abuse

## ✅ Normal shipping
Ship baseline

## ❌ Unauthorized shipping
Ship attack

---

# 💳 4. Payment Logic Abuse (IDOR + Business Logic)

## ✅ Normal payment
Pay baseline

## ❌ Unauthorized payment
Pay attack

---

# ⚠️ Impact

- Unauthorized access to other users' data
- Manipulation of order price
- Unauthorized order processing (shipping & payment)
- Lack of server-side validation
- Broken access control

---

# 🧠 Key Learning

- Always validate ownership on the server side
- Never trust client-controlled parameters
- Business logic must be strictly enforced

---

# 🛠️ Tools Used

- Burp Suite (Proxy, Repeater, Intruder)
- Browser DevTools
- Manual testing

---

# 👩‍💻 Author

Tatiana Trunova  
Junior Application Security / Pentester (in progress)
