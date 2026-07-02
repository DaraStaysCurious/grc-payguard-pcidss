**Segmentation mechanism:** AWS VPC with security groups and
network ACLs controlling traffic between CDE and non-CDE segments.

**Third-party connection:** Stripe token vault — external
connection from CDE to Stripe's infrastructure for tokenization.

---

## Segmentation Verification Status

| Verification activity | Required frequency | Last performed | Status |
|-----------------------|-------------------|----------------|--------|
| Penetration test — segmentation validation | Annual | 24 months ago | ❌ Overdue |
| Firewall rule review | Every 6 months | Unknown | ❌ Unknown |
| Network ACL review | Every 6 months | Unknown | ❌ Unknown |
| Security group audit | Annual | Unknown | ❌ Unknown |
| CDE scope confirmation | Annual | 18 months ago (SAQ) | ⚠️ Outdated |

**Current segmentation assurance level: None.**
All verification activities are either overdue or status unknown.
PayGuard cannot currently demonstrate to a QSA that their CDE
boundary is intact.

---

## Identified Boundary Risks

### Risk 1: Customer Dashboard CDE Connection

| Element | Detail |
|---------|--------|
| **Issue** | Customer dashboard connects to financial reporting engine inside CDE |
| **Risk** | Dashboard may be creating an unintended path into the CDE from the non-CDE network |
| **Current state** | Connection exists — not formally reviewed or documented |
| **PCI DSS impact** | If dashboard is not properly isolated, it may expand CDE scope to include customer-facing systems |
| **Rating** | **High** |

**Required action:** Formally review and document the dashboard-
to-CDE connection. Determine whether dashboard should be
classified as in-scope for CDE. Implement compensating controls
if connection cannot be eliminated.

---

### Risk 2: Developer Workstation CDE Access

| Element | Detail |
|---------|--------|
| **Issue** | Developer workstations require CDE access for maintenance and troubleshooting |
| **Risk** | Workstations that connect to both CDE and external networks create potential bypass paths |
| **Current state** | No formal policy governing developer workstation security or CDE connection procedures |
| **PCI DSS impact** | Workstations without controls could bridge CDE to untrusted networks |
| **Rating** | **High** |

**Required action:** Implement formal developer workstation
security policy. Define approved CDE access procedures.
Verify workstations cannot bridge CDE to external networks.

---

### Risk 3: Stripe Token Vault External Connection

| Element | Detail |
|---------|--------|
| **Issue** | CDE connects to Stripe's infrastructure for token vault management |
| **Risk** | External connection from CDE must be formally controlled and documented |
| **Current state** | Connection exists — Stripe's PCI compliance not formally verified by PayGuard |
| **PCI DSS impact** | Third-party connections from CDE must be documented, controlled, and verified |
| **Rating** | **Moderate** |

**Required action:** Obtain and document Stripe's current PCI
DSS Attestation of Compliance (AOC). Formally document the
CDE-to-Stripe connection in network diagrams. Establish formal
third-party security monitoring.

---

## Compensating Controls

**Where full segmentation verification cannot be immediately
completed, compensating controls reduce exposure in the interim.**

| Gap | Compensating control | Limitation |
|-----|---------------------|-----------|
| Penetration test overdue | Enhanced log monitoring for CDE boundary anomalies | Monitoring detects — doesn't prevent boundary failures |
| Dashboard connection unreviewed | Restrict dashboard to read-only reporting data — no write access to CDE | Reduces scope risk but doesn't confirm boundary integrity |
| Developer workstation risk | Require VPN + MFA for all developer CDE access | Reduces unauthorized access risk — doesn't address bridging risk |

**Important:** Compensating controls do not satisfy PCI DSS
segmentation verification requirements. They reduce risk while
verification is being completed — not instead of it.

---

## Remediation Requirements

**Four actions required to achieve verified segmentation:**

| # | Action | Owner | Timeline | PCI DSS requirement |
|---|--------|-------|---------|-------------------|
| 1 | Commission penetration test — include segmentation validation | CTO | Immediately | 11.4 |
| 2 | Review and document customer dashboard CDE connection | Head of Engineering | 30 days | 1.3, 1.4 |
| 3 | Implement and document developer workstation CDE access policy | CTO | 30 days | 1.3, 12.2 |
| 4 | Obtain Stripe AOC and document third-party connection formally | GRC Analyst | 30 days | 12.8, 12.9 |

**Definition of done:**
Segmentation is verified when a qualified penetration tester
confirms — in writing — that no unauthorized paths exist between
the CDE and non-CDE networks, and that all identified boundary
risks have been remediated or formally accepted with documented
compensating controls.

---

## Contact

**Dara Thomas** — GRC Analyst & Consultant | Human-Centered Risk & Compliance

[LinkedIn](YOUR_LINKEDIN_URL) · dara.thomas.grc@gmail.com · [GitHub Portfolio](https://github.com/DaraStaysCurious)

---

*Part of the [grc-payguard-pcidss](../README.md) repository.*
*Next: [remediation-roadmap.md](remediation-roadmap.md)*
