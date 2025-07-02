# OWASP Juice Shop Penetration Testing Report

![OWASP Juice Shop Logo](https://raw.githubusercontent.com/juice-shop/juice-shop/master/frontend/src/assets/public/images/JuiceShop_Logo.png)

## Overview
This repository contains the findings and methodology of a **black-box penetration test** conducted on the OWASP Juice Shop application (`demo.owasp-juice.shop`). The assessment focused on identifying vulnerabilities aligned with the **OWASP Top 10 (2023)**.

---

## Key Vulnerabilities Discovered
| Vulnerability | Severity | Impact |
|--------------|----------|--------|
| **Broken Access Control** | Critical | Unauthorized access to admin panels and user data. |
| **SQL Injection (Multiple Vectors)** | Critical | Bypass authentication, extract data, and execute arbitrary SQL. |
| **CSRF (Cross-Site Request Forgery)** | High | Unauthorized actions (e.g., profile tampering) via malicious requests. |
| **IDOR (Insecure Direct Object Reference)** | High | Access/modify other users’ data by manipulating object IDs. |
| **Predictable OAuth State** | Critical | Session hijacking via guessable OAuth tokens. |
| **JWT Token Disclosure** | High | Admin credentials leaked via weakly secured tokens. |
| **Backup File Exposure** | Medium | Sensitive files (e.g., coupons, configs) accessible via directory brute-forcing. |

---

## Tools Used
- **Scanners**: Burp Suite, Acunetix, Nuclei  
- **Brute-Forcing**: Gobuster (with SecLists)  
- **Exploitation**: SQLmap, custom scripts  
- **Manual Testing**: CSRF, authentication bypass, business logic flaws  

---

## Critical Findings
1. **Authentication Bypass**  
   - SQLi payloads (`'OR 1=1--`) granted admin access.  
   - Predictable OAuth passwords (base64-encoded reversed emails).  

2. **Admin Account Takeover**  
   - JWT tokens exposed MD5-hashed passwords (e.g., `admin123`).  

3. **Data Manipulation**  
   - IDOR allowed editing other users’ baskets.  
   - Weak coupon encryption (Z85 encoding) enabled unauthorized discounts.  

---

## Recommendations
- 🔒 **Enforce CSRF tokens** and validate request origins.  
- 🛡️ **Use parameterized queries** to prevent SQLi.  
- 🔑 **Secure OAuth flows** with unpredictable state values.  
- 🚫 **Restrict sensitive endpoints** with role-based access control (RBAC).  
- 📜 **Implement security headers** (CSP, HSTS, HttpOnly cookies).  

---

## Full Report
For detailed methodology, PoCs, and remediation steps, refer to:  
📄 [Web Penetration Testing Project - Notion Documentation](https://www.notion.so/Web-Penetration-Testing-Project-1edb802eb69a80b191c3dc7fd968d6f2?pvs=4)  

---

## Contributors
- [Mark Mekhael Adly]()  
- [Hassan Amgad Hassan]()  
- [Shahd Ahmed Mohamad]()  
- [Mohamad Mahmoud Ali]()  

> **Note**: Juice Shop is an intentionally vulnerable app for educational purposes.  
> **Disclaimer**: Testing was authorized; vulnerabilities reported responsibly.  