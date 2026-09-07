# Methodology

## Scope

- **In scope:** `https://medirozahospital.com` — the patient portal, its authentication mechanism, and any linked resources discovered during testing.
- **In-scope activities:** reconnaissance, authentication testing, directory/file enumeration, credential attacks against the login form, and offline cracking of any encrypted files retrieved during testing.
- **Out of scope:** denial-of-service testing, social engineering of staff, and any systems not resolving to the `medirozahospital.com` domain.

## Rules of Engagement

- All testing was performed under written authorisation obtained prior to the engagement.
- Testing was limited to the agreed window (4–7 September 2026).
- No destructive actions (data modification/deletion, service disruption) were performed at any point.
- All findings were handled confidentially and reported only to the client/instructor.

## Approach

The engagement followed a standard black-box web application testing methodology, broadly aligned with OWASP's testing phases:

### 1. Reconnaissance & Content Discovery
Manual browsing and directory enumeration were used to map the application's structure. Requesting known application paths without a valid resource parameter (e.g. `/patient/`) revealed that directory listing was enabled, exposing script names, log files, and — critically — a legacy `/old/` directory.

### 2. Authentication Analysis
The `/patient/login.php` endpoint was analysed for session handling, response behaviour on failure vs. success, and the presence (or absence) of anti-automation controls such as CAPTCHA, rate-limiting, or account lockout.

### 3. Credential Attack
With no rate-limiting observed, Burp Suite Intruder was used in Sniper mode against the `password` parameter (username fixed as `admin`) with a curated wordlist. Responses were filtered for HTTP 302 (successful redirect) to identify a working credential pair.

### 4. Post-Exploitation Data Review
Once authenticated, all reachable resources were reviewed — including the three password-protected PDF lab reports available from the portal, and the previously discovered `/old/` directory, which contained an unprotected SQL database backup.

### 5. Offline Cracking
A crackable hash (pdf2john/hashcat-compatible format) was extracted from each retrieved PDF and run through a dictionary attack to recover the individual document passwords.

### 6. Reporting
All findings were consolidated into a client-ready report including an executive summary, methodology, evidence-backed findings, CVSS-aligned risk ratings, and actionable remediation guidance.

## Limitations

This was a time-boxed, black-box assessment. No source code review or internal network testing was performed. Findings are limited to what was reachable and observable from an external, unauthenticated (and subsequently low-privilege authenticated) vantage point.
