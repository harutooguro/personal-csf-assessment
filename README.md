# Personal IT Environment Assessment Using NIST CSF 2.0

A self-directed cybersecurity portfolio project applying the NIST 
Cybersecurity Framework 2.0 to assess, document, and remediate the 
security posture of my own personal IT environment.

**Author:** Haruto Oguro (Ensign College, Cybersecurity direction)  
**Period:** September – October 2026  
**Status:** Phase 1 complete; Phase 2 remediation in progress

## Why this project

As a first-year cybersecurity student targeting security governance 
roles, I wanted to move beyond textbook study of CSF 2.0 and apply 
it to something concrete. My own IT environment turned out to be a 
rich case study — with real Single Points of Failure, unmanaged 
assets, password reuse, and network segmentation gaps that mirror 
problems organizations face at larger scale.

## Framework and method

- **NIST CSF 2.0** — Framework Core (Govern, Identify, Protect, 
  Detect, Respond, Recover) used as the structural backbone.
- **CIA Triad** (Confidentiality, Integrity, Availability) used to 
  valuate each asset and derive priority.
- **ISO/IEC 27001 concepts** — ISMS thinking (PDCA cycle, Annex A 
  control categories, residual risk acceptance) applied as 
  governance overlay.

## Deliverables

| File | Function | Content |
|---|---|---|
| `01-asset-inventory.md` | Identify | 62 assets catalogued across hardware, accounts, and data, with CIA-based prioritization |
| `02-current-state-assessment-v2.xlsx` | Protect + Detect | Matrix evaluation of 47 critical/high-priority assets against 13 CSF subcategories; 217 applicable controls, 138 gaps identified |
| `03-remediation-plan.md` | Respond | Phased remediation plan (Immediate / Short-term / Long-term) organized around 6 Key Findings |
| `personal-security-policy.md` | Govern | Personal information security policy covering credential, data, network, and incident response rules; semi-annual review cadence |

## Key Findings

Six structural findings emerged from the assessment:

1. **iPhone as Single Point of Failure** — Apple Pay (5 cards) + 
   primary 2FA device + Apple ID hub converge on one device.
2. **Apple ID lacks recovery configuration** — Controls all Apple 
   devices and Apple Pay, but Recovery Contact and Recovery Key 
   are not configured.
3. **SIM swap vulnerability** — Mobile carrier account lacks PIN 
   and port-out protection; SMS 2FA remains in use for some 
   services.
4. **Obsidian career vault has no backup** — Local-only with no 
   version control or cloud sync; single point of permanent data 
   loss.
5. **Shared Wi-Fi without network segmentation** — Home network 
   is landlord-provided and shared with roommates; no VPN.
6. **Password reuse across critical identity accounts** — Apple ID 
   and Google Account previously shared credentials with other 
   services.

## Assessment coverage

- Protect function: 147 applicable controls, 65% coverage
- Detect function: 70 applicable controls, 46% coverage
- Overall: 217 applicable controls, 59% coverage

The gap between Protect and Detect coverage (65% vs 46%) is itself 
a finding: individual environments tend to prioritize prevention 
over detection, mirroring a pattern that emerging organizations 
also face.

## What I learned

- **CSF Govern function is harder than it looks.** Writing a 
  policy that is lightweight enough to actually follow, but 
  specific enough to be enforceable, requires real tradeoffs.
- **Residual risk acceptance is unavoidable.** Treating shared 
  Wi-Fi and institution-provided SaaS as third-party dependencies 
  — rather than trying to eliminate them — made the plan realistic.
- **Assets you did not know you had are your biggest risk.** The 
  inventory phase surfaced 20+ accounts I had forgotten I owned.

## Next phase

- Execute Phase 1 remediation actions (Week 1)
- Re-measure coverage after Phase 1 and Phase 2
- Semi-annual review scheduled for 2027-04

## About this project

This project was produced as part of my application preparation for 
the Reazon Holdings 2027 summer security internship. It is my attempt 
to answer the question: "what would it look like to actually run an 
ISMS, at the smallest possible scale?"

Feedback and critique welcome via GitHub Issues.
