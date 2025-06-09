# 🧪 Burp Lab Note: *Authentication bypass via flawed state machine*

## 🔹 Lab Metadata
- **Title**: Authentication bypass via flawed state machine
- **Category**: Business Logic
- **Difficulty**: Practitioner

---

## 🎯 Lab Objective
> _To find a flaw in the login process workflow and gain access to admin status and delete user `carlos`_

---

## 🧠 Application Logic Overview
- **Normal Workflow**:
  - Login page credentials -> click login -> Select role (User/Author) -> Account Page
- **Security Assumption**:
  - That the user will mandatorily fill the Role Selector
- **Exploration Strategy**:
  - I tried changing requests and through repeater while POST or GET /role-selector was still in transit. Chnaging the order of the requests being processed.

---

## 🔍 Observations
- **Endpoints Involved**: 
  - `POST /role-selector`, `GET /role-selector`, `GET /admin`
- **Interesting Behaviors**:
  - Discovered a /admin path in my audit selections, so directly tried path in browser and it said "only available if logged in as adminstrator". So if administrator is a user. I didn't think the order or role had to do with the vuln.
- **Useful Burp Tools**:
  - Proxy, Repeater, Scanner

---

## 🧨 Vulnerability Summary
- **Vulnerability Type**: Business Logic
- **Abused Logic**:
  - The site didn't know what to do if the Role Selector returned Null.
- **How It Was Abused**:
  - The GET request for Role Selector was dropped and I returned to home page.
- **Impact**:
  - The site gave me admin status by default.

---

## 🧪 Exploitation Steps
1. Login with valid credentials and intercept `GET /role-selector`
2. Drop the intercepted request
3. Navigate manually to `/` and it defaults to admin status
4. You now have admin access → delete `carlos`

---

## 🧰 Fix Suggestions
- Handle the error gracefully by defaulting to User Role. Or by rolling back the entire login.
- Role selection before session activation.

---

## ✍️ Notes & Reflections
- Subtle and fun — abusing what the app doesn't expect.
- Shows how skipping just *one* step in a workflow can break everything.
- Reinforces the value of manipulating flows, not just inputs.
