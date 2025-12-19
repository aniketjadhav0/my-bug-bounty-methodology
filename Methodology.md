# 🔐 Bug Bounty Authentication & Access Control Testing Methodology

> 📌 **Disclaimer**  
> This repository is shared **only for educational and learning purposes**.  
> It explains **security testing methodologies**, not exploitation.  
> **Do not** use this information on systems without proper authorization.

---
---

## 1️⃣ Registration Function Testing

While testing the registration functionality, I check the following:

- **SQL Injection**
  - In username input
  - In email input  

- **Blind XSS**
  - Via User-Agent
  - Via username field  

- Registering with an **existing email address**  
- **Unicode email bypass testing**
  - Example: `dewⒸode@email.com`
  - Reference: https://www.compart.com/en/unicode/category/So  

- Registering from **mobile with the same email**  
- Attempting to **overwrite default web application pages** using crafted usernames  

  Example check:
  http://www.chintan.com/dewcode

  
- Enumerating default folders such as:
- `/images`
- `/contact`
- `/portfolio`

- Registering with usernames like:
- images
- contact
- portfolio  

- Checking whether these folders are overwritten by the profile link  
- **OTP bypass and OTP reuse testing**  
- **Open Redirect testing**  
- **Email verification bypass testing**

---

## 2️⃣ Password Reset Function Testing

For password reset functionality, I test:

- **SQL Injection**
- In email input
- Sending POST request to `sqlmap`  

- **XSS**
- In email input
- In token input  

- **Blind XSS**
- Via User-Agent  

- Reusing password reset tokens  
- Checking for **leaked reset tokens** in responses  

- **Host Header poisoning** to trigger Blind XSS:
 Host: web..com"><img src=blind-xss-payload>


- **Header Injection**  
- **Parameter Pollution**

- **HTML Injection / Content Spoofing**
```html
<a href="https://evil.com">Click me</a>
<img src="image path">

Password reset over HTTP
SSTI Injection and Hyperlink Injection 
```

---

## 3️⃣ Edit User Settings & Invite Function

While testing **user settings and invite features**, I check the following:

- **CSRF** leading to account takeover  

- **Email Update Issues**
  - Updating email address to an existing user’s email  
  - Using **Unicode characters** to bypass email uniqueness  

- **SQL Injection**
  - Sending POST request to `sqlmap`  

- **Blind XSS**
  - Editing username with Blind XSS payload  
  - Payload executes when admin visits the user page  

- **Auto User Creation**

- **User Limit Bypass**
  - Using race condition techniques  

- **IDOR Testing**
  1. Normal user accesses admin page via response manipulation  
  2. Copy ID from URL and modify data  
  3. Change ID parameter to edit or delete data  

- **Stored XSS Testing**

- **SSTI Injection Testing**

---

## 4️⃣ Cross-Site Request Forgery (CSRF)

CSRF testing includes the following checks:

- **Request Method Manipulation**
  - Changing request method from `POST` to `GET`

- **CSRF Token Handling**
  - Reusing CSRF token  
  - Deleting CSRF token  
  - Using CSRF token as an array:
    ```
    token[]=asdfhjiky
    ```

- **Token Validation**
  - Same-length token with different value  

- **Hidden Endpoint Discovery**
  - Searching for hidden endpoints:
    ```
    https://www.redacted.com/test/FUZZ
    ```
- **CSRF Impact Testing**
  - CSRF to delete user account  
  - CSRF to change user details  
  - CSRF on all sensitive forms
 
---

## 6️⃣ Open Redirect Testing

Open redirect testing includes the following steps:

- **Injection & Chaining**
  - CRLF injection leading to XSS  
  - XSS in login page leading to account takeover  
  - Facebook access token theft testing  

- **OAuth Abuse**
  - Open redirect to GitLab OAuth  

- **SSRF via Open Redirect**
  - SSRF attempts using open redirect:
    ```
    http://169.254.169.254/latest/meta-data/
    ```

- **Impact Testing**
  - Open redirect leading to OAuth token leakage  
  - Open redirect leading to XSS  

---

## 7️⃣ Broken Access Control Testing

Access control testing methodology includes:

- **Admin Feature Enumeration**
  - Browsing the application as admin and observing features:
    - Dashboard  
    - Upload / Download  
    - User Management  
    - Settings  

- **Unauthorized Access Testing**
  - Copying all admin URLs  
  - Attempting to access admin endpoints as a low-privileged user  

- **IDOR & Permission Testing**
  - Identifying ID parameters in CRUD operations:
    - Create  
    - Read  
    - Update  
    - Delete  

- **Authorization Analysis**
  - Analyzing and understanding the permission model
  
---

## 8️⃣ Stored XSS Testing

Stored XSS testing includes the following checks:

- **Input Field Testing**
  - Testing all input fields such as:
    - Name  
    - Email  
    - Address  
    - Chat  

- **Entry & Exit Point Identification**
  - Identifying where data is stored and rendered  

- **Payload Injection**
  - Injecting payload:
    ```html
    <img src=x onerror=alert(1)>
    ```

- **Malicious File Uploads**
  - Uploading malicious files:
    - GIF  
    - SVG  
    - PNG  

---

## 9️⃣ SQL Injection in XML Parsing

XML-based testing includes:

- Checking SQL Injection in XML parsing data  
- Inspecting request headers  
- **Time-based testing**
  ```text
  sleep(5)


