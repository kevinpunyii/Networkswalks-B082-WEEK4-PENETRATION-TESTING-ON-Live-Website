# Mediroza General Hospital — Web Application Penetration Test

##![Status](https://img.shields.io/badge/status-complete-brightgreen)
##![Type](https://img.shields.io/badge/engagement-authorised%20black--box-blue)
##![Severity](https://img.shields.io/badge/highest%20severity-critical-critical?color=b03a2e)
##![License](https://img.shields.io/badge/docs%20license-MIT-lightgrey)

A student penetration testing engagement against a purpose-built, fictional hospital web application (`medirozahospital.com`), completed as part of the **Networkwalks Academy** cybersecurity training program. This repository contains the full methodology, evidence, and final client-facing report produced across all four project milestones.

> **This is a training lab.** Mediroza General Hospital, its staff, patients, and data are entirely fictional and were generated for this exercise. All testing was carried out in a controlled environment against a target the student was explicitly authorised, in writing, to test. Nothing in this repository was performed against a real organisation.

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
- [License](#license)

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

The objective was to simulate a real-world external attacker targeting the hospital's patient portal and supporting infrastructure, culminating in a professional penetration testing report suitable for delivery to a client.

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
├── LICENSE                        # Documentation license
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

This project is conducted in a controlled environment for **educational purposes only**. The target was a purpose-built training application authorised for security testing by Networkwalks Academy. These techniques must never be applied to any system without explicit written permission from the owner. Unauthorised access to computer systems is illegal in most jurisdictions.

## License

The written documentation in this repository (README, report, and docs) is released under the [MIT License](LICENSE). This license covers the write-up only — it does not grant permission to test any system, and no warranty is made regarding the accuracy of the fictional data used in this exercise.
