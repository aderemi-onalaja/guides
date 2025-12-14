# 🔐 Securing AI-Built Apps (Practical Checklist)

A practical security guide distilled from Prajwal Tomar’s experience building **45+ AI-powered MVPs**.  
Use this as a **baseline checklist** when shipping AI-generated or AI-assisted applications.

> ⚠️ AI speeds up development — it does **not** guarantee secure code.

---

## 📌 What This Repo Is

This is **not** a full security framework.  
It’s a **foundational checklist** to help solo builders, indie hackers, and small teams avoid common (and costly) mistakes when launching AI-built apps.

---

## 🛡️ Core Security Principles

### 1️⃣ Don’t Trust AI Blindly
AI tools (Cursor, Copilot, etc.) generate code fast — but often miss edge cases.

**Best practice**
- Use a second AI (e.g. CodeRabbit) to review AI-generated code
- Treat AI output like junior-level code that still needs review

---

### 2️⃣ Add Rate Limiting Early
Unprotected endpoints = bot abuse + unexpected cloud bills.

**Best practice**
- Start strict (e.g. `100 requests/hour per IP`)
- Adjust limits as usage patterns become clear

---

### 3️⃣ Enforce Row Level Security (RLS)
One of the most common SaaS data-leak mistakes.

**Best practice**
- Ensure users can only access their own data
- Manually test queries as different users
- Never rely on frontend filtering alone

---

### 4️⃣ Protect Secrets & API Keys
Hard-coded secrets are one commit away from a breach.

**Best practice**
- Use environment variables or a secrets manager
- Rotate keys regularly (every 60–90 days)
- Scope keys to minimum required permissions

---

### 5️⃣ Add CAPTCHA Where It Matters
Stops spam, fake signups, and automated abuse.

**Best practice**
- Protect:
  - Sign-up
  - Login
  - Password reset
  - Contact forms
- Use lightweight CAPTCHA to avoid UX friction

---

### 6️⃣ Enforce HTTPS Everywhere
Plain HTTP exposes users to interception and tampering.

**Best practice**
- Redirect all traffic to HTTPS
- Use free SSL providers (e.g. Let’s Encrypt)
- Reject insecure requests at the server level

---

### 7️⃣ Sanitize & Validate All Inputs
Frontend validation is not security.

**Best practice**
- Validate inputs:
  - Client-side (UX)
  - Server-side (security)
- Sanitize user input to prevent:
  - SQL injection
  - XSS
  - Prompt injection (for AI apps)

---

### 8️⃣ Keep Dependencies Updated
Most vulnerabilities come from outdated libraries.

**Best practice**
- Enable Dependabot or Renovate
- Review and merge security patches promptly
- Remove unused dependencies

---

## ✅ Pre-Launch Checklist

- [ ] AI-generated code reviewed
- [ ] Rate limiting enabled
- [ ] Row Level Security tested
- [ ] Secrets stored securely
- [ ] CAPTCHA added to key flows
- [ ] HTTPS enforced
- [ ] Input validation implemented
- [ ] Dependencies audited & updated

---

## 🚀 Why This Matters

Security failures don’t just break apps — they break trust.

Fixing security **before launch** is:
- Cheaper
- Faster
- Less damaging to your reputation

---

## 📎 Source

Inspired by a thread from **Prajwal Tomar** on securing AI-built apps based on real MVP experience.

---

## 🧠 Reminder

> Move fast — but don’t ship vulnerabilities faster.
