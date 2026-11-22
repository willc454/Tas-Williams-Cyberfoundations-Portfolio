# Lab 06 — Identity Investigation + Case File (Deliverable 4)

**Learner:** (name not entered)  
**Attempt:** attempt F6FAF6 · seed chic-w11-v1 · state revision 34 · text revision 431

> Training simulation — fictional Cloud Heights accounts and resources. Your actions change only your Week 11 learning attempt. This is not a live AD domain, Microsoft Entra tenant or Azure subscription.

## Objective

Correlate historical logs and assemble the Cloud Heights IAM Investigation Case File — Portfolio Deliverable 4.

## My answers

### Starting hypothesis before filtering

**Optional practice**

_Optional practice not completed._

## IAM Investigation Case File (Portfolio Deliverable 4)

_This is a technical case file. Week 12 uses it as source material to produce the professional Technical Incident Report and Executive Summary and to finalize and present the portfolio._

### 1. Scope and environment

I investigated Finley's account because he was terminated to ensure access was disabled and revoked.

### 2. Identity/directory trace and AD DS–Entra–Azure comparison

One user can have several accounts, be associated with different groups, hold various roles, and have varying permissions across the directory. In this environment, some users had both a CL account and AD account. Blair is a prime example. Blair can sign-in to their account but not be able to access records where permission was not assigned based on the associated account privileges.

### 3. Blair authentication-versus-authorization investigation

The sign-in records show Blair attempted to sign-in but could not access the account because the first authentication failed.

### 4. Directory administration and sensitive-action verification

During directory administration, I performed  a test sign-in to ensure the account was indeed accessible.

### 5. Three job-role configurations, scopes and business rationales

The role was scoped for access to the account on the attempted sign-in.

### 6. Access test matrix and temporary grant/revoke evidence

I tested access by simulating a test sign-in.

### 7. ABAC current-policy and what-if findings

The policy test showed that the account was accessible.

### 8. Joiner/mover/leaver and unverified-reset decisions

For the lifecycle requests, I checked sign-in access.

### 9. Historical identity findings (see findings below)

The historical findings are supported by the records.

#### Finding 1: Account Disabled-Employee Termination

- **Events:** S012
- **Observation:** Drew's account is disabled.
- **Hypothesis:** The account needs to be disabled.
- **Supported conclusion:** Confirmation that the account is disabled.
- **Uncertainty / missing information:** The reason the account was disabled.
- **Next action:** Find out why the account was disabled.
- **Priority:** high — Ensure the correct/accurate access.

#### Finding 2: Authentication Issues

- **Events:** S009, A002
- **Observation:** The records show that initial sign-in failed (not authenticated). The re-attempt authenticated.
- **Hypothesis:** One possible explanation is the wrong password was entered therefore the account could not be authenticated.
- **Supported conclusion:** Based on the available records, the password entered failed. On the second attempt, the password was authenticated.
- **Uncertainty / missing information:** The available evidence does not establish what the actual password is and does not determine what privileges are associated with the account.
- **Next action:** It should be ensured that the account holder knows the correct password and  has access to the appropriate privileges.
- **Priority:** low — No access issues were reported. A review of the associated access privileges can avoid any potential issues.


### 10. Sign-in/audit correlation and one benign/ambiguous comparison

The records demonstrates the actions taken on all accounts.

**Benign/ambiguous comparison** (S002, S003): There is an initial concern that Blair's password did not authenticate. However, the second time Blair entered their password, it authenticated. These records are not enough to claim compromise, malicious activity, or any other unsupported conclusions because no additional evidence, issues, or concerns arose from this incident.

**Live simulator chain (current attempt, not historical):** I removed Finely from the group, disabled his account, and revoked the session.  Record LA-F6FAF6-27-1 recorded that Finley was removed from the group. Record LA-F6FAF6-28-1 shows that the account status changed to disabled. Record LA-F6FAF6-29-1 shows that the session was revoked.

### 11. Preliminary response/remediation recommendations, priority and uncertainty

The next action I recommend checking is the accuracy of the account holder's password.

### 12. Evidence index notes

The case file references that sign-in attempts and when they failed and succeeded authentication.

### Explicit simulation/environment limitations

It can not tell if the password was indeed entered wrong or if there was an issue with the system.

### Earlier labs

- [Lab 01](lab-01-identity-directory.md)
- [Lab 02](lab-02-authentication-vs-authorization.md)
- [Lab 03](lab-03-build-and-manage-directory.md)
- [Lab 04](lab-04-least-privilege-challenge.md)
- [Lab 05](lab-05-joiner-mover-leaver.md)

## Evidence

- **E17 · EV-F6FAF6-008** — Two distinct findings with raw-event references and correlation (captured at revision 34)  
  _What this proves:_ The selected record support my observation that Drew's account is disabled.  
  See [evidence index](evidence/week11-evidence-index.md#ev-f6faf6-008)
- **E17 · EV-F6FAF6-009** — Two distinct findings with raw-event references and correlation (captured at revision 34)  
  _What this proves:_ The selected record support my observation that Drew's account is disabled.  
  See [evidence index](evidence/week11-evidence-index.md#ev-f6faf6-009)
- **E18 · EV-F6FAF6-010** — Benign/ambiguous comparison (captured at revision 34)  
  _What this proves:_ Drew's account is disabled.  
  See [evidence index](evidence/week11-evidence-index.md#ev-f6faf6-010)
- **E17 · EV-F6FAF6-011** — Two distinct findings with raw-event references and correlation (captured at revision 34)  
  _What this proves:_ The selected records show when Blair's password authentication failed and when it was successful. These records support my observation that the incorrect password was entered the first time. The evidence does not determine what the passwords are.  
  See [evidence index](evidence/week11-evidence-index.md#ev-f6faf6-011)
- **E18 · EV-F6FAF6-012** — Benign/ambiguous comparison (captured at revision 34)  
  _What this proves:_ The selected records show the account holder was removed from the group, the account was disabled, and access was revoked.  
  See [evidence index](evidence/week11-evidence-index.md#ev-f6faf6-012)
- **E19 · EV-F6FAF6-013** — Completed case file / versioned export (captured at revision 34)  
  _What this proves:_ The Case File references these records to support that Drew's account was disabled and there was an unsuccessful authentication on Blair's account followed by a successful authentication (as well as other action on Blair's account).  
  See [evidence index](evidence/week11-evidence-index.md#ev-f6faf6-013)
