# Mediroza General Hospital — Web Application Penetration Test

[![Status](https://img.shields.io/badge/status-complete-brightgreen?style=for-the-badge)](#engagement-status)
[![Type](https://img.shields.io/badge/engagement-authorised%20black--box-blue?style=for-the-badge)](#assessment-overview)
[![Assessment](https://img.shields.io/badge/assessment-web%20application%20pentest-0969da?style=for-the-badge)](#assessment-overview)
[![Methodology](https://img.shields.io/badge/methodology-OWASP%20WSTG-8250df?style=for-the-badge)](#methodology)
[![Highest Severity](https://img.shields.io/badge/highest%20severity-critical-d73a49?style=for-the-badge)](#risk-summary)

A comprehensive web application penetration testing engagement for Mediroza General Hospital (medirozahospital.com), conducted as part of the Networkwalks Academy cybersecurity training program. This repository documents the complete assessment methodology, security findings, supporting evidence, remediation recommendations, and final client-facing report developed across all four project milestones.
---

## Table of Contents

- [Project Overview](#project-overview)
- [Milestones](#milestones)
- [Key Findings](#key-findings)
- [Repository Structure](#repository-structure)
- [Methodology](#methodology)
- [Tools Used](#tools-used)
- [Report](#report)
- [Disclaimer](#disclaimer)


---

## Project Overview

| | |
|---|---|
| **Client** | Mediroza General Hospital *(fictional)* |
| **Target** | `medirozahospital.com` |
| **Engagement type** | Authorised web application penetration test (black-box, credential-guessing permitted) |
| **Testing window** | 4–7 September 2026 |
| **Authorisation** | Written permission granted for all testing activities |
| **Platform** | Kali Linux |
| **Report date** | 7 September 2026 |


## Milestones

The engagement was broken into four graded milestones:

| ID | Milestone | Objective | Status |
|----|-----------|-----------|--------|
| **M1** | Initial Access | Attack the website and retrieve 3 confidential patient PDF lab reports | ✅ Complete |
| **M2** | Data Extraction | Crack the encryption on all 3 retrieved files | ✅ Complete |
| **M3** | Attack (Cracking) | Find staff salaries and shareholder details of the hospital | ✅ Complete |
| **M4** | Pentest Report | Write a professional penetration testing report for the client | ✅ Complete |

See [`docs/engagement-brief.md`](docs/engagement-brief.md) for the full brief, hints, and deliverables issued for each milestone.

## Key Findings

| ID | Finding | Severity | Milestone |
|----|---------|----------|-----------|
| F1 | Sensitive database backup exposed via predictable/legacy directory (`/old/`) | 🔴 **Critical** | M1 / M3 |
| F2 | Directory listing enabled, exposing application source and internal paths | 🟠 **High** | M1 |
| F3 | Weak authentication — no account lockout or rate limiting on `login.php` | 🟠 **High** | M1 |
| F4 | Weak, dictionary-crackable passwords protecting confidential patient PDF reports | 🟡 **Medium** | M2 |

Full details, CVSS-aligned risk ratings, evidence, and remediation guidance for every finding are in the [final report](#report).

## Repository Structure

```
mediroza-pentest/
├── README.md                      # This file                       
├── docs/
│   ├── engagement-brief.md        # Original milestone brief (M1–M4)
│   └── methodology.md             # Testing methodology and rules of engagement
├── report/
│   └── Mediroza_Pentest_Report.docx   # Final client-facing report
└── evidence/
    ├── M1-initial-access/         # Recon, directory listing, brute-force login
    ├── M2-data-extraction/        # PDF hash extraction & dictionary cracking
    └── M3-critical-exposure/      # Exposed SQL backup (staff + shareholders)
```

Evidence filenames are numbered in the order the corresponding action was performed, so each folder can be read top-to-bottom as a walkthrough.

## Methodology

Testing followed a standard black-box web application methodology:

1. **Reconnaissance & content discovery** — mapping reachable paths and identifying misconfigurations
2. **Authentication analysis** — reviewing the login mechanism for weaknesses
3. **Credential attack** — automated brute-forcing via Burp Suite Intruder
4. **Post-exploitation data review** — analysing every retrieved file for further exposures
5. **Offline cracking** — recovering passwords protecting encrypted deliverables
6. **Reporting** — consolidating findings into a client-ready report with evidence and remediation

Full details in [`docs/methodology.md`](docs/methodology.md).

## Tools Used

- **Kali Linux** — testing platform
- **Burp Suite Professional** (Proxy, Repeater, Intruder) — request interception and automated credential attacks
- **Networkwalks Hash Calculator** — extraction of crackable hashes from encrypted PDFs (pdf2john/hashcat-compatible)
- **Networkwalks Password Cracker** — dictionary attack engine
- **Firefox** — manual browsing and content discovery

## Report

The full professional penetration testing report — Executive Summary, Scope & Methodology, Findings & Proof of Exploitation, Risk Rating, and Recommendations — is available at:

📄 [`report/Mediroza_Pentest_Report.docx`](report/Mediroza_Pentest_Report.docx)

## Disclaimer

This penetration testing engagement was conducted with explicit authorization from Networkwalks Academy. All testing activities were performed within the agreed scope and in accordance with the applicable rules of engagement.

The techniques and procedures documented in this repository are intended for authorized security testing and defensive purposes only. Security testing must never be performed against systems, applications, or infrastructure without explicit permission from the owner. Unauthorized access or security testing may violate applicable laws and regulations.
