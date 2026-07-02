# Remediation Roadmap
> PayGuard has 8 months before a mandatory QSA audit.
> Four findings will block the audit from proceeding.
> Those four get fixed first — everything else follows.

---

## Table of Contents
- [Executive Summary](#executive-summary)
- [Prioritization Framework](#prioritization-framework)
- [Phase 1 — QSA Blockers](#phase-1--qsa-blockers)
- [Phase 2 — Audit Readiness](#phase-2--audit-readiness)
- [Phase 3 — Sustained Compliance](#phase-3--sustained-compliance)
- [Full Remediation Table](#full-remediation-table)
- [Contact](#contact)

---

## Executive Summary

PayGuard has 24 findings requiring remediation before the Level 1
QSA audit. Unlike OccuSafe — which was building a security program
from scratch — PayGuard has a partial security foundation. The
remediation roadmap focuses on closing specific gaps rather than
building everything from zero.

**The critical constraint: 8 months to QSA audit readiness.**

**Remediation summary:**

| Phase | Timeline | Findings | Focus |
|-------|---------|---------|-------|
| Phase 1 — QSA Blockers | 0–30 days | 6 critical | Remove audit blockers |
| Phase 2 — Audit Readiness | 31–90 days | 12 high | Build compliance foundation |
| Phase 3 — Sustained Compliance | 91–180 days | 6 moderate | Formalize and verify |

---

## Prioritization Framework

**Two criteria drive sequencing:**

| Criterion | Definition |
|-----------|-----------|
| QSA blocker | Finding that will prevent audit from proceeding — fixed first regardless of effort |
| Effort vs. impact | Low effort + high impact addressed before high effort + low impact |

**Human behavior findings are prioritized alongside technical
findings** — because a technically compliant control that
developers route around is not a compliant control.

---

## Phase 1 — QSA Blockers
### 0–30 Days

**6 findings. All must be resolved before QSA audit can proceed.**

| # | Finding | Owner | Effort | PCI DSS req |
|---|---------|-------|--------|------------|
| 1 | Commission penetration test — include segmentation validation | CTO | High | 11.4 |
| 2 | Resolve CDE logging gaps — unresolved 18 months | Engineering Lead | Medium | 10.2 |
| 3 | Eliminate shared service accounts — enforce unique IDs | Engineering Lead | Medium | 8.2 |
| 4 | Enforce MFA on all CDE access points | Engineering Lead | Low | 8.3–8.4 |
| 5 | Audit all debug logs for PAN capture — sanitize immediately | Engineering Lead | Medium | 3.3, 3.5 |
| 6 | Review and document customer dashboard CDE connection | Head of Engineering | Medium | 1.3, 1.4 |

**Note on Finding 1:**
Penetration test must be commissioned immediately — results
take 2–4 weeks to receive. Delaying the commission delays
the entire audit timeline. This is the first action PayGuard
should take after receiving this assessment.

**Note on Finding 5:**
Debug log audit may reveal existing PAN capture. If PANs are
found in plain text logs — this becomes a reportable incident
under PCI DSS and potentially HIPAA if health data is also
present. Legal counsel must be involved before audit begins.

---

## Phase 2 — Audit Readiness
### 31–90 Days

**12 high-priority findings. Required for QSA audit readiness.**

| # | Finding | Owner | Effort | PCI DSS req |
|---|---------|-------|--------|------------|
| 7 | Establish formal change management process | CTO + Head of Engineering | High | 6.5 |
| 8 | Implement developer security training program | GRC Analyst + HR | Medium | 12.6 |
| 9 | Establish secure development lifecycle | Head of Engineering | High | 6.2 |
| 10 | Implement vulnerability scanning program | Engineering Lead | Medium | 11.3 |
| 11 | Establish formal network security policy | CTO | Low | 1.1 |
| 12 | Document and review firewall and ACL rules | Engineering Lead | Medium | 1.2, 1.3 |
| 13 | Implement formal access control policy | CTO | Low | 7.1 |
| 14 | Obtain Stripe AOC — document third-party connection | GRC Analyst | Low | 12.8, 12.9 |
| 15 | Implement developer workstation CDE access policy | CTO | Low | 1.3, 12.2 |
| 16 | Establish formal log review process | GRC Analyst | Medium | 10.4 |
| 17 | Define log retention policy | GRC Analyst + Legal | Low | 10.5 |
| 18 | Implement file integrity monitoring on CDE | Engineering Lead | Medium | 11.5 |

**Human behavior note on Finding 7:**
Change management bypass is cultural — not just a missing
process. The new change management process must be designed
with the engineering team, not handed down to them. A process
that adds more friction than the current bypass will be routed
around. Design for the workflow that actually exists.

---

## Phase 3 — Sustained Compliance
### 91–180 Days

**6 moderate findings. Required for sustained certification.**

| # | Finding | Owner | Effort | PCI DSS req |
|---|---------|-------|--------|------------|
| 19 | Implement formal cryptography and key management policy | CTO + Engineering | Medium | 3.6, 3.7 |
| 20 | Establish WAF rule review and update cadence | Engineering Lead | Low | 6.3 |
| 21 | Implement application security testing program | Engineering Lead | High | 6.4 |
| 22 | Establish formal background screening for CDE roles | HR | Low | 12.7 |
| 23 | Implement change detection on payment pages | Engineering Lead | Medium | 11.6 |
| 24 | Establish incident response plan | CTO + Legal | Medium | 12.10 |

---

## Full Remediation Table

**All 24 findings — sortable by phase, owner, and requirement:**

| # | Finding | Phase | Owner | Rating | PCI DSS |
|---|---------|-------|-------|--------|---------|
| 1 | Commission penetration test | 1 | CTO | Critical | 11.4 |
| 2 | Resolve CDE logging gaps | 1 | Engineering | Critical | 10.2 |
| 3 | Eliminate shared service accounts | 1 | Engineering | Critical | 8.2 |
| 4 | Enforce MFA on all CDE access | 1 | Engineering | Critical | 8.3–8.4 |
| 5 | Audit debug logs for PAN capture | 1 | Engineering | Critical | 3.3, 3.5 |
| 6 | Review dashboard CDE connection | 1 | Head of Eng | Critical | 1.3, 1.4 |
| 7 | Formal change management process | 2 | CTO + Eng | High | 6.5 |
| 8 | Developer security training | 2 | GRC + HR | High | 12.6 |
| 9 | Secure development lifecycle | 2 | Head of Eng | High | 6.2 |
| 10 | Vulnerability scanning program | 2 | Engineering | High | 11.3 |
| 11 | Formal network security policy | 2 | CTO | High | 1.1 |
| 12 | Firewall and ACL rule review | 2 | Engineering | High | 1.2, 1.3 |
| 13 | Formal access control policy | 2 | CTO | High | 7.1 |
| 14 | Obtain Stripe AOC | 2 | GRC Analyst | High | 12.8, 12.9 |
| 15 | Developer workstation policy | 2 | CTO | High | 1.3, 12.2 |
| 16 | Formal log review process | 2 | GRC Analyst | High | 10.4 |
| 17 | Log retention policy | 2 | GRC + Legal | High | 10.5 |
| 18 | File integrity monitoring | 2 | Engineering | High | 11.5 |
| 19 | Cryptography and key management policy | 3 | CTO + Eng | Moderate | 3.6, 3.7 |
| 20 | WAF rule review cadence | 3 | Engineering | Moderate | 6.3 |
| 21 | Application security testing | 3 | Engineering | Moderate | 6.4 |
| 22 | Background screening — CDE roles | 3 | HR | Moderate | 12.7 |
| 23 | Change detection — payment pages | 3 | Engineering | Moderate | 11.6 |
| 24 | Incident response plan | 3 | CTO + Legal | Moderate | 12.10 |

---

## Contact

**Dara Thomas** — GRC Analyst & Consultant | Human-Centered Risk & Compliance

[LinkedIn](YOUR_LINKEDIN_URL) · dara.thomas.grc@gmail.com · [GitHub Portfolio](https://github.com/DaraStaysCurious)

---

*Part of the [grc-payguard-pcidss](../README.md) repository.*
*Next: [executive-summary.md](executive-summary.md)*
