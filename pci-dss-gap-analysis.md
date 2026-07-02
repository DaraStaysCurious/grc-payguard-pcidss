# PCI DSS v4.0 Gap Analysis
> All 12 requirements apply. There are no exclusions.
> The question is not whether PayGuard must comply —
> it's how far they have to go to get there.

---

## Table of Contents
- [Executive Summary](#executive-summary)
- [Gap Analysis Approach](#gap-analysis-approach)
- [Requirements 1-2 — Network Security](#requirements-1-2--network-security)
- [Requirements 3-4 — Cardholder Data Protection](#requirements-3-4--cardholder-data-protection)
- [Requirements 5-6 — Vulnerability Management](#requirements-5-6--vulnerability-management)
- [Requirements 7-8 — Access Control](#requirements-7-8--access-control)
- [Requirement 9 — Physical Security](#requirement-9--physical-security)
- [Requirements 10-11 — Logging and Testing](#requirements-10-11--logging-and-testing)
- [Requirement 12 — Security Policies](#requirement-12--security-policies)
- [Compliance Summary](#compliance-summary)
- [Contact](#contact)

---

## Executive Summary

PayGuard is partially compliant with PCI DSS v4.0. Tokenization
is in place, network segmentation exists, and basic security
controls are operational. However, four critical gaps will result
in immediate QSA findings if unresolved before the Level 1 audit:
an unresolved logging gap, an overdue penetration test, shared
service accounts in the CDE, and unaudited debug logs with
potential PAN capture.

**Compliance summary:**

| Status | Count | Percentage |
|--------|-------|-----------|
| ✅ Compliant | 4 | 33% |
| ⚠️ Partially compliant | 6 | 50% |
| ❌ Non-compliant | 2 | 17% |

---

## Gap Analysis Approach

**Three compliance determinations for each requirement:**

| Status | Definition |
|--------|-----------|
| ✅ Compliant | Fully implemented and independently verifiable |
| ⚠️ Partially compliant | Implemented but gaps remain — remediation required |
| ❌ Non-compliant | Not implemented — immediate action required |

---

## Requirements 1-2 — Network Security

### Requirement 1: Install and maintain network security controls

**Status: ⚠️ Partially compliant**

| Sub-requirement | Current state | Gap |
|----------------|---------------|-----|
| 1.1 — Network security control processes defined | Partial — informal | No formal network security policy documented |
| 1.2 — CDE network controls configured | AWS VPC in place | Configuration not formally reviewed or documented |
| 1.3 — Network access to CDE restricted | Partially implemented | Inbound/outbound rules not formally reviewed in 24 months |
| 1.4 — Network connections between trusted/untrusted networks controlled | Partial | Customer dashboard connection to CDE unreviewed |
| 1.5 — Security risks from connecting to untrusted networks mitigated | No policy | No remote access security policy for developers |

**Key gap:** CDE network segmentation assumed but not independently
verified. Customer dashboard connection creates potential CDE
boundary ambiguity.

---

### Requirement 2: Apply secure configurations

**Status: ⚠️ Partially compliant**

| Sub-requirement | Current state | Gap |
|----------------|---------------|-----|
| 2.1 — Processes for managing secure configurations defined | None | No configuration management process |
| 2.2 — System components configured and managed securely | Partial — informal | No formal configuration baselines documented |
| 2.3 — Wireless environments secured | N/A — AWS hosted | Not applicable |
| 2.4 — Inventory of system components maintained | Partial | Asset inventory completed — this engagement |
| 2.5 — Default passwords changed | Unknown | Not formally verified across all CDE components |
| 2.6 — Non-console administrative access secured | Partial | MFA not enforced on all administrative access |

---

## Requirements 3-4 — Cardholder Data Protection

### Requirement 3: Protect stored account data

**Status: ⚠️ Partially compliant**

| Sub-requirement | Current state | Gap |
|----------------|---------------|-----|
| 3.1 — Processes for protecting stored account data defined | None | No formal data retention and deletion policy |
| 3.2 — Storage of account data minimized | Stripe tokenization in place | PANs not stored in primary database |
| 3.3 — Sensitive authentication data not stored | Unknown | Debug logs not audited — potential CVV/PAN capture |
| 3.4 — PAN rendered unreadable | Tokenization via Stripe | PANs in Stripe vault — not in PayGuard database |
| 3.5 — Primary account numbers secured | Partial | Debug log audit required to confirm no plain text PANs |
| 3.6 — Cryptographic keys secured | Stripe manages — unverified | Stripe key management not formally reviewed |
| 3.7 — Key management policies defined | None | No formal cryptography or key management policy |

**Key gap:** Debug logs are the highest-risk unknown in this
requirement. Until audited, compliance with 3.3 and 3.5 cannot
be confirmed.

---

### Requirement 4: Protect cardholder data in transit

**Status: ✅ Compliant**

| Sub-requirement | Current state | Gap |
|----------------|---------------|-----|
| 4.1 — Processes for protecting data in transit defined | TLS implemented | Formal policy needed but controls in place |
| 4.2 — PANs protected during transmission | TLS 1.2+ enforced | No gaps identified |
| 4.3 — End-user messaging technologies secured | N/A | Not applicable to PayGuard's environment |

**Note:** Requirement 4 is PayGuard's strongest area — TLS
encryption is consistently implemented across all transmission
points. This is the only fully compliant requirement.

---

## Requirements 5-6 — Vulnerability Management

### Requirement 5: Protect all systems against malware

**Status: ⚠️ Partially compliant**

| Sub-requirement | Current state | Gap |
|----------------|---------------|-----|
| 5.1 — Processes for malware protection defined | Partial | No formal malware protection policy |
| 5.2 — Malware protection deployed | Basic endpoint protection | No EDR tooling — basic AV only |
| 5.3 — Anti-malware mechanisms active and monitored | Partial | No centralized monitoring of malware protection status |
| 5.4 — Phishing protections in place | Partial | Email filtering in place — no formal phishing simulation program |

---

### Requirement 6: Develop and maintain secure systems

**Status: ❌ Non-compliant**

| Sub-requirement | Current state | Gap |
|----------------|---------------|-----|
| 6.1 — Security vulnerabilities identified and managed | None | No vulnerability management program |
| 6.2 — Bespoke software developed securely | None | No secure development lifecycle |
| 6.3 — Web-facing applications protected | Partial — WAF in place | WAF rules not formally reviewed or updated |
| 6.4 — Public-facing web applications protected against attacks | Partial | No formal application security testing program |
| 6.5 — Changes to system components managed securely | ❌ Active violation | Change management bypassed regularly by engineering team |

**Key gap:** Requirement 6.5 is an active violation — not a
missing control. Change management bypass behavior is documented,
cultural, and ongoing. This will be a primary QSA finding.

---

## Requirements 7-8 — Access Control

### Requirement 7: Restrict access to system components

**Status: ⚠️ Partially compliant**

| Sub-requirement | Current state | Gap |
|----------------|---------------|-----|
| 7.1 — Processes for access control defined | None | No formal access control policy |
| 7.2 — Access to system components restricted | Partial | Role-based access partially implemented — not formally verified |
| 7.3 — Access to system components managed via access control system | Partial | No formal PAM solution in place |

---

### Requirement 8: Identify users and authenticate access

**Status: ❌ Non-compliant**

| Sub-requirement | Current state | Gap |
|----------------|---------------|-----|
| 8.1 — Processes for user identification defined | None | No formal identity management policy |
| 8.2 — User identification and authentication managed | ❌ Active violation | Shared service accounts in use — violates unique ID requirement |
| 8.3 — User authentication strengthened | ❌ Active violation | MFA not enforced on all CDE access |
| 8.4 — MFA implemented for all access to CDE | ❌ Active violation | Multiple CDE access points without MFA |
| 8.5 — Application and system accounts managed | None | No formal service account management program |
| 8.6 — System and application accounts managed | Partial | Service account inventory incomplete |

**Key gap:** Requirement 8 has three active violations —
shared accounts, missing MFA, and no identity management
policy. This is PayGuard's most non-compliant requirement
and will generate multiple QSA findings.

---

## Requirement 9 — Physical Security

### Requirement 9: Restrict physical access to cardholder data

**Status: ✅ Compliant**

| Sub-requirement | Current state | Gap |
|----------------|---------------|-----|
| 9.1 — Physical security controls defined | AWS responsible | AWS handles data center physical security |
| 9.2 — Physical access to CDE controlled | AWS responsible | Not applicable — cloud hosted |
| 9.3 — Physical access for personnel managed | Hybrid office | Basic physical access controls in place |
| 9.4 — Visitor access managed | N/A — remote first | Minimal physical office presence |
| 9.5 — Point-of-interaction devices protected | N/A | PayGuard doesn't manage physical payment terminals |

**Note:** Like OccuSafe, PayGuard's cloud-first architecture
means physical security requirements largely fall to AWS under
the shared responsibility model.

---

## Requirements 10-11 — Logging and Testing

### Requirement 10: Log and monitor all access

**Status: ⚠️ Partially compliant**

| Sub-requirement | Current state | Gap |
|----------------|---------------|-----|
| 10.1 — Logging processes defined | None | No formal logging policy |
| 10.2 — Audit logs implemented | Partial — CloudWatch | Logging gaps in CDE identified in prior SAQ — unresolved |
| 10.3 — Audit logs protected | Unknown | Log integrity controls not verified |
| 10.4 — Audit logs reviewed | None | No formal log review process |
| 10.5 — Audit log history retained | Undefined | No log retention policy defined |
| 10.6 — Time synchronization | Unknown | Clock synchronization not formally verified |
| 10.7 — Failures of security controls detected | None | No monitoring or alerting for control failures |

**Key gap:** The unresolved SAQ logging gap lives here —
Requirement 10.2. This is an 18-month open finding entering
a QSA audit. It will be the first thing a QSA examines.

---

### Requirement 11: Test security of systems and networks

**Status: ❌ Non-compliant**

| Sub-requirement | Current state | Gap |
|----------------|---------------|-----|
| 11.1 — Processes for security testing defined | None | No formal security testing program |
| 11.2 — Wireless access points managed | N/A — AWS hosted | Not applicable |
| 11.3 — External and internal vulnerabilities managed | None | No vulnerability scanning program |
| 11.4 — External and internal penetration testing | ❌ Overdue 12 months | Last pentest 24 months ago — QSA requires annual |
| 11.5 — Network intrusions and unexpected file changes detected | None | No IDS/IPS or file integrity monitoring |
| 11.6 — Unauthorized changes to payment pages detected | None | No change detection on customer-facing payment components |

**Key gap:** Requirement 11.4 is an immediate QSA blocker.
A QSA audit cannot proceed without current penetration test
results. This must be commissioned immediately.

---

## Requirement 12 — Security Policies

### Requirement 12: Support information security with policies

**Status: ✅ Compliant — Partial**

| Sub-requirement | Current state | Gap |
|----------------|---------------|-----|
| 12.1 — Information security policy defined | Partial — informal | No formal documented security policy |
| 12.2 — Acceptable use policies defined | None | No AUP for CDE systems |
| 12.3 — Risks identified, evaluated, managed | Completed — this engagement | No ongoing risk management process |
| 12.4 — PCI DSS compliance managed | SAQ completed | Transitioning to QSA — management process needs formalization |
| 12.5 — PCI DSS scope documented | Completed — this engagement | No prior formal scope documentation existed |
| 12.6 — Security awareness program | None | No security awareness training program |
| 12.7 — Personnel screened | Partial | No formal background screening for CDE-access roles |
| 12.8 — Third-party risks managed | None | Stripe compliance not formally verified and documented |
| 12.9 — Third-party service providers acknowledge responsibility | None | No formal acknowledgment from Stripe or other vendors |
| 12.10 — Incident response plan implemented | None | No incident response plan |

---

## Compliance Summary

**PayGuard PCI DSS v4.0 compliance at a glance:**

| Requirement | Topic | Status |
|-------------|-------|--------|
| 1 — Network security controls | Network architecture | ⚠️ Partial |
| 2 — Secure configurations | Configuration management | ⚠️ Partial |
| 3 — Protect stored data | Cardholder data storage | ⚠️ Partial |
| 4 — Protect data in transit | Encryption in transit | ✅ Compliant |
| 5 — Malware protection | Endpoint security | ⚠️ Partial |
| 6 — Secure development | SDLC and change management | ❌ Non-compliant |
| 7 — Restrict access | Access control | ⚠️ Partial |
| 8 — Identify and authenticate | Identity and MFA | ❌ Non-compliant |
| 9 — Physical security | Physical access | ✅ Compliant |
| 10 — Logging and monitoring | Audit logs | ⚠️ Partial |
| 11 — Security testing | Penetration testing | ❌ Non-compliant |
| 12 — Security policies | Policy framework | ⚠️ Partial |

**QSA audit blockers — must resolve before audit:**

| Blocker | Requirement | Timeline |
|---------|------------|---------|
| Commission penetration test | 11.4 | Immediately |
| Resolve CDE logging gaps | 10.2 | Within 30 days |
| Eliminate shared service accounts | 8.2 | Within 30 days |
| Enforce MFA on all CDE access | 8.3–8.4 | Within 30 days |
| Audit debug logs for PAN capture | 3.3, 3.5 | Within 30 days |
| Address change management bypass | 6.5 | Within 60 days |

---

## Contact

**Dara Thomas** — GRC Analyst & Consultant | Human-Centered Risk & Compliance

[LinkedIn](YOUR_LINKEDIN_URL) · dara.thomas.grc@gmail.com · [GitHub Portfolio](https://github.com/DaraStaysCurious)

---

*Part of the [grc-payguard-pcidss](../README.md) repository.*
*Next: [network-segmentation-review.md](network-segmentation-review.md)*
