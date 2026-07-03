# Executive Summary
> PayGuard has 8 months before a mandatory QSA audit.
> Four findings will block that audit from proceeding.
> This document tells you what they are and what to do about them.

---

## Table of Contents
- [Situation](#situation)
- [What We Found](#what-we-found)
- [What's At Risk](#whats-at-risk)
- [What Needs to Happen](#what-needs-to-happen)
- [The Path to Level 1 Certification](#the-path-to-level-1-certification)
- [Contact](#contact)

---

## Situation

PayGuard processes $2.4B in annual payment volume for 350
mid-market businesses. At current growth rates, PayGuard will
cross the PCI DSS Level 1 threshold — 6M+ transactions annually
— within 8 months. Level 1 triggers a mandatory annual audit by
a Qualified Security Assessor.

This assessment evaluated PayGuard's current PCI DSS v4.0
compliance posture. The finding: PayGuard is partially compliant.
Tokenization is in place, network segmentation exists, and basic
controls are operational. But four findings will block the QSA
audit from proceeding — and one of them must be commissioned
today.

---

## What We Found

**24 findings. 6 are QSA audit blockers.**

| Status | Count | Meaning |
|--------|-------|---------|
| Critical — QSA blockers | 6 | Audit cannot proceed without resolution |
| High — audit readiness | 12 | Required before QSA audit begins |
| Moderate — sustained compliance | 6 | Required for ongoing certification |

**The four most significant findings:**

| Finding | Why it matters |
|---------|---------------|
| Penetration test overdue 12 months | QSA cannot proceed without current pentest results — must be commissioned immediately |
| CDE logging gaps unresolved 18 months | Open finding from prior SAQ — first thing a QSA will examine |
| Shared service accounts in CDE | Active PCI DSS Requirement 8 violation — no individual accountability, no audit trail |
| Debug logs not audited for PAN capture | PANs may exist in plain text in application logs — silent violation that may already be reportable |

---

## What's At Risk

**Three categories of harm — in order of immediacy:**

**1. Audit failure**
A QSA audit that identifies the penetration test gap, the logging
gap, and the shared account violation will not certify PayGuard.
Failed certification at Level 1 means PayGuard cannot demonstrate
compliance to enterprise customers — and risks losing the ability
to process card payments through acquiring banks.

**2. Reportable incident**
If the debug log audit reveals PANs stored in plain text,
PayGuard has a reportable PCI DSS incident — regardless of
whether a breach occurred. Reporting triggers card brand
notification, potential fines, and forensic investigation.

**3. Revenue impact**
PayGuard has lost deals due to the absence of Level 1
certification. Every month the audit is delayed is a month
enterprise prospects choose compliant competitors. The cost
of remediation is significantly lower than the cost of
continued lost revenue.

---

## What Needs to Happen

**Six critical actions — the first one starts today:**

| Priority | Action | Owner | Timeline |
|----------|--------|-------|---------|
| 1 | Commission penetration test — include segmentation validation | CTO | Today |
| 2 | Audit all debug logs for PAN capture | Engineering Lead | This week |
| 3 | Resolve CDE logging gaps — 18-month open finding | Engineering Lead | 30 days |
| 4 | Eliminate shared service accounts — enforce unique IDs + MFA | Engineering Lead | 30 days |
| 5 | Review and document customer dashboard CDE connection | Head of Engineering | 30 days |
| 6 | Enforce MFA on all remaining CDE access points | Engineering Lead | 30 days |

*Full remediation roadmap with all 24 findings, owners,
timelines, and PCI DSS requirement mappings in
[remediation-roadmap.md](remediation-roadmap.md).*

---

## The Path to Level 1 Certification

**QSA audit readiness in 6 months — certification in 8.**

| Milestone | Timeline |
|-----------|---------|
| Penetration test commissioned | Week 1 |
| Penetration test results received | Week 3–5 |
| Phase 1 complete — 6 QSA blockers resolved | Month 1 |
| Phase 2 complete — 12 high findings resolved | Month 3 |
| Phase 3 complete — 6 moderate findings resolved | Month 6 |
| QSA audit — Stage 1 documentation review | Month 7 |
| QSA audit — Stage 2 implementation verification | Month 8 |
| PCI DSS Level 1 certification issued | Month 8 |

**The business case:**
PayGuard's average enterprise contract value in the embedded
payments space ranges from $100K–$500K annually. Level 1
certification removes the primary barrier to closing enterprise
deals. A single enterprise contract won as a result of
certification covers the entire cost of the compliance program.

**One additional note:**
The change management bypass behavior documented in this
assessment is a cultural risk that technical controls alone
will not fix. The Head of Engineering and engineering team
should be involved in designing the new change management
process — not just informed of it. Controls designed with
the people who must use them are more durable than controls
handed down for implementation.

*This note reflects the human-centered security methodology
documented in
[risk-assessment-methodology](https://github.com/DaraStaysCurious/risk-assessment-methodology).*

---

## Contact

**Dara Thomas** — GRC Analyst & Consultant | Human-Centered Risk & Compliance

[LinkedIn](YOUR_LINKEDIN_URL) · dara.thomas.grc@gmail.com · [GitHub Portfolio](https://github.com/DaraStaysCurious)

---

*Part of the [grc-payguard-pcidss](../README.md) repository.*
*Return to: [README.md](../README.md)*
