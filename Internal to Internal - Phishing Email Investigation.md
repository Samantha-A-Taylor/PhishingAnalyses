***
# Phishing Email Investigation: Internal to Internal

## Summary
Investigated a 

## Alert Details

| SEVERITY | DATE | SMTP ADDRESS | SENDER | RECIPIENT | SUBJECT | ATTACHMENT |
| --- | --- | --- | --- | --- | --- | --- |
| Medium | Feb, 07, 2021 | 172.16.20.3 | john@letsdefend.io | susie@letsdefend.io | Meeting | No |

## Investigation Process
### 1. Initial Triage - Identifying "red flags"

First, the email is examined in its entirety.<br><br>
<img width="589" height="268" alt="image" src="https://github.com/user-attachments/assets/07f1bdbc-879f-4bf8-af2d-14531dc4fa7c" />
<br>

        From first glance, no red flags are raising:
               - Subject line is non-urgent
               - No "call to action" (CTA)
               - There is no attachment, or links to be found in images or elsewhere
<br>

## Findings
The alert was confirmed as a **false positive**. There was no attachment, link, image, or call-to-action. Could possibly be conversational baiting, but as the finding submittion came back as correct, unlickly.

## Skills Demonstrated
- Phishing Email Investigation

## Practice Project Source
[LetsDefend's SOC120 - Phishing Mail Detected - Internal to Internal](https://app.letsdefend.io/monitoring?channel=investigation&event_id=52) 

***
