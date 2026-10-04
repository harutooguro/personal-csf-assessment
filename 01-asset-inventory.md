# 01 — Asset Inventory (NIST CSF 2.0 · Identify / ID.AM)

> **Scope:** Personal IT environment of a single individual (student)
> **Framework:** NIST Cybersecurity Framework 2.0 — Identify function, Asset Management category (ID.AM)
> **Assessment date:** September 2026
> **Status:** Current state (as-is). Remediation is tracked in later documents.

---

## Table of Contents

1. [Overview](#1-overview)
2. [Methodology](#2-methodology)
3. [Assessment Framework](#3-assessment-framework)
4. [Layer 1: Hardware](#4-layer-1-hardware)
5. [Layer 2: Accounts](#5-layer-2-accounts)
6. [Layer 3: Data](#6-layer-3-data)
7. [Overall Summary](#7-overall-summary)
8. [Key Findings](#8-key-findings)
9. [Next Steps](#9-next-steps)

---

## 1. Overview

### Purpose

This document is the first deliverable of a project that applies NIST CSF 2.0 to a personal IT environment. The goal is simple: **you cannot protect what you do not know you have.** Before evaluating controls, this inventory establishes a complete, prioritized list of the hardware, accounts, and data that make up my digital footprint.

Treating one person as a "small organization" is a deliberate exercise. The same questions an enterprise asks during asset management — *What do we own? Who controls it? What depends on what? What happens if it fails?* — apply directly, just at a smaller scale.

### Mapping to CSF 2.0 ID.AM

| CSF 2.0 Subcategory | Description | Where addressed |
|---|---|---|
| **ID.AM-01** | Inventories of hardware managed by the organization are maintained | [Layer 1: Hardware](#4-layer-1-hardware) |
| **ID.AM-02** | Inventories of software, services, and systems are maintained | [Layer 2: Accounts](#5-layer-2-accounts) |
| **ID.AM-03** | Representations of authorized network communication and data flows are maintained | Home network entry (H-05), [Key Finding 5](#finding-5-shared-network-with-no-transport-protection) |
| **ID.AM-04** | Inventories of services provided by suppliers are maintained | Third-party accounts in Layer 2 (financial, carrier, platforms) |
| **ID.AM-05** | Assets are prioritized based on classification, criticality, resources, and impact | [Assessment Framework](#3-assessment-framework) and priority column throughout |
| **ID.AM-07** | Inventories of data and corresponding metadata are maintained | [Layer 3: Data](#6-layer-3-data) |

### Public-disclosure note

This repository is public. To avoid turning the document into a reconnaissance aid, it follows these rules:

- No email addresses, usernames, account IDs, or phone numbers.
- Financial institutions, the mobile carrier, and specific organizations are described **by role**, not by name (e.g., "Primary US bank").
- Private project and client details are abstracted.
- Findings describe *categories* of weakness, not step-by-step exposure.

---

## 2. Methodology

Assets were discovered by working from several independent sources and cross-checking them, since no single source is complete.

| Source | What it revealed |
|---|---|
| **Password manager / browser saved logins** | The bulk of active online accounts |
| **Email search** (keywords such as "welcome", "verify your account", "receipt", "password reset") | Forgotten or dormant accounts not stored in the password manager |
| **Bank and card statements** | Paid subscriptions and payment-linked services |
| **Device settings** (Apple ID devices list, Wallet, connected apps) | Device-to-account relationships and payment dependencies |
| **2FA / authentication review** | Which accounts depend on SMS, which device receives codes |
| **File system walkthrough** (local folders, iCloud Drive, Google Drive) | Where sensitive data actually lives |
| **Physical walkthrough of home** | Identity documents and physical cards |

Each asset was then:

1. Assigned to a layer (Hardware / Accounts / Data) and subcategory.
2. Rated on Confidentiality, Integrity, and Availability.
3. Assigned an overall priority, adjusted for dependencies (see below).

**Known limitations:** Cloud storage contents (iCloud Drive, Google Drive) are listed at a summary level and still need a file-level inventory. Some secondary accounts have an unclear purpose and are flagged "to be reviewed."

---

## 3. Assessment Framework

### CIA Triad Ratings

Each asset is rated on the impact of losing each property.

| Property | Question asked | Low | Medium | High | Critical |
|---|---|---|---|---|---|
| **C** — Confidentiality | What if this were exposed? | Minor or no harm | Embarrassment, limited privacy loss | Financial loss, account takeover, significant privacy harm | Irreversible harm (e.g., identity theft using government IDs) |
| **I** — Integrity | What if this were altered without my knowledge? | Trivial to notice and fix | Inconvenient to correct | Wrong decisions, fraud, or reputational damage | Legal or identity consequences |
| **A** — Availability | What if I lost access to this? | Can live without it | Disruptive for days | Blocks study, work, or finances | — |

The **Critical** level is reserved for regulated identity data, where exposure cannot be "undone" by changing a password.

### Priority Classification

Priority is **not** a mechanical maximum of the CIA scores. It also considers **dependency and blast radius** — how many other assets fail if this one fails.

| Priority | Definition |
|---|---|
| 🔴 **Critical** | Compromise or loss causes direct financial loss, identity theft, or cascading compromise of other assets. Typically an authentication hub, financial account, or irreplaceable data. |
| 🟠 **High** | Compromise causes significant harm or disruption, but is contained to that asset or a small group of assets. |
| 🟡 **Medium** | Compromise is inconvenient or mildly harmful; recovery is straightforward. |
| 🟢 **Low** | Minimal impact; easy to recreate or abandon. |

> **Example of dependency-based adjustment:** The home Wi-Fi scores only Medium/Low/Medium on CIA, but it is rated **High** because I do not control it and every device's traffic passes through it.

---

## 4. Layer 1: Hardware

*CSF: ID.AM-01*

| ID | Asset | Description | C | I | A | Priority |
|---|---|---|---|---|---|---|
| H-01 | MacBook Air (M4) | Primary laptop; holds all work and study files | High | High | High | 🔴 Critical |
| H-02 | iPhone 14 | Primary phone; 2FA device for most accounts; Apple Pay wallet | High | High | High | 🔴 Critical |
| H-03 | iPad | Study device (note-taking, reading) | Medium | Medium | Medium | 🟡 Medium |
| H-04 | eSIM profile | Binds the phone number to the device; foundation of SMS-based 2FA | High | High | High | 🔴 Critical |
| H-05 | Home Wi-Fi network | Landlord-provided; password shared with roommates; router admin access status unknown. **Not controlled by me.** | Medium | Low | Medium | 🟠 High |

**Layer 1 subtotal:** 5 assets — 🔴 3 · 🟠 1 · 🟡 1 · 🟢 0

---

## 5. Layer 2: Accounts

*CSF: ID.AM-02 (services), ID.AM-04 (supplier-provided services)*

### 5.1 Financial (7)

| ID | Asset | Description | C | I | A | Priority |
|---|---|---|---|---|---|---|
| A-F01 | Primary US bank | Checking and savings; main US banking | High | High | High | 🔴 Critical |
| A-F02 | International transfer service | JP ↔ US transfers; stores bank details in both countries | High | High | High | 🔴 Critical |
| A-F03 | Credit card portal (×1) | US-issued credit card | High | High | Medium | 🔴 Critical |
| A-F04 | Debit card portals (×4) | US-issued debit cards | High | High | Medium | 🟠 High |
| A-F05 | Apple Pay | Holds all 5 payment cards; depends on a single iPhone | High | High | Medium | 🔴 Critical |
| A-F06 | P2P payment app | Linked to bank account | Medium | High | Medium | 🟠 High |
| A-F07 | Bank-integrated transfer service | Direct bank-to-bank transfers | Medium | High | Medium | 🟠 High |

### 5.2 Identity & Email (7)

| ID | Asset | Description | C | I | A | Priority |
|---|---|---|---|---|---|---|
| A-I01 | Gmail (primary) | Password-reset destination for most services | High | High | High | 🔴 Critical |
| A-I02 | Gmail (secondary) | Purpose to be reviewed | High | High | Medium | 🟠 High |
| A-I03 | College email | Institution-issued; official academic communication | High | Medium | High | 🟠 High |
| A-I04 | Outlook account | Purpose to be reviewed | Medium | Medium | Low | 🟡 Medium |
| A-I05 | Apple ID | Controls iPhone, iPad, MacBook, iCloud, and Apple Pay | High | High | High | 🔴 Critical |
| A-I06 | Google Account | Tied to primary Gmail; controls Drive, Photos, YouTube | High | High | High | 🔴 Critical |
| A-I07 | Microsoft 365 (institution-provided) | Managed by the college, not by me | Medium | Medium | Medium | 🟡 Medium |

### 5.3 Education & Learning (10)

| ID | Asset | Description | C | I | A | Priority |
|---|---|---|---|---|---|---|
| A-E01 | College student portal | Grades, enrollment, financial aid, transcripts | High | High | High | 🔴 Critical |
| A-E02 | Learning management system | Coursework and submissions | Medium | High | High | 🟠 High |
| A-E03 | English proficiency test account | Official test scores and score reporting | Medium | High | Low | 🟡 Medium |
| A-E04 | Programming learning platform | Beginner coding courses | Low | Low | Low | 🟢 Low |
| A-E05 | TryHackMe | Security learning progress | Low | Medium | Low | 🟢 Low |
| A-E06 | Language learning app | Casual practice | Low | Low | Low | 🟢 Low |
| A-E07 | ChatGPT | Conversation history may contain personal context | Medium | Low | Low | 🟡 Medium |
| A-E08 | Claude | Conversations include career strategy, resume drafts, project planning | Medium | Low | Low | 🟡 Medium |
| A-E09 | Gemini | Limited usage | Low | Low | Low | 🟢 Low |
| A-E10 | Notion (account) | Study notes; may contain career information | High | High | Medium | 🟠 High |

> The Notion **account** is listed here; the **data** it holds is evaluated separately in [Layer 3](#63-knowledge-bases), where it is rated higher.

### 5.4 Job Hunting & Professional (7)

| ID | Asset | Description | C | I | A | Priority |
|---|---|---|---|---|---|---|
| A-J01 | Job platform A (JP / bilingual) | Resume, personal information, applications | High | High | Medium | 🟠 High |
| A-J02 | Job platform B (JP) | Profile with career information | High | Medium | Medium | 🟠 High |
| A-J03 | Internship platform A | Application platform | High | High | Medium | 🟠 High |
| A-J04 | Internship platform B | Application platform | High | High | Medium | 🟠 High |
| A-J05 | LinkedIn | Public professional identity; US and JP networks | High | High | High | 🔴 Critical |
| A-J06 | GitHub | Hosts this project; future portfolio | High | High | High | 🔴 Critical |
| A-J07 | Zoom | Interview meetings; possible recording history | Medium | Low | Medium | 🟡 Medium |

### 5.5 Social Media (6)

| ID | Asset | Description | C | I | A | Priority |
|---|---|---|---|---|---|---|
| A-S01 | X (Twitter) | Public identity; direct messages | Medium | Medium | Low | 🟡 Medium |
| A-S02 | Instagram | Photos, direct messages, stories | Medium | Medium | Low | 🟡 Medium |
| A-S03 | Facebook | Legacy account; rarely used | Medium | Low | Low | 🟢 Low |
| A-S04 | LINE | Primary JP communication (family, friends); linked to phone number | High | High | Medium | 🟠 High |
| A-S05 | TikTok | Consumption only | Low | Low | Low | 🟢 Low |
| A-S06 | YouTube | Accessed through Google Account (A-I06) | Low | Low | Low | 🟢 Low |

> YouTube shares credentials with the Google Account. It is listed to keep the service inventory complete; its real risk is inherited from A-I06.

### 5.6 Utilities & Life Services (2)

| ID | Asset | Description | C | I | A | Priority |
|---|---|---|---|---|---|---|
| A-U01 | Mobile carrier account | Controls the phone number → SMS 2FA foundation; SIM-swap target | High | High | High | 🔴 Critical |
| A-U02 | Student health insurance | School-provided | Medium | Medium | Low | 🟡 Medium |

> H-04 (eSIM profile on the device) and A-U01 (carrier account) are related but distinct: one is the device-side binding, the other is the account that can **reassign** the number.

### 5.7 Entertainment & Shopping (1)

| ID | Asset | Description | C | I | A | Priority |
|---|---|---|---|---|---|---|
| A-X01 | Amazon | Purchase history, saved addresses, saved payment cards | Medium | Medium | Low | 🟡 Medium |

### Layer 2 Summary

| Subcategory | Count | 🔴 Critical | 🟠 High | 🟡 Medium | 🟢 Low |
|---|---|---|---|---|---|
| Financial | 7 | 4 | 3 | 0 | 0 |
| Identity & Email | 7 | 3 | 2 | 2 | 0 |
| Education & Learning | 10 | 1 | 2 | 3 | 4 |
| Job Hunting & Professional | 7 | 2 | 4 | 1 | 0 |
| Social Media | 6 | 0 | 1 | 2 | 3 |
| Utilities & Life Services | 2 | 1 | 0 | 1 | 0 |
| Entertainment & Shopping | 1 | 0 | 0 | 1 | 0 |
| **Total** | **40** | **11** | **12** | **10** | **7** |

---

## 6. Layer 3: Data

*CSF: ID.AM-07*

### 6.1 Data on MacBook (Local)

| ID | Asset | Description | C | I | A | Priority |
|---|---|---|---|---|---|---|
| D-L01 | Job-hunting materials | Resumes, application essays, motivation letters (multiple versions) | High | High | Medium | 🔴 Critical |
| D-L02 | Client project materials | Proposal and prototype code for an external project | High | Medium | Low | 🟠 High |
| D-L03 | Academic files | Coursework, notes, textbook PDFs | Medium | High | Medium | 🟠 High |
| D-L04 | Personal ID scans | Passport, visa, and SSN-related documents | **Critical** | **Critical** | Low | 🔴 Critical |
| D-L05 | Financial documents | Tax documents, bank statements | High | High | Low | 🟠 High |
| D-L06 | Development code | AI-assisted coding outputs, learning artifacts | Low | Medium | Low | 🟡 Medium |

### 6.2 Data in Cloud Storage

| ID | Asset | Description | C | I | A | Priority |
|---|---|---|---|---|---|---|
| D-C01 | iCloud Photos | Family and personal photos | High | Medium | Medium | 🟠 High |
| D-C02 | iCloud Drive files | File-level inventory pending | Medium | Medium | Medium | 🟡 Medium |
| D-C03 | Google Drive files | File-level inventory pending | Medium | Medium | Medium | 🟡 Medium |
| D-C04 | Video files | Personal video content | Low | Low | Low | 🟢 Low |

### 6.3 Knowledge Bases

| ID | Asset | Description | C | I | A | Priority |
|---|---|---|---|---|---|---|
| D-K01 | Obsidian career vault | Core career strategy notes. **Local only — no version control, no cloud sync.** | High | High | Medium | 🔴 Critical |
| D-K02 | Notion workspace (data) | Daily log, job-hunting notes, target company list, interview records (cloud-hosted) | High | High | Medium | 🔴 Critical |

### 6.4 Physical Assets

Physical assets are included because their digital copies (D-L04) and their physical originals share the same identity risk.

| ID | Asset | Storage / Handling | Priority |
|---|---|---|---|
| D-P01 | Passport | At home, secure storage | 🔴 Critical |
| D-P02 | Student status document (immigration-related) | At home, secure storage | 🔴 Critical |
| D-P03 | SSN-related documents | At home, secure storage | 🔴 Critical |
| D-P04 | Physical credit/debit cards | At home, rarely carried; Apple Pay used instead (✅ good practice) | 🟠 High |
| D-P05 | Student ID | At home or carried occasionally | 🟡 Medium |

### Layer 3 Summary

| Subcategory | Count | 🔴 Critical | 🟠 High | 🟡 Medium | 🟢 Low |
|---|---|---|---|---|---|
| Local (MacBook) | 6 | 2 | 3 | 1 | 0 |
| Cloud Storage | 4 | 0 | 1 | 2 | 1 |
| Knowledge Bases | 2 | 2 | 0 | 0 | 0 |
| Physical | 5 | 3 | 1 | 1 | 0 |
| **Total** | **17** | **7** | **5** | **4** | **1** |

---

## 7. Overall Summary

| Layer | Assets | 🔴 Critical | 🟠 High | 🟡 Medium | 🟢 Low |
|---|---|---|---|---|---|
| Layer 1: Hardware | 5 | 3 | 1 | 1 | 0 |
| Layer 2: Accounts | 40 | 11 | 12 | 10 | 7 |
| Layer 3: Data | 17 | 7 | 5 | 4 | 1 |
| **Total** | **62** | **21 (34%)** | **18 (29%)** | **15 (24%)** | **8 (13%)** |

### Observations

- **One in three assets is Critical.** This is higher than expected for an individual, and it is driven mostly by concentration: a small number of hubs (iPhone, Apple ID, primary Gmail, carrier account) sit upstream of many others.
- **Financial accounts are uniformly high-risk** (4 Critical, 3 High, nothing lower). Every payment path ultimately traces back to the same phone.
- **Low-priority assets are mostly learning and entertainment services.** These are candidates for consolidation or deletion to reduce attack surface.
- **Accounts outnumber everything else.** 40 of 62 assets (65%) are third-party services I do not operate — my security posture depends heavily on supplier controls I cannot see.

---

## 8. Key Findings

### Finding 1: iPhone as a Single Point of Failure

**Related assets:** H-02, A-F05, A-I05, A-U01 · **CSF:** ID.RA (Risk Assessment)

The iPhone is simultaneously:

- the **wallet** (Apple Pay holding all 5 payment cards),
- the **primary 2FA device** for most accounts, and
- the **entry point to the Apple ID** that controls every other Apple device and iCloud data.

**Why it matters:** A single stolen or compromised device — especially one stolen while unlocked — gives access to finances, authentication, and personal data at the same time. Losing the device also locks me out of the accounts I would need to recover from the loss. In enterprise terms, this is a concentration risk: too many critical functions depend on one component with no redundancy.

---

### Finding 2: Apple ID Protection Does Not Match Its Criticality

**Related assets:** A-I05, H-01, H-02, H-03, A-F05 · **CSF:** PR.AA-01 (Identity and credential management), PR.AA-03 (Authentication)

At the time of assessment, the Apple ID — the control point for all Apple devices, iCloud data, and Apple Pay — lacked the account-recovery and multi-factor safeguards expected for an asset of this criticality.

**Why it matters:** The Apple ID is arguably the highest-value credential in the environment. A takeover could allow an attacker to locate or erase devices, access iCloud Photos and Drive, and interfere with payment cards. The gap between *how critical the asset is* and *how well it is protected* is the clearest example in this inventory of why asset prioritization must come before control selection.

---

### Finding 3: SMS-Based 2FA Rests on a Fragile Foundation

**Related assets:** A-U01, H-04, and every account using SMS codes · **CSF:** PR.AA-03 (Authentication)

Most accounts with 2FA use SMS codes. SMS delivery depends on the carrier account, which can be targeted through **SIM swapping** — an attacker convinces or compromises the carrier to move my number to their SIM.

**Why it matters:** This is a cascading risk. One successful attack against the carrier account can defeat the second factor on many accounts at once, including financial ones. The root cause is the absence of an authenticator app or hardware security key; the carrier account is not "a phone bill account" but a piece of authentication infrastructure.

---

### Finding 4: Career Knowledge Base Has No Backup

**Related assets:** D-K01, H-01 · **CSF:** PR.DS-01 (Data-at-rest protection), PR.DS-11 (Backups), RC.RP-01 (Recovery plan execution)

The Obsidian vault holding my core career strategy exists **only on the MacBook** — no version control, no cloud sync, no external backup.

**Why it matters:** This is a pure availability failure waiting to happen. Loss, theft, or hardware failure of the laptop would permanently destroy months of accumulated work, and there is no recovery path. It also shows that "Critical" does not always mean "confidential" — here the dominant risk is loss, not exposure. Any backup design must still protect confidentiality (e.g., a **private** repository or encrypted backup).

---

### Finding 5: Shared Network with No Transport Protection

**Related assets:** H-05, H-01, H-02, H-03 · **CSF:** ID.AM-03 (Network communication and data flows), PR.IR-01 (Network protection / segmentation), PR.DS-02 (Data-in-transit protection), GV.SC (Supply chain risk management)

All devices connect through a landlord-provided Wi-Fi network whose password is shared with roommates. Router administration is not under my control, and I do not currently use a VPN.

**Why it matters:** I cannot verify the router's configuration, firmware, or who has administrative access, and my devices share a network segment with devices I do not manage. This mirrors a common organizational problem: relying on infrastructure owned by a third party (a supplier) without visibility into its controls. The realistic response is not to "fix the router" but to **compensate at the endpoint** — encrypted transport, device firewalls, and treating the home network as untrusted.

---

## 9. Next Steps

This inventory completes the **Identify (ID.AM)** phase. The next phase uses it as input.

| Phase | Deliverable | Focus |
|---|---|---|
| **Next** | `02-current-state-assessment-v2.xlsx` | Assess current controls for each Critical and High asset against CSF 2.0 **Protect (PR)** subcategories — primarily PR.AA (authentication), PR.DS (data security), and PR.IR (infrastructure resilience). |
| Then | `03-remediation-plan.md` | Define the target state and a prioritized gap list. |
| Then | `personal-security-policy.md` | Actions, owners (me), and timeline, starting with the Key Findings above. |

### Immediate carry-overs from this inventory

- [ ] Complete file-level inventory of iCloud Drive and Google Drive (D-C02, D-C03).
- [ ] Decide the purpose of — or retire — the secondary Gmail and Outlook accounts (A-I02, A-I04).
- [ ] Map which accounts use SMS 2FA vs. stronger methods (input for Finding 3).
- [ ] Review Low-priority accounts for deletion to reduce attack surface.
- [ ] Schedule a quarterly review of this inventory (supports ID.AM-08, asset lifecycle).

---

*This is a student learning project. Ratings reflect my own judgment applied to NIST CSF 2.0 and are not a professional audit.*
