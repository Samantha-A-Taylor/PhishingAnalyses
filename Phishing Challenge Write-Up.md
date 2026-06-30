***
# Phishing Email Challenge
## Summary
Investigated a low-complexity phishing alert involving an email containing a malicious link with financial intent. Identified several red flags during initial triage, including a non-English message body, suspicious sender address, and a PayPal-themed call-to-action. The embedded URL was validated as malicious via sandbox testing and VirusTotal analysis. The alert was closed as a true positive, with the threat confirmed through independent URL analysis.

## Alert Details
| DATE | SMTP ID | SENDER | RECIPIENT | ATTACHMENT |
| --- | --- | --- | --- | --- |
| Aug, 15, 2022 | l5csp1310935vqx | Marrybenh@kodehexa.net | krystyalia@gmail.com | Link |

## Investigation Process
### 1. Initial Triage - Identifying "red flags"
First, the email is examined in its entirety.
<br><br>

<img width="800" height="613" alt="Screenshot 2026-06-29 202202" src="https://github.com/user-attachments/assets/b02b25e0-6b78-4b2e-b005-5011f6cde34e" />
<br><br>

       From first glance, several red flags are raised:
               - Email is not in English, and sender has strange characters in address name
               - Call-to-action (CTA) within the message body (click PayPal)
               - Links with financial intent
<br>

### 2. URL Analysis - Utilizing VirusTotal
First, URL *https://storage.googleapis.com/hqyoqzatqthj/aemmfcylvxeo.html* was opened in a sandbox environment, resulting in Internet Explorer blocking it.

<br>

<img width="862" height="599" alt="Screenshot 2026-06-29 203208" src="https://github.com/user-attachments/assets/624173cb-832e-4b9a-ab2e-2e2b9aa7e34b" />

<br>

       The URL domain was analyzed by third-party sandbox VirusTotal.

<br><br>

<img width="1281" height="691" alt="Screenshot 2026-06-29 203316" src="https://github.com/user-attachments/assets/30299ffe-2ea0-40b9-a1b0-ce3e382c95ba" />

<br>

       VirusTotal flagged the URL as malicious (7/92 vendors).
<br>

<img width="478" height="292" alt="Screenshot 2026-06-29 203339" src="https://github.com/user-attachments/assets/905f1b36-767a-43b3-92b1-73f91d96608e" />
<br>

        The body SHA-256 of the domain was 13945ecc33afee74ac7f72e1d5bb73050894356c4bf63d02a1a53e76830567f5.

## Findings
The alert was confirmed as a **true positive**. The embedded URL was blocked by Internet Explorer upon opening in a sandbox environment, and VirusTotal independently flagged the domain as malicious (7/92 vendors). Combined with the email's non-English content, suspicious sender address, and PayPal-themed financial lure, the evidence collectively confirms this as a phishing attempt.

## Skills Demonstrated
- Phishing Email Investigation
- Malware triage
- URL Analysis (VirusTotal)

## Practice Project Source
[Challenge | LetsDefend](https://app.letsdefend.io/challenge/phishing-email)
***
