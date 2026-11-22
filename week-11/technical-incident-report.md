# Cloud Heights Identity Investigation — Technical Incident Report

> Fictional training scenario: Cloud Heights Identity Center (simulated). No real organisation, people or systems.

- Analyst: Catasia Williams
- Source case file: [../week-11/labs/lab-06-identity-investigation-case-file.md](../week-11/labs/lab-06-identity-investigation-case-file.md)
- Evidence index: [../week-11/labs/evidence/week11-evidence-index.md](../week-11/labs/evidence/week11-evidence-index.md)

## 1. Purpose / incident context
This report documents the investigation of Drew's account status.

## 2. Scope
The investigation only covered the logged evidence representing the status (disabled) of Drew's account. It does not cover anything else regarding Drew's account.

## 3. Evidence reviewed
The following records were used: sign-in logs.

Evidence IDs (EV-…) and event IDs (S…, A…, C…) refer to records in my Week 11 evidence index; full evidence is not duplicated here.

## 4. Timeline
The record shows that Drew's account was disabled.

## 5. Findings
### Finding 1 (RF1) — confidence: confirmed

The records show the account was disabled.

- Evidence / events: S012
- Uncertainty: The available evidence does not establish why the account was disabled and whether disabling the account worked as intended.

### Finding 2 (RF2) — confidence: confirmed

Based on the available records, the password entered failed. On the second attempt, the password was authenticated.

- Evidence / events: S002, S003
- Uncertainty: The records do not show why the account was disabled or whether a test was run to ensure that the actions taken to disable the account worked.

## 6. Impact / risk
The evidence shows that Drew's account was disabled therefore, Drew should no longer be able to access the account.

## 7. Recommendations / next actions
### Recommendation 1 (R1)

- **What:** At 2026-09-21T14:20:00Z, this account was disabled: drew@cvi-training.example. Within 24 hours the IAM team will run a test on the account to ensure that the account is disabled, can no longer be accessed, and document the reason why the account was disabled.
- **Who:** IAM
- **Why:** This action lowers the risk of unauthorized access.
- **Priority:** high
- **Timeframe:** within 24 hours
- **Linked findings:** RF1
- **Success measure:** Run a check to ensure the actual is disabled, as intended.

## 8. Limitations / unknowns
This investigation is limited because it does not provide a test of the account to ensure that Drew can no longer access the account.

## 9. Conclusion
Based on the available records, once an account is disabled to prevent the respective individual from accessing it again, a test should be done to ensure the account can not be accessed by that individual.
