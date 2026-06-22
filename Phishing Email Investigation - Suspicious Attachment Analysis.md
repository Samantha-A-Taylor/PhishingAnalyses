***
# Phishing Email Investigation: Suspicious Task Scheduler Attachment

## Summary
Investigated a medium-severity phishing alert involving an email with a password-protected attachment and urgent, COVID-19-themed subject matter. Cross-referenced the sender's domain health, validated the attachment as malicious using two independent sandboxes, and traced the email's delivery path through log and endpoint data to confirm no execution occurred. The alert was closed as a true positive, with the threat fully contained by the existing email block.

## Alert Details

| SEVERITY | DATE | SMTP ADDRESS | SENDER | RECIPIENT | SUBJECT | ATTACHMENT |
| --- | --- | --- | --- | --- | --- | --- |
| Medium | Mar, 21, 2021 | 189.162.189.159 | aaronluo@cmail.carleton.ca | mark@letsdefend.io | COVID19 Vaccine | Yes |

## Investigation Process
### 1. Initial Triage - Identifying "red flags"

First, the email is examined in its entirety.<br><br>
<img width="659" height="487" alt="image" src="https://github.com/user-attachments/assets/2e9e5e79-f0b7-441a-a2ce-f4f2067b6af1" />
<br>

        From first glance, several red flags are raised:
               - Urgency in the "COVID19 Vaccine" subject line
               - Urgency within the message with phrases like "breaking news" and "Open it now!"
               - Password inclusion with the attachment

Next, a tool is used to obtain an email domain health report of the sender's address *@cmail.carleton.ca*.<br><br>
<img width="1576" height="694" alt="image" src="https://github.com/user-attachments/assets/284d9c3e-18ee-4ee0-b2ad-adac216bab3c" />
<br><br>
            
        MX Toolbox SuperTool delivered a Domain Health Report suggesting:
               - 11 total problems
               - 3 total Mail Server tests failed
               - 1 total Web Server tests failed
<br>

While not outright suggesting a malicious sender, it gives reason to warrant suspicion.
        
### 2. Attachment Analysis - Utilizing VirusTotal & HybridAnalysis

Attachment *72c812cf21909a48eb9cceb9e04b865d* was analyzed by third-party sandboxes VirusTotal and HybridAnalysis.<br><br>

<img width="1597" height="644" alt="image" src="https://github.com/user-attachments/assets/90d24996-0ab7-4dd0-8be9-1a2d129391d7" />
<br><br>

      VirusTotal flagged the attachment hash as malicious (32/61 vendors), with Popular threat label suggesting trojan.

<br><br>

<img width="1580" height="728" alt="image" src="https://github.com/user-attachments/assets/69b6b8e8-bcc9-417c-9162-f44ca7a34346" />
<br><br>

      HybridAnalysis also flagged the attachment hash as:
               - malicious (5/6 vendors)
               - suspicious (1/6 vendors)
<br>

Both third-party sandboxes independently identified the attachment as malicious.

### 3. Log Managment - Tracing the delivery path

Log managment was conducted on sender address *189.162.189.159* to find the email destination address and port number.<br><br>

<img width="1532" height="626" alt="image" src="https://github.com/user-attachments/assets/c6997c13-ee48-4563-987d-6b719b974b52" />
<br><br>

      The email destination address was 172.16.20.3 and port number was 25.
<br>

### 4. Endpoint Verification - Execution check

Endpoint Security was used from destination IP 172.16.20.3 to identify the destination machine and process history.<br><br>

<img width="1496" height="582" alt="image" src="https://github.com/user-attachments/assets/fe737bd2-8b52-46cd-8bc1-69f0d9269e96" />
<br><br>

      The destination machine was the MS Exchange Server. 
      However, there are no suspicious activities revealed in the history. 
      This may be explained by the device action having already been blocked. 
<br>

## Findings
The alert was confirmed as a **true positive**. The attachment was independently flagged as malicious by both VirusTotal and HybridAnalysis, and while the sender's domain showed multiple health/configuration issues, the email itself was blocked before delivery, which was confirmed by the absence of any suspicious process activity on the destination host.

## Skills Demonstrated
- Phishing Email Investigation
- Log analysis
- Malware triage
- Endpoint investigation
- Attachment Analysis (VirusTotal, HybridAnalysis)

## Practice Project Source
[LetsDefend's SOC140 - Phishing Mail Detected - Suspicious Task Scheduler](https://app.letsdefend.io/monitoring?channel=investigation&event_id=82) 

***
