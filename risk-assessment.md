# Risk Assessment
> PayGuard's greatest threat isn't an external attacker
> breaking through the perimeter. It's a developer logging
> raw payment data "just for debugging."

---

## Table of Contents
- [Executive Summary](#executive-summary)
- [Methodology](#methodology)
- [Threat Identification](#threat-identification)
- [Vulnerability Identification](#vulnerability-identification)
- [Risk Scoring](#risk-scoring)
- [Risk Priority Summary](#risk-priority-summary)
- [Contact](#contact)

---

## Executive Summary

This risk assessment applies NIST 800-30 methodology to PayGuard's
payment processing environment — with particular attention to the
human behavior patterns that determine whether PCI DSS controls
work in practice.

PayGuard's technical security posture is stronger than OccuSafe's
— tokenization is in place, network segmentation exists, and a
prior SAQ was completed. But three unresolved issues create
significant audit risk: an overdue penetration test, an unresolved
logging gap, and a developer culture that routinely bypasses change
management controls.

---

## Methodology

**Framework:** NIST 800-30 — Guide for Conducting Risk Assessments

**Risk scoring:** Likelihood × Exposure × Impact

**Risk levels:**

| Score | Risk Level | Action |
|-------|-----------|--------|
| Very High | Immediate remediation required | Stop / contain |
| High | Remediation within 30 days | Priority action |
| Moderate | Remediation within 90 days | Planned action |
| Low | Monitor | Ongoing awareness |

**Finding sources:**

| Source | Findings generated |
|--------|-------------------|
| Prior SAQ findings | Unresolved logging gap — 18 months open |
| Stakeholder interviews | Engineering bypass behavior, CFO cost concerns |
| Infrastructure review | Penetration test overdue, segmentation unverified |
| Documentation review | Change management gaps, debug log risk |
| Threat intelligence | Payment platform attack patterns — skimming, API abuse |

---

## Threat Identification

**Five threat categories identified for PayGuard's environment.**

### Threat 1: Inadvertent PAN Capture in Developer Logs

| Element | Detail |
|---------|--------|
| **Threat source** | Developers logging raw API request/response data for debugging |
| **Threat event** | PANs captured in plain text in application or system logs |
| **Why it's the highest priority** | Silent and pervasive — developers don't realize they're storing card data; logs may persist indefinitely; discovered only during audit or breach investigation |
| **Human behavior angle** | Logging raw data is the path of least resistance for debugging — friction of sanitizing logs feels unnecessary until it causes a breach |
| **Affected assets** | Application logs, system logs, debug logs, CloudWatch logs |

---

### Threat 2: CDE Network Segmentation Failure

| Element | Detail |
|---------|--------|
| **Threat source** | Misconfigured network controls, unverified segmentation boundaries |
| **Threat event** | Non-CDE systems gain access to CDE — expanding attack surface dramatically |
| **Why it's critical** | Segmentation not independently verified in 24 months; if segmentation fails, entire network is in PCI DSS scope |
| **Human behavior angle** | Engineers add network connections for convenience without security review — each connection potentially collapses the CDE boundary |
| **Affected assets** | CDE network segment, payment processing API, transaction database |

---

### Threat 3: Unauthorized CDE Access — Shared Service Accounts

| Element | Detail |
|---------|--------|
| **Threat source** | Shared service accounts without MFA used by engineering team |
| **Threat event** | Single compromised credential provides full CDE access — no individual accountability |
| **Why it's high priority** | PCI DSS Requirement 8 requires unique IDs for all users; shared accounts violate this requirement and eliminate audit trail integrity |
| **Human behavior angle** | Shared accounts reduce friction for team collaboration — individual accounts with MFA feel slower |
| **Affected assets** | CDE access credentials, transaction database, payment processing API |

---

### Threat 4: Uncontrolled Production Changes

| Element | Detail |
|---------|--------|
| **Threat source** | Head of Engineering bypassing change management for emergency deployments |
| **Threat event** | Unreviewed code change introduces vulnerability into production CDE |
| **Why it's high priority** | PCI DSS Requirement 6 requires formal change management; bypass behavior is documented and cultural — not occasional |
| **Human behavior angle** | Change management process is perceived as a deployment blocker — bypass is the rational choice under deadline pressure |
| **Affected assets** | Payment processing API, source code repository, CDE integrity |

---

### Threat 5: External Attack — Payment Platform Targeting

| Element | Detail |
|---------|--------|
| **Threat source** | Sophisticated external attackers — skimming groups, ransomware operators, API abuse |
| **Threat event** | Breach of payment processing API or transaction database — mass cardholder data exposure |
| **Why it's elevated** | Payment platforms are high-value targets; $2.4B payment volume makes PayGuard attractive; penetration test overdue means current vulnerabilities are unknown |
| **Human behavior angle** | Security team of 2 is understaffed for the threat surface — alert fatigue and prioritization gaps are inevitable |
| **Affected assets** | Payment processing API, transaction database, customer trust |

---

## Vulnerability Identification

| Vulnerability | Type | Threat category | Severity |
|---------------|------|----------------|----------|
| Debug logs not audited for PAN capture | Technical | PAN capture | Critical |
| Penetration test overdue 12 months | Process | External attack | Critical |
| CDE segmentation unverified 24 months | Technical | Segmentation failure | Critical |
| Logging gaps in CDE — unresolved 18 months | Technical | All categories | Critical |
| Shared service accounts in CDE | Technical | Unauthorized access | Critical |
| MFA not enforced on all CDE access | Technical | Unauthorized access | Critical |
| Change management bypassed regularly | Process | Uncontrolled changes | High |
| No compensating controls for bypass behavior | Process | Uncontrolled changes | High |
| Stripe BAA and PCI compliance not verified | Process | Third-party risk | High |
| Security team understaffed for threat surface | Organizational | All categories | High |
| Customer dashboard CDE connection unreviewed | Technical | Segmentation failure | High |
| No formal developer security training | People | PAN capture | High |
| Emergency change procedure not documented | Process | Uncontrolled changes | Moderate |
| CloudWatch log retention policy undefined | Technical | Log integrity | Moderate |

---

## Risk Scoring

| Risk | Likelihood | Exposure | Impact | Risk Level |
|------|-----------|---------|--------|-----------|
| PAN capture in debug logs | High | High | Very High | **Very High** |
| CDE segmentation failure | Moderate | High | Very High | **Very High** |
| Shared accounts — CDE breach | High | High | Very High | **Very High** |
| Uncontrolled production change | High | High | High | **Very High** |
| External attack — overdue pentest | Moderate | High | Very High | **High** |
| Stripe compliance unverified | Low | High | Very High | **High** |
| Developer security training absent | High | High | Moderate | **High** |
| Log retention undefined | Moderate | High | Moderate | **Moderate** |

---

## Risk Priority Summary

**Four findings require immediate action before any other
remediation activity begins.**

| Priority | Finding | Rationale |
|----------|---------|-----------|
| 1 | Audit all logs for PAN capture — sanitize immediately | Silent violation that may already exist — must be confirmed before QSA audit |
| 2 | Commission penetration test immediately | QSA cannot proceed without current pentest results — 8-month deadline |
| 3 | Verify CDE network segmentation independently | Assumed segmentation is not compliant segmentation |
| 4 | Eliminate shared service accounts — enforce individual IDs + MFA | PCI DSS Requirement 8 violation — QSA will flag immediately |

*Full gap analysis and remediation roadmap in subsequent documents.*

---

## Contact

**Dara Thomas** — GRC Analyst & Consultant | Human-Centered Risk & Compliance

[LinkedIn](YOUR_LINKEDIN_URL) · dara.thomas.grc@gmail.com · [GitHub Portfolio](https://github.com/DaraStaysCurious)

---

*Part of the [grc-payguard-pcidss](../README.md) repository.*
*Next: [pci-dss-gap-analysis.md](pci-dss-gap-analysis.md)*
