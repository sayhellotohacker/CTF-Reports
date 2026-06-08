# 🛡️ Web Security CTF & Vulnerability Write-ups

**Welcome to my cybersecurity research portfolio.**  
This repository contains over **50 technical reports** on exploiting a wide range of web vulnerabilities, from OWASP Top 10 classics to advanced techniques like HTTP Request Smuggling, XXE OOB, WebSocket Hijacking, and Race Conditions.

> **Purpose:** This portfolio demonstrates my hands-on penetration testing skills, my approach to vulnerability discovery and exploitation, and my ability to produce clear, actionable technical reports.

---

## 📊 Key Highlights

| Category | # of Reports |
| :--- | :--- |
| **SQL Injection** | 5 |
| **XSS (DOM, Stored, Reflected)** | 5 |
| **XXE (OOB, SSRF, File Upload)** | 5 |
| **Access Control (IDOR, Privilege Escalation)** | 4 |
| **Authentication & 2FA Bypass** | 3 |
| **SSRF & Command Injection** | 5 |
| **HTTP Request Smuggling (CL.TE, TE.CL, TE.TE)** | 3 |
| **Path Traversal** | 3 |
| **CSRF & CORS** | 4 |
| **SSTI & DOM Clobbering** | 2 |
| **WebSocket** | 2 |
| **Other (Business Logic, API Security, etc.)** | ~10 |
| **Total** | **50+** |

---

## 🎯 Vulnerability Coverage (By Category)

Click on any category to view the detailed write-ups.

### 🔹 Injection Attacks
- **SQL Injection** – Error-based, Blind (Time-based, Conditional), OOB (DNS exfiltration) – [Read more](./SQL-Injection/)
- **Command Injection** – Blind OOB, Time Delay, Output Redirection – [Read more](./Command-Injection/)
- **XXE (XML External Entity)** – Local file disclosure, SSRF to AWS Metadata, OOB data exfiltration via DTD – [Read more](./XXE/)
- **SSTI** – Basic server-side template injection – [Read more](./SSTI/)

### 🔹 Access Control & Authentication
- **IDOR (Insecure Direct Object References)** – Via chat transcripts, user IDs, filename manipulation – [Read more](./Access-Control/)
- **Privilege Escalation** – HTTP method manipulation, GUID-based user identification – [Read more](./Access-Control/)
- **Authentication Bypass** – 2FA via URL manipulation, brute-force protection bypass (IP block, multiple credentials per request) – [Read more](./Authentication/)

### 🔹 Advanced Techniques
- **HTTP Request Smuggling** – CL.TE, TE.CL, TE.TE variants – [Read more](./HTTP-Request-Smuggling/)
- **SSRF (Server-Side Request Forgery)** – Blacklist bypass, URL parser confusion, blind SSRF to internal server + Shellshock RCE – [Read more](./SSRF/)
- **WebSocket Attacks** – Message manipulation, CSWSH (Cross-Site WebSocket Hijacking) – [Read more](./WebSocket/)

### 🔹 Client-Side Attacks
- **XSS (Cross-Site Scripting)** – DOM-based (postMessage, eval), Stored (via DOMPurify bypass), Reflected, Cookie stealing – [Read more](./XSS/)
- **CSRF (Cross-Site Request Forgery)** – SameSite Lax bypass, SameSite Strict bypass via client-side redirect – [Read more](./CSRF/)
- **CORS Misconfiguration** – Origin reflection, trusted insecure protocol – [Read more](./CORS/)
- **DOM Clobbering** – Bypassing DOMPurify to achieve stored XSS – [Read more](./XSS/)

### 🔹 File & Path Manipulation
- **Path Traversal** – Double URL encoding, null byte bypass, non-recursive stripping bypass – [Read more](./Path-Traversal/)

---

## 🧪 How to Navigate This Repository

Each vulnerability category has its own folder (e.g., `SQL-Injection/`). Inside each folder you will find:

- `detailed.md` – The full technical report including:
  - **Step-by-step reproduction**
  - **Burp Suite screenshots** (in `/images` subfolder)
  - **Crafted payloads / scripts**
  - **Impact analysis**
  - **Remediation recommendations**
- `README.md` (in subfolder) – A quick 10-line executive summary of that vulnerability.

This structure allows you to quickly browse the summary or deep-dive into the details.

---

## 🛠️ Tools & Techniques Used

- **Burp Suite Professional** – Manual testing, request manipulation, Intruder, Repeater
- **Nmap** – Network reconnaissance
- **Metasploit** – Exploit development (where applicable)
- **Custom scripts** – Python, Bash for automation
- **Out-of-Band (OOB) techniques** – DNS, HTTP for blind exploitation

---

## 📫 Contact & Collaboration

I am actively looking for **Junior Penetration Tester / Application Security Engineer** roles, preferably remote or in Europe (Spain/Germany).

- **GitHub:** [[Link](https://github.com/sayhellotohacker)]
---

## 📜 License

This repository is for **educational and professional portfolio purposes only**. All write-ups are based on intentionally vulnerable labs (PortSwigger, HackTheBox, TryHackMe) and bug bounty programs where disclosure was permitted.

