***
# Phishing Email Investigation: Internal to Internal

## Summary
Investigated a low-complexity, medium-severity phishing alert involving an internal-to-internal email with no attachment, no links, and no calls to action. Examined the email in full and found no indicators of malicious intent. The alert was closed as a false positive, with no further action required.

## Alert Details

| SEVERITY | DATE | SMTP ADDRESS | SENDER | RECIPIENT | SUBJECT | ATTACHMENT |
| --- | --- | --- | --- | --- | --- | --- |
| Medium | Feb, 07, 2021 | 172.16.20.3 | john@letsdefend.io | susie@letsdefend.io | Meeting | No |

## Investigation Process
### 1. Initial Triage - Identifying "red flags"

First, the email is examined in its entirety.<br><br>
<img width="589" height="268" alt="image" src="https://github.com/user-attachments/assets/07f1bdbc-879f-4bf8-af2d-14531dc4fa7c" />
<br>

        From first glance, no red flags are raised:
               - Subject line is non-urgent
               - No call-to-action (CTA) present within the message body
               - No attachment, embedded links, or suspicious images found
<br>

## Findings
The alert was confirmed as a **false positive**. The email contained no attachment, link, image, or call-to-action, and originated from a recognized internal address within the same domain. While conversational baiting was considered as a possibility, the brevity and neutral tone of the message, combined with a correct finding submission, made this unlikely. No further escalation or remediation was warranted.

## Skills Demonstrated
- Phishing Email Investigation
- False positive identification

## Practice Project Source
[LetsDefend's SOC120 - Phishing Mail Detected - Internal to Internal](https://app.letsdefend.io/monitoring?channel=investigation&event_id=52) 

***
