# Analyze-a-Phishing-Email-Sample

Detailed analysis of a phishing email impersonating CitiBank. Includes email header review, identification of suspicious links and attachments, social engineering assessment, risk evaluation, and recommended mitigation steps. Designed for cybersecurity awareness and threat detection learning

# Phishing Email Analysis Report — CitiBank Sample

**Sample filename:** sample_email.eml
**Analyst:** Mohammad abdul sami
**Date:** 24 Sep 2025

---

## Summary
This email is a phishing attempt impersonating CitiBank. It contains multiple indicators of spoofing and social engineering: failed authentication (SPF/DKIM/DMARC), mismatched link text vs actual URL, generic greeting, urgent language, and a malicious-looking attachment `Statement_1234.pdf.exe`.

---

## 1. Raw headers examined
- Return-Path: `<bounce@citibank-spool.com>`
- Received from: `mail.citibank-spool.com (198.51.100.45)`
- Authentication-Results: `spf=fail; dkim=none; dmarc=fail`
- From: `"CitiBank" <alerts@citibank-secure.com>`
- Reply-To: `alerts@citibank-support.com`
- Message-ID: `<CA+xyz7890@mail.citibank-spool.com>`

**Conclusion:** Sender authentication fails and headers indicate delivery from an unauthorized mail server not controlled by CitiBank.

---

## 2. Sender/address analysis
- Display name: `CitiBank`
- From address: `alerts@citibank-secure.com` (not `citibank.com`) — suspicious domain.
- Reply-To domain: `citibank-support.com` (different again) — inconsistency.

**Indicator:** Multiple domains and mismatch with official domain; likely spoofing.

---

## 3. Links and attachments
- Visible link text: `https://www.citibank.com/`
- Actual href: `http://citibank-secure-login.com/verify?uid=8a7b6c`
  - Not HTTPS (http), and host is unrelated to official CitiBank domain.
- Attachment: `Statement_1234.pdf.exe` — double extension, executable disguised as PDF.

**Indicator:** Mismatched link, suspicious domain, and potentially malicious attachment.

---

## 4. Content and social engineering
- Urgent language: "suspicious activity", "temporarily restricted", implication of account loss.
- Generic greeting: "Dear Valued Customer" (no personalization).
- Phone number: `1-800-555-0199` (could be fake/forwarded).
- Branding: Use of CitiBank name and logo to build trust.

**Indicator:** Classic social engineering — urgency + authority.

---

## 5. Technical checks performed / recommended
- SPF check: Fails — sender IP is not authorized to send for the claimed domain.
- DKIM: None — message not signed.
- DMARC: Fails — policy not aligned with header from domain.
- Header analysis: Received path indicates non-CitiBank mail server.

**Tools used / recommended:** MXToolbox Email Header Analyzer, VirusTotal (for link/attachment check), WHOIS (domain ownership), and browser link-hover.

---

## 6. Risk assessment
- **Credential theft:** High risk if user clicks the link and submits login details.
- **Malware:** High risk due to `.exe` attachment disguised as PDF.
- **Business impact:** High — potential fraud or account takeover.

---

## 7. Recommended actions
1. Do not click links or open attachments.
2. Quarantine and report the email to your security team and to CitiBank's official phishing reporting channels.
3. Block sending IPs/domains at the email gateway.
4. If possible, analyze the attachment in a secure sandbox environment (do not run on production).
5. Train users to check sender domains, hover links, and verify communication via official channels.

---

## 8. Conclusion
The email demonstrates clear phishing indicators (authentication failures, link mismatch, social engineering). Treat it as malicious and follow incident response procedures.
