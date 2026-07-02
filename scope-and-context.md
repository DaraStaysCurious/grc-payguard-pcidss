# Scope and Context
> The Cardholder Data Environment is the perimeter that matters.
> Everything inside it must be hardened. Everything outside it
> must be isolated from it.

---

## Table of Contents
- [Company Profile](#company-profile)
- [PCI DSS Compliance Level](#pci-dss-compliance-level)
- [Cardholder Data Environment](#cardholder-data-environment)
- [Asset Inventory](#asset-inventory)
- [Data Classification](#data-classification)
- [Stakeholder Map](#stakeholder-map)
- [Assessment Constraints](#assessment-constraints)
- [Contact](#contact)

---

## Company Profile

**PayGuard Financial Technologies** — B2B SaaS embedded payment
processing and financial reporting platform. Clients embed
PayGuard's payment infrastructure directly into their own products.

| Attribute | Detail |
|-----------|--------|
| **Headquarters** | Austin, TX — hybrid workforce |
| **Employees** | 120 |
| **Customers** | 350 mid-market businesses |
| **Industries served** | E-commerce, SaaS, professional services |
| **Payment volume** | $2.4B annually |
| **Revenue** | $18M ARR — Series B, growing 55% YoY |
| **Infrastructure** | AWS — multi-region deployment |
| **Token vault** | Stripe — third-party tokenization |
| **Prior assessment** | SAQ D — completed 18 months ago |
| **Security team** | 2 people — one security engineer, one GRC analyst |

**Why this assessment now:**
PayGuard will cross the PCI DSS Level 1 threshold — 6M+
transactions annually — within 8 months. Level 1 requires a
mandatory annual QSA audit. PayGuard must be audit-ready before
that threshold is crossed.

**Prior finding:**
SAQ D completed 18 months ago identified logging gaps in the CDE.
Finding remains unresolved — will be flagged immediately in QSA
audit if not addressed.

---

## PCI DSS Compliance Level

**Understanding PayGuard's compliance obligations:**

| Level | Transaction volume | Requirement |
|-------|-------------------|-------------|
| Level 1 | 6M+ transactions/year | Annual QSA audit + quarterly network scans |
| **Level 2** | **1M–6M transactions/year** | **Annual SAQ + quarterly network scans** |
| Level 3 | 20K–1M transactions/year | Annual SAQ + quarterly network scans |
| Level 4 | < 20K transactions/year | Annual SAQ recommended |

**PayGuard is currently Level 2 — transitioning to Level 1
within 8 months.**

The transition from SAQ self-assessment to QSA audit is
significant. A QSA auditor will independently verify every
control — not just review self-reported compliance. The logging
gap that passed SAQ will not pass a QSA.

---

## Cardholder Data Environment

**The CDE is the most important concept in this assessment.**

PayGuard's CDE includes every system that stores, processes,
or transmits cardholder data — and every system connected to it.

**CDE components:**

| Component | Function | In CDE? |
|-----------|---------|---------|
| Payment processing API | Receives and processes card transactions | ✅ Yes |
| Token vault (Stripe) | Maps tokens to real PANs | ✅ Yes — third party |
| Transaction database (RDS) | Stores tokenized transaction records | ✅ Yes |
| Financial reporting engine | Generates revenue reconciliation reports | ✅ Yes |
| CDE network segment | Isolated network containing CDE systems | ✅ Yes |
| Developer workstations | Used to build and maintain CDE systems | ✅ Yes — in scope |
| Internal HR systems | Employee management | ❌ No — isolated |
| Marketing website | Public-facing website | ❌ No — isolated |
| Customer dashboard | Client reporting portal | ⚠️ Partial — connected to reporting engine |

**Network segmentation status:**
CDE is isolated via AWS VPC — separate from non-CDE systems.
Segmentation has not been independently verified or penetration
tested in 24 months. Segmentation effectiveness is assumed,
not confirmed.

---

## Asset Inventory

**Information assets ranked by criticality:**

| Asset | Type | Criticality | Primary concern |
|-------|------|------------|----------------|
| Payment processing API | System | Critical | Integrity + Availability |
| Token vault (Stripe) | Third-party system | Critical | Confidentiality + Integrity |
| Transaction database | Data | Critical | Confidentiality + Integrity |
| CDE network segment | Infrastructure | Critical | Availability + Integrity |
| Developer workstations | Endpoint | High | Confidentiality |
| Financial reporting engine | System | High | Integrity + Availability |
| CDE access credentials | Data | Critical | Confidentiality |
| Audit logs | Data | High | Integrity + Availability |
| Customer dashboard | System | High | Availability |
| Source code repository | System | High | Integrity |

---

## Data Classification

**Cardholder data classified by PCI DSS requirements:**

| Data element | Storage permitted? | Protection required |
|-------------|-------------------|-------------------|
| Primary Account Number (PAN) | Only if necessary — encrypted | Encryption + access controls + logging |
| Cardholder name | Yes | Access controls |
| Expiration date | Yes | Access controls |
| CVV/CVC | **Never** after authorization | Must not be stored |
| PIN/PIN block | **Never** | Must not be stored |
| Full magnetic stripe data | **Never** | Must not be stored |
| Transaction tokens | Yes — replaces PAN | Access controls + logging |

**Current state:** PayGuard uses Stripe tokenization — PANs are
not stored in PayGuard's database. However: developer debug logs
have not been audited for inadvertent PAN capture. This is a
known risk in payment platforms and a primary focus of this
assessment.

---

## Stakeholder Map

| Stakeholder | Role | Primary concern | Assessment relevance |
|-------------|------|----------------|---------------------|
| CEO | Executive sponsor | Audit timeline, enterprise growth | Risk appetite, resource authorization |
| CTO | Technical owner | Security architecture, audit readiness | CDE design, control implementation |
| CFO | Financial owner | Compliance cost, audit fees | Budget authorization for remediation |
| Head of Engineering | CDE owner | Developer workflow, deployment speed | Human behavior — friction vs. compliance |
| GRC Analyst (internal) | Assessment contact | Finding documentation, remediation tracking | Primary collaboration partner |
| Legal Counsel | Risk and liability | International expansion, regulatory exposure | Cross-border data handling requirements |

**Key finding from stakeholder interviews:**
The Head of Engineering prioritizes deployment speed — emergency
production changes bypass the change management process regularly.
This is documented as both a predisposing condition and a cultural
risk factor that affects control effectiveness across multiple
PCI DSS requirements.

---

## Assessment Constraints

| Constraint | Impact |
|------------|--------|
| 8-month Level 1 deadline | Remediation roadmap must be aggressive — no low-priority deferrals |
| Penetration test overdue 12 months | QSA will require current pentest before audit proceeds |
| Logging gap unresolved 18 months | Open finding from prior SAQ — elevated scrutiny in QSA |
| Head of Engineering bypass behavior | Change management controls at risk of being routed around |
| Stripe token vault — third party | Stripe's PCI compliance status must be verified and documented |
| Developer debug log risk | Logs may contain inadvertent PAN capture — requires audit |

---

## Contact

**Dara Thomas** — GRC Analyst & Consultant | Human-Centered Risk & Compliance

[LinkedIn](YOUR_LINKEDIN_URL) · dara.thomas.grc@gmail.com · [GitHub Portfolio](https://github.com/DaraStaysCurious)

---

*Part of the [grc-payguard-pcidss](../README.md) repository.*
*Next: [risk-assessment.md](risk-assessment.md)*
