# grc-payguard-pcidss
> Payment security controls fail when they create more friction
> than developers are willing to tolerate. This assessment
> measures both the technical gaps and the human ones.

---

## Table of Contents
- [Executive Summary](#executive-summary)
- [Why This Assessment Is Distinctive](#why-this-assessment-is-distinctive)
- [Scope and Frameworks](#scope-and-frameworks)
- [Repository Contents](#repository-contents)
- [Key Findings Preview](#key-findings-preview)
- [Contact](#contact)

---

## Executive Summary

PayGuard Financial Technologies processes $2.4B in annual payment
volume for 350 mid-market businesses. In 8 months they cross the
PCI DSS Level 1 threshold — triggering a mandatory QSA audit they
are not currently ready for.

This project documents a full PCI DSS v4.0 readiness assessment
with NIST 800-30 risk methodology applied throughout. The assessment
evaluates both technical compliance gaps and the human behavior
patterns that determine whether payment security controls work in
practice — or get routed around by developers under deadline
pressure.

---

## Why This Assessment Is Distinctive

**Most PCI DSS assessments measure whether controls exist.
This one also measures whether they work.**

Payment security controls fail in a specific and predictable way:
developers integrating payment APIs find workarounds when security
requirements create friction. The workaround becomes standard
practice. The control exists on paper and fails in production.

**The human behavior lens applied to payment security:**

| Control | Friction it creates | Common workaround | Actual risk |
|---------|--------------------|--------------------|------------|
| Tokenization requirement | Extra API calls slow integration | Logging raw PANs temporarily "for debugging" | PANs stored in plain text in logs |
| MFA on CDE access | Slows developer workflow | Shared service accounts without MFA | Single compromised credential = full CDE access |
| Change management process | Delays deployment pipeline | Direct production changes without review | Uncontrolled changes introduce vulnerabilities |
| Penetration testing requirement | Expensive and disruptive | Skipped or delayed | Vulnerabilities persist undetected |

**The thesis:** PCI DSS compliance that ignores developer behavior
is compliance theater. Durable payment security requires controls
designed around how engineering teams actually work.

---

## Scope and Frameworks

**Organization:** PayGuard Financial Technologies — 120 employees,
Austin TX, AWS multi-region, $2.4B annual payment volume

**Frameworks applied:**

| Framework | Purpose |
|-----------|---------|
| PCI DSS v4.0 | Primary compliance framework — 12 requirements |
| NIST 800-30 | Underlying risk assessment methodology |
| NIST CSF 2.0 | High-level security posture mapping |

**Data in scope:**

| Data type | Sensitivity | Primary concern |
|-----------|------------|----------------|
| Primary Account Numbers (PANs) | Critical | Must never be stored unencrypted |
| Cardholder names | High | Combined with PAN = usable fraud data |
| Expiration dates | High | Combined with PAN = usable fraud data |
| CVV/CVC codes | Critical | Must never be stored post-authorization |
| Authentication data | Critical | Must never be stored after authorization |
| Transaction records | High | Integrity + availability |

---

## Repository Contents

| Document | What it covers | Status |
|----------|---------------|--------|
| `README.md` | Project overview and assessment framing | ✅ Complete |
| [`scope-and-context.md`](scope-and-context.md) | Company profile, CDE definition, stakeholder map | ✅ Complete |
| [`risk-assessment.md`](risk-assessment.md) | NIST 800-30 threat and vulnerability analysis | ✅ Complete |
| [`pci-dss-gap-analysis.md`](pci-dss-gap-analysis.md) | All 12 PCI DSS v4.0 requirements assessed | ✅ Complete |
| [`network-segmentation-review.md`](network-segmentation-review.md) | CDE isolation analysis and compensating controls | ✅ Complete |
| [`remediation-roadmap.md`](remediation-roadmap.md) | Prioritized findings with effort/impact matrix | ✅ Complete |
| [`executive-summary.md`](executive-summary.md) | Board-ready one-pager — audit timeline and business case | ✅ Complete |

---

## Key Findings Preview

- **Critical:** Penetration test overdue by 12 months — QSA will
  flag immediately; Level 1 audit cannot proceed without current
  pentest results
- **Critical:** Logging gaps in CDE identified in prior SAQ —
  unresolved after 18 months; open finding entering QSA audit
- **High:** MFA not enforced on all CDE access points — shared
  service accounts in use by engineering team
- **High:** Change management process bypassed for emergency
  deployments — no compensating controls in place

*Full findings, risk scores, and remediation roadmap in the
documents above.*

---

## Contact

**Dara Thomas** — GRC Analyst & Consultant | Human-Centered Risk & Compliance

[LinkedIn](YOUR_LINKEDIN_URL) · dara.thomas.grc@gmail.com · [GitHub Portfolio](https://github.com/DaraStaysCurious)

---

*Part of the [DaraStaysCurious](https://github.com/DaraStaysCurious)
GRC & Cloud Security portfolio.*
*Methodology: [risk-assessment-methodology](https://github.com/DaraStaysCurious/risk-assessment-methodology)*
