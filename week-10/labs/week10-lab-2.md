# Week 10 — Lab 2: Prioritize Risks and Recommend Controls

Learner: Catasia Williams
Case: Cloud Heights Family Clinic — Risk & Threat Investigation
Scenario date: Friday 13 March 2026, 09:00 (clinic local time)
Report generated: 2026-10-04T00:02:33.289Z
Study mode: Independent (hints hidden)

Completion checklist: all required work for Lab 2 is present.

## Risk ratings

| ID | Asset | Likelihood | Why | Impact | Why | Score (L x I) | Classroom band |
| --- | --- | --- | --- | --- | --- | --- | --- |
| SC-01 | Appointment scheduling account | 3 | The likelihood is high because the threat exposure is routine \- the employees receive the phishing emails "most weeks", the weakness is present in the evidence, and there is no evidence of implementation of a control that would reliably stop the threat. | 3 | The impact is high because if the threat/event occurred clinic operations could stop, patient data could be exposed or lost, and recovery could be slow, uncertain, and  untested. | 9 | High (6–9) |
| SC-02 | Patient records application | 3 | The likelihood is high because the exposure is routine, the weakness is present in the evidence, and nothing found so far would reliably stop it. The employees use a shared account to access patient records everyday, the evidence presents several weaknesses, and no control was implemented to rectify this. | 2 | The impact is medium because the records application contains sensitive and confidential patient information. Unauthorized or inappropriate access could expose or alter patient records, and the shared account makes it difficult to determine who accessed them. Recovery and investigation could therefore be difficult. Clinic operations could be affected but may not need to stop completely. | 6 | High (6–9) |
| SC-03 | Staff laptops | 3 | The likelihood is high because the exposure is routine \(two laptops have gone 90 days without security updates and are used daily for email and the records application\). The evidence also shows a laptop signed into the records application with the screen unlocked and no one present in a shared workspace accessible from a patient corridor. There is no identified control or assigned responsibility ensuring the laptops are updated or preventing unauthorized access when a laptop is left unlocked. Also, there is no assigned responsibility to ensure the laptops are update; staff who utilize the respective laptop continuously postpone the update and there is no IT staff assigned to ensure the updates are installed. | 3 | The impact is high because because the evidence suggests there was possibly a threat event that occurred. That event or other events could cause clinic operations to stop, patient data could be exposed or lost, and recovery could be slow, uncertain, and untested. | 9 | High (6–9) |
| SC-04 | Public information website | 3 | The likelihood is high because exposure is routine, the weakness is present in the evidence, and nothing found so far would reliably stop it. The certificate expires in 7 days, renewal is manual, the last two renewals occurred only after browser warnings appeared, and there is no calendar reminder or named owner. The evidence does not identify an existing control that reliably ensures renewal before expiration. | 1 | The impact is low because  clinic operations could continue, sensitive data is not affected because the website only contains public information and restoration of the certificate could happen  quickly. An expired certificate could cause browser warnings and discourage visitors, but the evidence does not indicate exposure or loss of sensitive patient information. | 3 | Medium (3–4) |
| SC-05 | Backup archive | 3 | The likelihood is high because exposure is routine, the weakness is present in the evidence, and nothing found so far would reliably stop it. There is one external backup drive, the last successful backup was 14 days ago, the evidence suggests that  six backups were completed with errors, and the clinic has never tested restoration of the backups. The external backup drive is permanently attached to a workstation. In addition, there is no second drive, offsite copy, or cloud copy. No existing protection provides a demonstrated alternative recovery method or solutions for any of the other threats. | 3 | The impact is high because clinic operations could stop, patient data could be lost or hard to recovery. If the clinic needed to restore data and the backup failed, clinic and patient information could be lost. Operations could be disrupted, and recovery could be slow or uncertain because restoration has never been tested and there is no alternate backup. The physical location of the external drive exposes it to physical damage and allows problems affecting the workstation to potentially affect the backup drive. | 9 | High (6–9) |

Bands (1–2 low, 3–4 medium, 6–9 high) are a classroom teaching aid, not a compliance standard.

## Priority risks
- SC-03 — Staff laptops
- SC-05 — Backup archive

**Why these:** Risk 3 \(SC-03\) - Staff laptops and Risk 5 \(SC-05\) - Backup archive should receive priority because the consequences are greatest.

## Recommended controls
### SC-03
- **Control:** Implement an updated security update policy that requires an assigned responsibility role to one person to monitor and remediate compliance of laptop security and implement.
- **How it helps:** This makes the event less likely, less damaging and easier to identify because there will be more oversight of the security update process.
- **Risk remaining afterwards:** Residual risk remains because a vulnerability could still be missed, an update could fail, or an authorized user could still make a mistake or allow unauthorized access. The control reduces the risk but does not eliminate it.

### SC-05
- **Control:** Implement procedures for backups to include a safer location for the backup drive, creation of a second backup copy on a separate drive to be stored offsite, and  schedule regular restore tests to confirm that the backup can actually be recovered.
- **How it helps:** The additional offsite backup reduces the impact of a failure, loss, or damage to the primary backup drive. Regular restore testing makes it easier to detect a backup that cannot be restored before the clinic needs it. A different location for the backup drive can reduce the chance of damage.
- **Risk remaining afterwards:** Residual risk remains because a backup could still fail or be unavailable when it is needed.

## Owner briefing
Word count: 552 (guide: 100–150)

The review identified five findings. The findings are detailed below, along with corresponding recommendations to reduce the associated risks.

Risk 1 \(SC-01\)  - Appointment scheduling account:
Front desk staff are receiving repeated suspicious emails that request usernames and passwords for the scheduling account. Improper access to the scheduling account could compromise patient confidentiality, affect integrity of information, and disrupt access to the scheduling system.
Recommendation - The Practice Manager should instruct staff not to respond to suspicious emails or provide usernames, passwords, or other login information. The clinic should also establish a process for reporting suspicious emails to the IT contractor for them to be addressed.

Risk 2 \(SC-02\) - Patient records application:
Four employees share one account username and password to access the patient records. Having a shared account makes it difficult to identify which employee accessed patient information. Also, the password has not been changed for 8 months.
Recommendation - The IT Contractor should assign each employee a dedicated account with unique login credentials and retire the current username and password. The passwords on all accounts should be changed more frequently.

Risk 3 \(SC-03\) - Staff laptops:
Security updates have not been installed on two laptops \(the other 7 laptops have been updated\). The updates have postponed by the employees using the laptop and no one is assigned the task of overseeing compliance of this. In addition,  a laptop that appeared to capture a screenshot, but no one was sitting at the desk. The laptop was located near a corridor used by patients.
Recommendation - The IT Contractor should assign someone responsibility for monitoring and enforcing compliance of the updates. Employees should be briefed on the importance of installing security updates when prompted and locking their laptops whenever they step away.

Risk 4 \(SC-04\) Public Information website:
The website security certificate expires in 7 days, and  there is no process in place to ensure the certificate is renewed before it expires. The certificate has expired at least twice in the past and the issue was only discovered after an employee noticed a warning sign on the website. Although the website does not host sensitive or confidential patient information, an expired certificate could cause visitors to receive a browser warning indicating that the site's certificate is not trusted. This could discourage visitors from trusting the clinic's website.
Recommendation - The Practice Manager should assign the IT Contractor responsibility for monitoring and renewing the website certificate before expiration to ensure future renewals are completed on time.

Risk 5 \(SC-05\) Backup Archive:
Restoring the backup has never been attempted so it is unknown whether the backup can be successfully restored. The last successful backup was on February 27, 2026, and since then there have been six job entries indicating that there were errors with the backups. There are also no additional copies of the backup files. The external backup drive is permanently connected to the reception workstation desk which, exposes it to potential physical damage and the things that happens on the workstation could also affect the backup drive.
Recommendation - Implement procedures for backups that include storing the external drive in a safer location, creating a second backup copy on a separate drive stored offsite, and  scheduling regular restore tests to confirm that the backup data can actually be recovered and used.
