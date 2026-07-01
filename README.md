***
# SOC Phishing Investigation Portfolio
***
## Project Overview ☰
This project documents a series of hands-on phishing email and phishing URL investigations completed as SOC analyst practice through LetsDefend's simulated alert environment. Each write-up follows a full investigation workflow, from initial triage through evidence gathering, verdict determination, and closure reasoning, for alerts involving malicious attachments, malicious links, and internal email traffic. **The goal of this project is to demonstrate a repeatable, evidence-based approach to phishing triage:** identifying red flags, validating indicators of compromise (IOCs) through independent third-party sandboxes, tracing delivery paths through log data, and confirming (or ruling out) execution on the destination endpoint.

## Project Parts  <img width="23.75" height="29.75" alt="image" src="https://github.com/user-attachments/assets/0b89b807-26fe-4839-9dc3-00d2ed328bd5" />

✓ [SOC Alert | Phishing URL Detected](https://github.com/Samantha-A-Taylor/PhishingAnalyses/blob/main/Phishing%20URL%20Detected%20Write-Up.md)<br>
✓ [SOC Alert | Phishing Mail Detected - Suspicious Task Scheduler](https://github.com/Samantha-A-Taylor/PhishingAnalyses/blob/main/Suspicious%20Task%20Scheduler%20Attachment%20Write-Up.md) <br>
✓ [SOC Alert | Phishing Mail Detected - Internal to Internal](https://github.com/Samantha-A-Taylor/PhishingAnalyses/blob/main/Internal%20to%20Internal%20Write-Up.md) <br>
✓ [SOC Alert | Malicious Attachment Detected - Phishing Alert](https://github.com/Samantha-A-Taylor/PhishingAnalyses/blob/main/Malicious%20Attachment%20Detected%20Write-Up.md)<br>
✓ [SOC Alert | Phishing Mail Detected - Excel 4.0 Macros](https://github.com/Samantha-A-Taylor/PhishingAnalyses/blob/main/Excel%204.0%20Macros%20Write-Up.md)<br>
✓ [Challenge | Phishing Email](https://github.com/Samantha-A-Taylor/PhishingAnalyses/blob/main/Phishing%20Challenge%20Write-Up.md)

## Summary Table  <img width="23" height="23" alt="image" src="https://github.com/user-attachments/assets/4b5c4721-14d5-4284-8bd0-83adb2b465c3" />

| Alert | Severity | Verdict | Key Evidence |
| --- | --- | --- | --- |
| Phishing URL Detected | High | True Positive | Malicious domain flagged by VirusTotal & HybridAnalysis; endpoint history showed remote script execution |
| Suspicious Task Scheduler | Medium | True Positive | Malicious attachment flagged by VirusTotal & HybridAnalysis; email blocked before delivery, no endpoint execution |
| Internal to Internal | Medium | False Positive | No attachment, link, or call-to-action; benign internal correspondence |
| Malicious Attachment Detected | High | True Positive | Malicious Excel dropper flagged by VirusTotal, HybridAnalysis & Filescan.io; EXCEL.EXE execution confirmed on endpoint |
| Excel 4.0 Macros | High | True Positive | All 3 attachment files flagged malicious by HybridAnalysis; DLL registration confirmed via regsvr32.exe on endpoint |
| Phishing Email Challenge | N/A | True Positive | Malicious URL flagged by VirusTotal; PayPal-themed financial lure with non-English body text |

## Key Features 🔑
       ✓ Initial email triage to identify red flags in headers, sender addresses, subject lines, and message body language
       ✓ Sender and destination domain reputation/health checks (SPF, DKIM, blacklist status, mail server configuration issues)
       ✓ Malicious attachment analysis across file types, including zip archives, Excel (.xls/.xlsx) documents, and DLLs, 
          including Excel 4.0 macro–based malware
       ✓ Malicious URL analysis, including sandbox detonation and multi-vendor threat scoring
       ✓ Log management to trace email/request delivery paths between source and destination addresses
       ✓ Endpoint investigation to confirm or rule out execution, using process and terminal history review
       ✓ True positive / false positive determination with documented, evidence-based closure reasoning

## Technologies Used 🛠️
       ✓ LetsDefend SOC Platform (Log Management & Endpoint Security modules)
       ✓ VirusTotal
       ✓ HybridAnalysis
       ✓ Filescan.io
       ✓ MXToolbox SuperTool

## Project Sources 🗂️
✓ [SOC141 - Phishing URL Detected | LetsDefend](https://app.letsdefend.io/monitoring?channel=investigation&event_id=86)<br>
✓ [SOC140 - Phishing Mail Detected - Suspicious Task Scheduler | LetsDefend](https://app.letsdefend.io/monitoring?channel=investigation&event_id=82) <br>
✓ [SOC120 - Phishing Mail Detected - Internal to Internal | LetsDefend](https://app.letsdefend.io/monitoring?channel=investigation&event_id=52) <br>
✓ [SOC114 - Malicious Attachment Detected - Phishing Alert | LetsDefend](https://app.letsdefend.io/monitoring?channel=investigation&event_id=45)<br>
✓ [SOC146 - Phishing Mail Detected - Excel 4.0 Macros | LetsDefend](https://app.letsdefend.io/monitoring?channel=investigation&event_id=93)<br>
✓ [Challenge - Phishing Email | LetsDefend](https://app.letsdefend.io/challenge/phishing-email)

## License
MIT License

Copyright (c) 2026 Samantha-A-Taylor
***
