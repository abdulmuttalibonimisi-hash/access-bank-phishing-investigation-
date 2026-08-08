# access-bank-phishing-investigation-

# Access Bank Phishing Email Investigation

## 1. Overview

This investigation analyzed an email claiming to be from Access Bank containing a July 2026 account statement as an encrypted PDF attachment.

The investigation focused on determining whether the email showed signs of phishing, spoofing, or suspicious sending infrastructure.

The attachment was not uploaded to public analysis platforms because the document contained sensitive financial information and was encrypted.

## 2. Investigation Objective

- Verify the sender's domain
- Analyze the email headers
- Verify SPF, DKIM, and DMARC results
- Identify the sending IP and mail infrastructure
- Check the IP reputation
- Examine the email content for phishing indicators
- Determine whether the attachment could be safely investigated
- Reach a reasonable final assessment based on available evidence

## 3. Email Information

| Field | Value |
|---|---|
| Sender | noreply@accessbankplc.com |
| Display name | Access Bank |
| Subject | July 2026 Account Statement |
| Attachment | Consolidated_Jul2026_Statement.pdf |

The email stated that the attached account statement was available and that the document required a password to open. It also contained a security reminder advising recipients not to share card numbers, CVV, OTPs, PINs, or passwords.

## 4. Initial Email Analysis

The sender address matched the Access Bank domain: `accessbankplc.com`

The email content was professionally written with no obvious spelling or grammatical errors. It did not immediately show common phishing indicators such as:

- An unrelated sender domain
- Obvious spelling mistakes
- Urgent threats
- Requests for OTPs or passwords
- Suspicious payment instructions

The sender address and content alone did not provide enough evidence to classify the email as phishing — further technical analysis was required.

**Evidence:** `evidence/email.png`

## 5. Email Header Analysis

### SPF — PASS
```
spf=pass
```
Sending IP: `202.162.253.144`. Google's authentication result indicated the sending infrastructure was authorized by the relevant sending domain.

### DKIM — PASS
```
dkim=pass header.i=@accessbankplc.com
```
DKIM selector: `nc2048`. This provided evidence that the message carried a valid DKIM signature associated with `accessbankplc.com`.

### DMARC — PASS
```
dmarc=pass
header.from=accessbankplc.com
```
The visible From domain passed DMARC authentication.

### Authentication Summary

| Check | Result |
|---|---|
| SPF | PASS |
| DKIM | PASS |
| DMARC | PASS |

All three authentication checks passed, significantly reducing the likelihood of a simple sender-domain spoofing attack.

## 6. Sending Infrastructure

- **Sending IP:** `202.162.253.144`
- **Sending server:** `mta-253.144.ncdelivery08.com`
- **X-Mailer:** `NetcoreCloud Mailer`
- **Message-ID domain:** `pepipost.com`

These headers indicate the email passed through third-party email delivery infrastructure (Netcore/Pepipost, a legitimate transactional email provider). These were recorded as infrastructure indicators for further investigation rather than treated as malicious by default.

## 7. IP Reputation

Checked `202.162.253.144` against **AbuseIPDB**.

**Result:** 0 abuse reports.

This reduced the suspicion associated with the IP, although a clean reputation result does not prove an IP is completely safe.

## 8. Attachment Analysis

`Consolidated_Jul2026_Statement.pdf` — Gmail flagged this as an **encrypted attachment** it could not scan for malicious content.

**Evidence:** `evidence/encrypted-attachment.png`

The attachment was **not** uploaded to public malware-analysis platforms (e.g. VirusTotal), since it appeared to contain sensitive financial information and uploading it would introduce unnecessary privacy and data-exposure risk.

**Attachment status: UNVERIFIED** — not classified as malicious (no evidence of malicious content) and not classified as safe (contents not inspected).

## 9. Findings

| Indicator | Finding |
|---|---|
| Sender domain | accessbankplc.com |
| SPF | PASS |
| DKIM | PASS |
| DMARC | PASS |
| Sending IP | 202.162.253.144 |
| IP reputation | 0 AbuseIPDB reports |
| Attachment | Encrypted PDF |
| Attachment analysis | Not performed |
| Email content | No obvious phishing indicators |

## 10. Final Assessment

No strong technical indicator showed the email was spoofed or fraudulent. The strongest evidence was the successful SPF, DKIM, and DMARC results combined with a clean IP reputation.

- **Email classification:** LIKELY LEGITIMATE
- **Attachment classification:** UNVERIFIED
- **Confidence:** Moderate–High (email authenticity) / Low–Moderate (attachment safety)

## 11. Investigation Limitations

The encrypted PDF was not independently analyzed, which prevented verification of its:

- File hash
- Embedded objects
- URLs
- Scripts or macros
- Metadata
- Potential malicious content

The investigation therefore focused on email authentication, sender infrastructure, IP reputation, and visible content rather than file-level analysis.

## 12. Tools Used

- Gmail (header source, attachment scan warning)
- Email header analysis (SPF/DKIM/DMARC parsing)
- WHOIS
- AbuseIPDB (IP reputation)

## 13. Conclusion

Strong evidence supported the authenticity of the email's sending domain: SPF, DKIM, and DMARC all passed, the sending IP had no AbuseIPDB reports, and the content showed no obvious phishing indicators. The encrypted attachment prevented complete file-level verification, so it was recorded as unverified rather than declared safe.

This investigation demonstrates the importance of combining email authentication, infrastructure analysis, reputation checks, and careful evidence handling when investigating suspected phishing emails — and of recognizing when *not* to upload sensitive material to third-party scanning services.
