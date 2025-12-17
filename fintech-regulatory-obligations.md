# Fintech & Payments Regulatory Obligations — Practical Breakdown

This document breaks down key regulatory obligations commonly referenced in fintech, payments, and card-processing architectures.  
The focus is on **what each regulation is**, **why it exists**, and **what it means in practice for product, data, and system design**.

---

## PCI DSS (Payment Card Industry Data Security Standard)

### What it is
A global security standard mandated by card schemes (Visa, Mastercard, Amex, etc.) for any system that **stores, processes, or transmits cardholder data**.

### Why it exists
To reduce card fraud by ensuring card data is handled, stored, and transmitted securely.

### Key concepts
- Cardholder Data Environment (CDE)
- PAN (Primary Account Number)
- Tokenisation
- Encryption at rest and in transit
- Least-privilege access

### Architectural implications
- Minimise PCI scope by **never storing raw PAN** where possible
- Use tokenisation services from PSPs or vault providers
- Segment PCI systems from non-PCI systems
- Enforce strong access controls and audit logging
- Regular vulnerability scans and penetration testing

### Common mistakes
- Logging PANs or CVVs
- Over-scoping environments unnecessarily
- Treating PCI as a one-time compliance exercise

---

## PSD2 (Payment Services Directive 2)

### What it is
An EU regulation governing electronic payments, open banking, and consumer protections.

### Why it exists
To increase competition, innovation, and security in payments while protecting consumers.

### Key concepts
- Strong Customer Authentication (SCA)
- Open Banking APIs
- Third-Party Providers (TPPs)
- Consent-based access

### Architectural implications
- Implement SCA flows (e.g. 2-factor authentication)
- Support API-based access for authorised TPPs
- Handle customer consent lifecycle securely
- Graceful fallbacks for SCA exemptions

### Common mistakes
- Treating SCA as purely a UX issue
- Poor consent revocation handling
- Weak API authentication/authorisation

---

## AML (Anti-Money Laundering)

### What it is
A collection of laws and regulations designed to prevent money laundering and financial crime.

### Why it exists
To stop illicit funds entering the financial system.

### Key concepts
- KYC (Know Your Customer)
- Transaction monitoring
- Risk scoring
- Suspicious Activity Reports (SARs)

### Architectural implications
- Integrate KYC providers (identity, sanctions, PEP checks)
- Build transaction monitoring pipelines
- Support manual review and escalation workflows
- Maintain immutable audit trails

### Common mistakes
- Static rules that don’t evolve
- Poor data quality for monitoring
- No clear separation between decisioning and execution

---

## GDPR (General Data Protection Regulation)

### What it is
EU data protection law governing the processing of personal data.

### Why it exists
To give individuals control over their personal data and how it is used.

### Key concepts
- Personal Data vs Sensitive Data
- Data minimisation
- Lawful basis for processing
- Right to access, rectify, and delete data

### Architectural implications
- Store only necessary personal data
- Support data deletion and export workflows
- Encrypt personal data
- Clear data lineage and ownership
- Strong access controls and logging

### Common mistakes
- Treating GDPR as just a privacy policy
- Hard-deleting data without auditability
- Poor separation between identifiers and transactional data

---

## Electronic Money Regulations (EMR)

### What it is
UK/EU regulations governing the issuance and management of electronic money.

### Why it exists
To ensure customer funds are protected and issuers operate safely.

### Key concepts
- E-money issuance
- Safeguarding of funds
- Segregation of customer money
- Redemption rights

### Architectural implications
- Clear separation between customer funds and operating funds
- Accurate ledgering and reconciliation
- Real-time or near-real-time balances
- Strong controls around fund movement

### Common mistakes
- Weak reconciliation processes
- Blurred ownership of balances
- Inconsistent ledger sources of truth

---

## Security-by-Design (Cross-Cutting Principle)

### What it is
A design philosophy where security is embedded from the start, not added later.

### Why it exists
Reactive security is expensive and risky in regulated environments.

### Key practices
- Threat modelling
- Zero-trust access
- Encryption by default
- Tokenisation over masking
- Defence in depth

### Architectural implications
- Design for breach scenarios
- Secure APIs and event streams
- Consistent secrets management
- Regular security reviews and audits

---

## Summary Table

| Regulation | Primary Focus | Architectural Impact |
|----------|--------------|----------------------|
| PCI DSS | Card data security | Tokenisation, segmentation |
| PSD2 | Payment security & open banking | SCA, APIs, consent |
| AML | Financial crime prevention | Monitoring, auditability |
| GDPR | Personal data protection | Data minimisation, access control |
| EMR | Customer fund protection | Ledger accuracy, safeguarding |

---

## Why This Matters for Fintech Architecture

Modern fintech platforms must:
- Balance **speed and innovation** with **regulatory rigor**
- Design systems that are **auditable, secure, and scalable**
- Treat compliance as a **product and architecture concern**, not just legal overhead

Well-designed systems reduce risk, cost, and time-to-market — while building trust with customers, partners, and regulators.
