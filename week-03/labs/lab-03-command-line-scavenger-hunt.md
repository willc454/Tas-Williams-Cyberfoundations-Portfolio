# Week 3 Lab 03 — Command Line Scavenger Hunt (CLI Simulator)

**Student Name:** Catasia Williams

**Date Completed:** August 1, 2026

**Module:** 1 — Digital Infrastructure & CLI | **Week:** 3  
**Submission Path:** `week-03/labs/lab-03-command-line-scavenger-hunt.md`

---

## Overview

Labs 01 and 02 walked you through each command step by step. This lab is Week 3's wrap-up challenge: a deeper, more independent folder structure with three hidden files to track down, using the navigating and reading commands from Lessons 3A/3B, the creating and organizing commands from Lesson 3C, and your own judgment about when to ask for help. There's less hand-holding here on purpose — this is your chance to prove to yourself that the blinking cursor from the start of Lesson 3A doesn't intimidate you anymore.

**Nothing here can break anything real.** Same consequence-free CLI Simulator as Labs 01 and 02. Getting "lost" in the folder tree costs you nothing but a few extra `cd` moves.

---

## Lab Environment / Pre-Lab Check

| Component | Details |
|---|---|
| Environment | CyberFoundations CLI Simulator (browser-based, inside the Lab Portal) |
| Shell | Your choice — bash or PowerShell |
| Prerequisite | Labs 01 and 02 completed |

**Before you start:** log into the Lab Portal, open **Week 3 → CLI Simulator**, and load the **"Foundry District Archive Room"** scenario. This tree goes several folders deeper than Labs 01 and 02, and includes a few similarly-named folders on purpose — read carefully before you `cd` into anything.

---

## Part A — The Hunt

Find all three of the following, hidden at different depths in the Archive Room tree:

- A file related to a **shift log**
- A file related to a **maintenance note**
- A file related to a **supply inventory**

For each one, use `pwd`/`Get-Location` and `ls`/`dir` as many times as you need while you search, then record the **full path** once you find it.

Shift log file — full path once found:

```
archivist@archive-room:/home/archivist/operations/ops-log$ ls

```

Maintenance note file — full path once found:

```
archivist@archive-room:/home/archivist$ ls records/records-2025
```

Supply inventory file — full path once found:

```
archivist@archive-room:/home/archivist$ ls records/records-2024
```

---

## Part B — Read and Report

For each of the three files you found in Part A, use `cat`/`type` to read it and record what it says.

Shift log contents:

```
Shift Log - Foundry District Archive Room
07:00 - Archive opened, no incidents overnight.
15:00 - Routine filing complete.
```

Maintenance note contents:

```
Maintenance Note - Conveyor belt 3 serviced, next check due in 90 days.
```

Supply inventory contents:

```
Supply Inventory - Q4 2024
Gloves - 400 units
Masks - 250 units
Tape - 60 rolls
```

---

## Part C — Organize Your Findings

Now that you've located and read all three files, clean up after yourself the way a professional would — don't leave your findings scattered across the tree.

### Step 1 — Create a Sorted-Findings Folder

Create a new folder called `sorted-findings` in your home directory.

Command you ran:

```
archivist@archive-room:/home/archivist$ mkdir sorted-findings
```

### Step 2 — Move All Three Files Into It

Move the shift log, maintenance note, and supply inventory files — the same three you found in Part A — into `sorted-findings`.

Commands you ran:

```
archivist@archive-room:/home/archivist$ mv operations/ops-log/shift-log.txt sorted-findings/
archivist@archive-room:/home/archivist$ mv records/records-2025/maintenance-note.txt sorted-findings/
archivist@archive-room:/home/archivist$ mv records/records-2024/supply-inventory.txt sorted-findings/
```

### Step 3 — Confirm the Move

List the contents of `sorted-findings` to confirm all three files are now there.

Command you ran:

```
*The first set of commands below was before the CLI Simulator was modified. The second set is after the modification.
archivist@archive-room:/home/archivist$ ls
README.md  operations  records  sorted-findings
archivist@archive-room:/home/archivist$ ls sorted-findings
maintenance-note.txt  shift-log.txt

After CLI Simulator modification: 
archivist@archive-room:/home/archivist$ mv records/records-2024/supply-inventory.txt sorted-findings/
archivist@archive-room:/home/archivist$ ls

```

Output:

```
✓ All three filed and confirmed.
```

---

## Part D — When You Get Stuck

At some point in the Archive Room, you'll likely run across a command or folder name you don't immediately recognize.

### Step 1 — Ask the Terminal

When that happens, use `--help`, `man`, or `Get-Help` instead of guessing. Record what you looked up and what you learned.

Command or term you looked up:

```
I used --help to look up the command chmod. I learned that the command is an access control command. It is designed to control who has access to read, write, or run a file. 
```

What the help text (or the folder's contents) told you:

```
The help text told me what the chmod command is desgined for. The command is desgined to control access to a file. 
```

### Step 2 — Describe a Wrong Turn

Everyone takes at least one wrong turn in a tree this size. Describe one moment you ended up somewhere unexpected, and how you used `pwd`/`Get-Location` and `cd ..` to recover.

```
I opened the same file twice and I already had a lot of command lines which was making my work cluttered. I used 'cd..' to go back because I already knew exactly what I needed to do. Doing this allowed me to have a better flow of the information. 
```

---

## Analysis Questions

### Analysis Question 1

Which of the three files in Part A took the longest to find, and what was it about the tree's structure (depth, similarly-named folders, etc.) that made it harder?

```
The maintenance note may have been the longest to find because of depth and similarly-named folders. The mainteance record could have easily been with the 1st or 2nd record folder. I needed to open both folders in order to find the maintenance note. 
```

### Analysis Question 2

Compare how you felt starting this lab to how you felt at the very start of Lesson 3A, looking at a blank blinking cursor for the first time. What changed?

```
Starting this lab truly felt overwhelming. I only used software programs on computers and never had to deal with any of the backend stuff. Anything related to the innerworkings of the computer was always related to something being wrong/broken which typically isn't a good feeling. By the end of the assignment, I was more confident about utilizing the computer in different manner. 
```

### Analysis Question 3

Week 4 moves from managing your own files to controlling who's allowed to do what to them — permissions — plus your first look at what a virtual machine is. Based on everything you've practiced this week, what's one thing you're curious about or looking forward to?

```
I am curious just to learn about what a virtual machine is. Also, I have always been curious about how computers are programmed so it would be very interesting for me to learn about permissions and how the computer is able to differentiate who to give access to. 
```

---

## Submission Checklist

- [x] All three target files located, with full paths recorded (Part A)

- [x] All three target files read and their contents recorded (Part B)

- [x] `sorted-findings` folder created and all three files moved into it, confirmed with a listing (Part C)

- [x] At least one command or term looked up with `--help`/`man`/`Get-Help`, with what you learned recorded (Part D, Step 1)

- [x] One wrong-turn moment described, including how you recovered (Part D, Step 2 — minimum 2 sentences)

- [x] All three Analysis Questions answered (minimum sentence counts met)

- [x] This file is committed to your portfolio repo at `week-03/labs/lab-03-command-line-scavenger-hunt.md`

---

## GitHub Commit Subsection

Same mechanism as Labs 01 and 02: fill out this lab's worksheet in the **CyberFoundations Lab Portal** (Week 3 → Lab 03) and click **Submit to GitHub** — the Portal commits the completed file to `week-03/labs/lab-03-command-line-scavenger-hunt.md` automatically. No manual typing or commit needed.

**📌 Optional:** a CLI Simulator session screenshot can be added the same way as Labs 01 and 02 — upload to `assets/screenshots/week-03/`, then right-click the uploaded image and choose **Copy image address**/**Copy Image Link** to embed it — but it isn't required and won't affect your grade.

---

*CyberVisionaries Institute · Cyber Foundations · Tier I*
