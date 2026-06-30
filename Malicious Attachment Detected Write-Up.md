***
# Phishing Alert: Malicious Attachment Detected

## Summary
Investigated a high-severity phishing alert involving an email with a password-protected zip attachment containing a malicious Excel file. Cross-referenced the sender's domain health, validated the zip and its contents as malicious using multiple independent sandboxes, and traced the email's delivery path through log and endpoint data to confirm execution had occurred on the destination machine. The alert was closed as a true positive, with evidence of the Excel dropper being triggered on the affected host.

## Alert Details
| SEVERITY | DATE | SMTP ADDRESS | SENDER | RECIPIENT | SUBJECT | ATTACHMENT |
| --- | --- | --- | --- | --- | --- | --- |
| High | Jan, 31, 2021 | 49.234.43.39 | accounting@cmail.carleton.ca | richard@letsdefend.io | Invoice | Yes |

## Investigation Process
### 1. Initial Triage - Identifying "red flags"

First, the email is examined in its entirety.<br><br>
<img width="924" height="399" alt="image" src="https://github.com/user-attachments/assets/ca2ed36a-2719-433f-a67f-2d41a09371c1" />
<br>

        From first glance, no severe red flags are raised:
               - No urgency in the subject line or within the message
               - Password inclusion with the attachment

Next, MXToolbox is used to obtain an email domain health report of the sender's address *@cmail.carleton.ca*.<br><br>
<img width="1092" height="576" alt="image" src="https://github.com/user-attachments/assets/21f0aa8a-4670-4e46-bb15-51d261cd27b3" />
<br><br>

        MX Toolbox SuperTool delivered a Domain Health Report suggesting:
               - 11 total problems
               - 3 total Mail Server tests failed
               - 1 total Web Server tests failed
<br>

While not outright suggesting a malicious sender, it gives reason to warrant suspicion.

### 2. Attachment Analysis - Utilizing VirusTotal, HybridAnalysis & Filescan.io

When opened in a sandbox environment, attachment *c9ad9506bcccfaa987ff9fc11b91698d* contained *44e65a641fb970031c5efed324676b5018803e0a768608d3e186152102615795.xlsx*. Each were analyzed by third-party sandboxes.<br><br>

#### *c9ad9506bcccfaa987ff9fc11b91698d.zip* Analysis
<img width="1168" height="526" alt="image" src="https://github.com/user-attachments/assets/71bbb74c-8572-48c8-87e6-ed96e5fe2171" />
<br><br>

      VirusTotal flagged the attachment as malicious (36/60 vendors), with Popular threat labels suggesting trojan or malware.
<br><br>

<img width="1168" height="621" alt="image" src="https://github.com/user-attachments/assets/96e5d983-3b66-4616-b979-83ee78c57a86" />
<br><br>

      HybridAnalysis also flagged the attachment as malicious (6/6 vendors).
<br>

#### *44e65a641fb970031c5efed324676b5018803e0a768608d3e186152102615795.xlsx* Analysis
<img width="1551" height="617" alt="image" src="https://github.com/user-attachments/assets/7ab85372-15d7-4bff-ab9b-34e68d3f6084" />
<br><br>

      Filescan.io flagged the attachment as a confirmed threat.
<br><br>

<img width="1266" height="620" alt="image" src="https://github.com/user-attachments/assets/8903bb59-4d0f-4aa4-9ab5-cf0cd2f2b0a2" />
<br><br>

      HybridAnalysis flagged the attachment as malicious (6/6 vendors).
<br>

Third-party sandboxes independently identified the zip and the file contained within it as malicious.

### 3. Log Management - Tracing the delivery path

Log management was conducted on sender address *49.234.43.39* to find the email destination address and port number.<br><br>
<img width="667" height="384" alt="image" src="https://github.com/user-attachments/assets/2646c014-233e-40c6-bf88-084d86626b86" />
<br><br>

      The email destination address was 172.16.20.3 and port number was 25.
<br>

### 4. Endpoint Verification - Execution check

Endpoint Security was used from user richard@letsdefend.io to identify the destination machine and history.<br><br>
<img width="960" height="404" alt="image" src="https://github.com/user-attachments/assets/62a847ea-aa3d-4b7f-8161-d7be8ec912dd" />
<br><br>

      The destination machine was RichardPRD.
      Process history shows record of command *C:/Program Files/Microsoft Office/Office14/EXCEL.EXE*,
         which opened the document and triggered the dropper.
<br>

## Findings
The alert was confirmed as a **true positive**. The zip and the Excel file contained within it were flagged as malicious by multiple independent sandboxes. Endpoint analysis confirmed the attachment was opened on RichardPRD, with process history showing EXCEL.EXE executing the file and triggering the dropper. The email reached the recipient and the affected machine should be isolated and the malicious files remediated.

## Skills Demonstrated
- Phishing Email Investigation
- Log analysis
- Malware triage
- Endpoint investigation
- Attachment Analysis (VirusTotal, HybridAnalysis, Filescan.io)

## Practice Project Source
[SOC114 - Malicious Attachment Detected - Phishing Alert | LetsDefend](https://app.letsdefend.io/monitoring?channel=investigation&event_id=45)

***
