## Overview
Applied NIST Cybersecurity Framework 2.0 to my personal IT environment 
as a hands-on learning project — identifying 50 assets across hardware, 
accounts, and data, and documenting gaps to remediate.

## Motivation
As a first-year cybersecurity student targeting security governance roles, 
I wanted to move beyond textbook study of the CSF and actually apply it 
to something concrete. My own IT environment turned out to be a rich 
case study — with real Single Points of Failure, unmanaged assets, and 
network segmentation gaps.

## Framework
- **NIST CSF 2.0** (Framework Core: Govern, Identify, Protect, Detect, Respond, Recover)
- **CIA Triad** (Confidentiality, Integrity, Availability) for asset valuation

## Progress
- ✅ Layer 1-3 asset inventory (60 assets identified)
- ⬜ Current state assessment (Protect, Detect, Respond, Recover)
- ⬜ Remediation implementation
- ⬜ Governance policy documentation

## Key Findings (Phase 1)
1. iPhone as Single Point of Failure (Apple Pay + 2FA + Apple ID hub)
2. Apple ID lacks 2FA and recovery contact
3. SMS 2FA foundation vulnerable to SIM swap
4. Obsidian career vault has no backup or version control
5. Shared Wi-Fi with no VPN or network segmentation

See [01-asset-inventory.md](./01-asset-inventory.md) for full details.
