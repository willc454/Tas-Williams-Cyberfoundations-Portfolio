# Week 7 Lab 01 — Meet the Guard

**Student Name:**  
**Date Completed:**  
**Module:** 2 — Networking & Cloud Foundations | **Week:** 7  
**Submission Path:** `week-07/labs/lab-01-meet-the-guard.md`

> ## Cloud Heights Protected-Rules Safety Rule
> The baseline rules at priorities **100** (`allow-ssh-from-bastion`), **110** (`allow-icmp-intra-vnet`), and **120** (`deny-ssh-student-subnet`) are protected. **Never modify, delete, replace, or use them as troubleshooting targets.** Create or edit student rules only in priorities **200–999**. A mistake in your student range is recoverable and is not a grading penalty when you diagnose it honestly.

> **Evidence safety:** Never include a Cloud Heights password or Bastion shareable URL. Crop browser address bars and login information before committing screenshots.

---

## Mission

Inspect the existing NIC-level security rules on your assigned VM without changing anything. Your goal is to recognize the guardrails, separate protected rules from student-editable space, and map each visible field to the firewall mental model.

## What You Already Know

A network security rule is a decision about traffic. Rules are evaluated from the lowest priority number to the highest, and the first matching rule wins. Inbound and outbound traffic use separate ledgers. A configured service, a security rule, a test result, and an evidence screenshot answer different questions.

## Lab Environment / Pre-Lab Check

| Component | Details |
|---|---|
| Environment | My Lab Environment → Cloud Heights → Security Rules |
| Change level | Read-only; do not add, edit, or delete rules |
| Expected protected rules | 100 `allow-ssh-from-bastion`; 110 `allow-icmp-intra-vnet`; 120 `deny-ssh-student-subnet` |
| Time | 15–20 minutes |

- [ ] I am using my assigned `cf-student-XX` VM through the CyberFoundations Lab Portal.
- [ ] The VM shows **Running**.
- [ ] I can identify the three protected baseline rules at priorities 100, 110, and 120.
- [ ] I understand that my editable priority range is 200–999.

### Cloud Heights Idle Stop

Cloud Heights may warn you that the VM is idle. Return to the Lab Portal and choose **I'm still working** if you are active. If the VM is stopped or deallocated, it was not deleted: restart it from **My Lab Environment**. Your disk files and saved configuration remain.

## Predict First

Before opening the rule list, predict why a course environment would protect its access and safety rules from student edits.

```text
(write your prediction here — 2 or 3 sentences)
```

## Guided Steps

### Step 1 — Open the Guard Post

In **My Lab Environment**, open your Cloud Heights controls and find **Security Rules**. Do not use the Azure Portal.

### Step 2 — Inventory the Baseline

Record each protected rule exactly as shown.

| Priority | Rule name | Direction | Protocol | Source | Destination/port | Action | Protected? |
|---|---|---|---|---|---|---|---|
| 100 |  |  |  |  |  |  | Yes |
| 110 |  |  |  |  |  |  | Yes |
| 120 |  |  |  |  |  |  | Yes |

### Step 3 — Map the Fields

For each field, write the question it answers: direction, source, source port, destination, destination port, protocol, action, and priority.

```text
(write your field-to-question map here)
```

## Stop & Check

- Can you edit a protected rule? You should not be able to.
- Where may student rules be created? Priorities 200–999.
- Which value is read first: 200 or 900? The lower number, 200.

## Test

This is a read-only lab. Your test is visual verification: confirm the three protected rules remain present and that no student rule was created.

## Capture Evidence

Capture the complete visible baseline rule list. If it does not fit in one image, use two clearly named images and explain why.

## Explain

In 3–4 sentences, explain how protected baselines and a separate student priority band reduce accidental lockout while still allowing meaningful practice.

```text
(your explanation here)
```

## Required Evidence

Save screenshots in `assets/screenshots/week-07/`:

- `week07-lab01-security-rules-baseline.png`

Open each image at full size before submission. Confirm that no password, Bastion shareable URL, browser address bar, or unrelated private information is visible.

## Analysis Questions

**Analysis Question 1.** Why is a priority number part of rule behavior rather than just an identifier? (Minimum 3 sentences.)

```text
(your answer here)
```

**Analysis Question 2.** Explain the difference between a rule being visible, editable, and protected. (Minimum 3 sentences.)

```text
(your answer here)
```

**Analysis Question 3.** Which baseline rule protects your current administrative path, and why must it never be used as a troubleshooting target? (Minimum 3 sentences.)

```text
(your answer here)
```

## Submission Checklist

- [ ] Baseline inventory completed without changes
- [ ] All visible rule fields mapped to their security questions
- [ ] Editable range 200–999 identified
- [ ] `week07-lab01-security-rules-baseline.png` captured
- [ ] Protected priorities 100, 110, and 120 were not changed.
- [ ] Every rule I created or edited used priority 200–999.
- [ ] No password, Bastion URL, or browser address bar appears in my files.
- [ ] This worksheet is committed to `week-07/labs/lab-01-meet-the-guard.md`.

## GitHub / Lab Portal Submission

1. Open **Week 7 → Lab 01: Meet the Guard** in the CyberFoundations Lab Portal.
2. Complete every worksheet field and confirm the listed evidence filenames.
3. Upload screenshots to `assets/screenshots/week-07/`.
4. Confirm your portfolio repository is connected, then choose **Submit to GitHub**.
5. Open the committed worksheet and each image on GitHub to verify formatting, legibility, and redaction.

*CyberVisionaries Institute · CyberFoundations · Tier I*
