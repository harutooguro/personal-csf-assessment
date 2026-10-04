# Remediation Plan

## Overview

This document outlines the planned remediation activities to address the 
138 gaps identified in `02-current-state-assessment.xlsx` across the 
Protect (PR) and Detect (DE) functions of NIST CSF 2.0.

Rather than treating each gap as an isolated technical fix, this plan 
groups actions by the six Key Findings (F1-F6) identified during 
assessment, so that structural root causes are addressed rather than 
only their symptoms.

## Methodology

### Prioritization

Actions are prioritized along two dimensions:

1. **Finding severity** — Which Key Finding does the gap belong to?
2. **Asset priority** — Critical / High / Medium / Low (CIA-weighted)

### Phasing

- **Phase 1 (Immediate, Week 1)**: Actions requiring no cost, no new 
  tooling, and no coordination with third parties. "Flip a switch" 
  level changes.
- **Phase 2 (Short-term, Month 1)**: Actions requiring new tools, 
  account changes, or structural setup (backup systems, VPN selection).
- **Phase 3 (Long-term, Quarter 1)**: Operational routines, periodic 
  reviews, and governance processes.

## Phase 1: Immediate Actions (Week 1)

Target: Close the most dangerous gaps that require no cost or new tooling.

### Finding F1 — iPhone as Single Point of Failure

| Action | Asset | CSF Subcategory | Effort | Status |
|---|---|---|---|---|
| Enable Find My iPhone | iPhone 14 | DE.CM-02 | 2 min | Pending |
| Verify Stolen Device Protection remains ON | iPhone 14 | PR.AA-03 | 1 min | Verified |
| Document dependency list (which accounts rely on iPhone 2FA) | iPhone 14 | DE.AE-04 | 30 min | Pending |

### Finding F2 — Apple ID lacks recovery configuration

| Action | Asset | CSF Subcategory | Effort | Status |
|---|---|---|---|---|
| Verify trusted recovery phone number | Apple ID | PR.AA-01 | 5 min | Pending |
| Configure Recovery Contact (family member) | Apple ID | PR.AA-01 | 10 min | Pending |
| Generate and store Recovery Key offline | Apple ID | PR.AA-01 | 15 min | Pending |

### Finding F3 — SIM Swap vulnerability

| Action | Asset | CSF Subcategory | Effort | Status |
|---|---|---|---|---|
| Set carrier account PIN | Mobile carrier | PR.AA-01 | 10 min | Pending |
| Enable number-lock / port-out protection | Mint Mobile | PR.AA-03 | 10 min | Pending |
| Enable SIM PIN on iPhone | eSIM profile | PR.PS-01 | 5 min | Pending |

### Finding F4 — Obsidian vault has no backup

| Action | Asset | CSF Subcategory | Effort | Status |
|---|---|---|---|---|
| Create private GitHub repo for vault backup | Obsidian vault | PR.DS-11 | 20 min | Pending |
| Initial git commit + push | Obsidian vault | PR.DS-11 | 10 min | Pending |
| Test restore from GitHub (dry-run on separate folder) | Obsidian vault | PR.IR / RC.RP | 15 min | Pending |

### Finding F6 — Password reuse across critical identity accounts

| Action | Asset | CSF Subcategory | Effort | Status |
|---|---|---|---|---|
| Change Google Account to unique 16+ char password | Google Account | PR.AA-01 | 5 min | Pending |
| Store in password manager | Google Account | PR.AA-01 | 2 min | Pending |
| Audit other reused passwords via password manager report | All accounts | PR.AA-01 | 30 min | Pending |

### Cross-Finding: Low-effort quick wins

| Action | Asset | CSF Subcategory | Effort | Status |
|---|---|---|---|---|
| Enable  Chase Bank alerts | Primary US bank | DE.CM-03 | 3 min | Pending |
| Save Google Account backup codes offline | Google Account | PR.AA-01 | 5 min | Pending |

**Phase 1 estimated total time: ~3 hours**

---

## Phase 2: Short-term Actions (Month 1)

Target: Address structural root causes that need new tooling or setup.

### Finding F4 — Backup strategy (expanded)

- Set up Time Machine on an external encrypted drive for MacBook
  - CSF: PR.DS-11, RC.RP-01
  - Dependency: Need to acquire external drive (~$50)
- Verify iCloud Backup restore from iPhone (dry-run)
  - CSF: PR.DS-11

### Finding F5 — Shared Wi-Fi mitigation

- Select and subscribe to a trusted VPN service
  - Candidates to evaluate: Mullvad, ProtonVPN, iCloud Private Relay
  - CSF: PR.DS-02
- Configure VPN on MacBook and iPhone
  - CSF: PR.DS-02
- Verify DNS resolution integrity (encrypted DNS)
  - CSF: PR.DS-02

### MacBook hardening

- Create separate standard user account for daily use; keep admin 
  account for installs only
  - CSF: PR.AA-05
- Verify FileVault recovery key is stored offline (not only iCloud)
  - CSF: PR.DS-01
- Verify Gatekeeper, SIP, and Firewall Stealth Mode settings
  - CSF: PR.PS-01, PR.IR-01

### Detection improvements

- Enable login alerts on all financial accounts (Chase, Wise, cards)
  - CSF: DE.CM-03
- Register primary email at Have I Been Pwned
  - CSF: DE.CM-06
- Review connected third-party apps on Google Account
  - CSF: PR.AA-05

**Phase 2 estimated total time: ~6 hours spread over the month**

---

## Phase 3: Long-term Actions (Quarter 1)

Target: Establish operational governance so that this assessment does 
not become stale.

### Quarterly review cadence

- **Monthly**: Verify Time Machine backup is current; review login 
  alerts and security notifications
- **Quarterly**: Re-run password manager audit; review trusted 
  devices on Apple ID and Google Account; review Mint Mobile account 
  activity
- **Semi-annually**: Re-assess full CSF Protect / Detect matrix; 
  update this document

### Policy artifact

- Document personal security policy as a living artifact 
  (`personal-security-policy.md`)
- Define new-service onboarding checklist (2FA requirement, 
  password manager entry, etc.)
- Define incident response playbook (what to do if iPhone / Apple ID 
  / Google Account is compromised)

### Residual risks accepted

- Home Wi-Fi remains landlord-controlled; mitigated via endpoint 
  controls and VPN
- Microsoft 365 (institution-provided) remains outside personal 
  governance scope; treated as third-party dependency
- Some low-priority accounts (TryHackMe, Duolingo, etc.) will not 
  receive full assessment given marginal risk

---

## Summary Table

| Phase | Timeframe | Actions | Effort | Addresses |
|---|---|---|---|---|
| Phase 1 | Week 1 | 17 immediate actions | ~3 hours | F1, F2, F3, F4 (initial), F6 |
| Phase 2 | Month 1 | 12 structural actions | ~6 hours | F4 (full), F5, hardening |
| Phase 3 | Quarter 1 | Governance routines | Ongoing | All findings (sustaining) |

## Next Steps

- Execute Phase 1 within one week of plan publication
- Track completion by updating `Status` column
- Re-measure Coverage % after Phase 1 and Phase 2 completion to 
  demonstrate improvement
