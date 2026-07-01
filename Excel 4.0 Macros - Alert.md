***
# Phishing Email Investigation: Excel 4.0 Macros

## Summary
Investigated a high-severity phishing alert involving an email with a password-protected zip attachment containing malicious Excel and DLL files leveraging Excel 4.0 macros. Cross-referenced the sender's domain health, validated all three files within the attachment as malicious using HybridAnalysis, and confirmed execution had occurred on the destination machine via endpoint analysis. The alert was closed as a true positive, with evidence of active DLL registration on the affected host.

## Alert Details

| SEVERITY | DATE | SMTP ADDRESS | SENDER | RECIPIENT | SUBJECT | ATTACHMENT |
| --- | --- | --- | --- | --- | --- | --- |
| High | Jun, 13, 2021 | 24.213.228.54 | trenton@tritowncomputers.com | lars@letsdefend.io | RE: Meeting Notes | Yes |

## Investigation Process
### 1. Initial Triage - Identifying "red flags"

First, the email is examined in its entirety.<br><br>
<img width="953" height="393" alt="image" src="https://github.com/user-attachments/assets/ba8fca22-b5e8-420d-88a5-f03bd49ab6bc" />
<br>

        From first glance, several red flags are raised:
               - Unusual wording within the message body: "Please inspect your docs as one document"
               - Password inclusion with the attachment

Next, MXToolbox is used to obtain an email domain health report of the sender's address *@tritowncomputers.com*.<br><br>
<img width="1381" height="578" alt="image" src="https://github.com/user-attachments/assets/686bf6c0-5168-4b03-bda8-0d6347015823" />
<br><br>
            
        MX Toolbox SuperTool delivered a Domain Health Report suggesting:
               - 7 total problems, 7 warnings
               - 10 total Mail Server tests failed
               - 1 Blacklist error
<br>

While not outright suggesting a malicious sender, it gives reason to warrant suspicion.
        
### 2. Attachment Analysis - Utilizing HybridAnalysis

Attachment *11f44531fb088d31307d87b01e8eabff* was a zip file containing 3 files: *iroto1.dll*, *iroto.dll*, and *research-1646684671.xls*.
<br>Each file was analyzed by third-party sandbox HybridAnalysis.<br><br>

#### *11f44531fb088d31307d87b01e8eabff.zip* Analysis
<img width="1204" height="578" alt="image" src="https://github.com/user-attachments/assets/fe6750fe-01e0-4bd1-9e76-59af0522432a" />
<br><br>

      HybridAnalysis flagged the attachment hash as:
               - malicious (6/6 vendors)
<br>

#### *research-1646684671.xls* Analysis
<img width="1196" height="686" alt="image" src="https://github.com/user-attachments/assets/c7626e99-2c68-4ef5-a3b5-4df69dbf7683" />
<br><br>

      HybridAnalysis flagged the attachment hash as:
               - malicious (14/19 vendors)
<br>

#### *iroto.dll* Analysis

<img width="1199" height="659" alt="image" src="https://github.com/user-attachments/assets/4a6270e9-9e82-483a-8b5f-ea1b60f1ff2b" />
<br><br>

      HybridAnalysis flagged the attachment hash as:
               - malicious (6/8 vendors)
<br>

#### *iroto1.dll* Analysis

<img width="1206" height="587" alt="image" src="https://github.com/user-attachments/assets/1f4cb705-274d-4d3a-a585-eb1f6a77beee" />
<br><br>

      HybridAnalysis flagged the attachment hash as:
               - malicious (8/8 vendors)
<br>

The zip and all three files contained within it were independently identified as malicious by HybridAnalysis.

### 3. Endpoint Verification - Execution check

Endpoint Security was used from recipient Lars to identify the destination machine and history.<br><br>

<img width="1394" height="395" alt="image" src="https://github.com/user-attachments/assets/dc7cd565-0a48-4d39-ba02-5742e0c5b531" />
<br><br>

      The destination machine was LarsPRD.
<br>

<img width="744" height="359" alt="image" src="https://github.com/user-attachments/assets/ea84494a-09ea-45f5-a156-ee29c3a43b32" />
<br><br>

      The terminal history shows both iroto.dll and iroto1.dll registration.
<br>

<img width="878" height="260" alt="image" src="https://github.com/user-attachments/assets/dae62a7f-b208-4635-a5c4-5d9121a4e0a7" />
<br><br>

      Process history shows regsvr32.exe registering iroto.dll.
<br>

## Findings
The alert was confirmed as a **true positive**. All three files contained within the zip attachment were flagged as malicious by HybridAnalysis, and the sender's domain showed multiple health and blacklist issues. Endpoint analysis confirmed the attachment was opened and executed, with terminal and process history showing active DLL registration via regsvr32.exe on LarsPRD. The email reached the recipient and the affected machine should be isolated and the malicious files remediated.

## Skills Demonstrated
- Phishing Email Investigation
- Malware triage
- Endpoint investigation
- Attachment Analysis (HybridAnalysis)

## Practice Project Source
[SOC146 - Phishing Mail Detected - Excel 4.0 Macros | LetsDefend](https://app.letsdefend.io/monitoring?channel=investigation&event_id=93)

***
