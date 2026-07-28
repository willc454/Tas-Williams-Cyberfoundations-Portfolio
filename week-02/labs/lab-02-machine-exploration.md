# Week 2 Lab 02 — Explore Your Own Machine (Real Specs & Live Activity)

**Student Name:** Catasia Williams

**Date Completed:** July 26, 2026

**Module:** 1 — Digital Infrastructure & CLI | **Week:** 2  
**Submission Path:** `week-02/labs/lab-02-machine-exploration.md`

---

## Overview

Lab 01 got you diagramming how hardware, OS, and software interact — in theory. This lab makes it real, in one sitting. First, you'll look up your own machine's actual specs (OS version, RAM, storage) using its built-in settings screens. Then you'll open Task Manager (Windows) or Activity Monitor (Mac) and watch those same hardware and software layers working together live — CPU usage, memory usage, and real running processes — and connect what you see back to your Lab 01 diagram.

**No terminal or command line is required this week** — that starts in Week 3. Settings screens, Task Manager, and Activity Monitor are all point-and-click tools.

---

## Lab Environment

| Component | Details |
|---|---|
| Environment | Your own computer (Windows or Mac) — no VM, no cloud, no install needed |
| Required Materials | Your computer's built-in Settings/About screen; Task Manager (Windows: `Ctrl+Shift+Esc`) or Activity Monitor (Mac: `Cmd+Space`, then type "Activity Monitor") |

**Prerequisite:** Lab 01 completed — you'll reference your diagram in this lab's Analysis Questions. Fill out this worksheet here in the Lab Portal, then hit Submit to commit it directly to your repo at `week-02/labs/lab-02-machine-exploration.md`.

---

## Part A — Find Your Real Specs

**Before you start:** here's what to expect so you don't second-guess yourself. On Windows, you're looking for a page titled **About**, reached via **Settings → System → About**, listing your device specs under "Device specifications." On Mac, you're looking for a window titled **About This Mac** (click the Apple menu, top-left corner), with an Overview tab listing your chip, memory, and macOS version. If what's on your screen doesn't roughly match that, you're in the wrong menu — try again before recording anything below.

### Step 1 — Find Your OS Version

Open your computer's system settings (Windows: **Settings → System → About**. Mac: **Apple menu → About This Mac**) and find the exact operating system name and version you're running.

**OS and version:**

```
Windows 11 Home/Version 24H2
```

### Step 2 — Check Your Installed RAM

On the same settings screen, find how much RAM (memory) is installed on your computer.

**Installed RAM:**

```
16.0 GB (15.7 GB usable)
```

### Step 3 — Check Your Available Storage

Find your computer's total storage capacity and how much is currently free (Windows: **Settings → System → Storage**. Mac: **About This Mac → Storage**).

**Total storage:**

```
453GB
```

**Free storage:**

```
325GB
```

---

## Part B — Watch It Live

Your Part A numbers are a snapshot. This part shows those same layers actually working, moment to moment.

### Step 1 — Open Task Manager or Activity Monitor

Windows: press `Ctrl+Shift+Esc`. Mac: press `Cmd+Space`, type "Activity Monitor," and press Enter.

### Step 2 — Find the Performance / CPU Tab

Windows: click the **Performance** tab. Mac: click the **CPU** tab.

### Step 3 — Freeze the List Before You Read It

The process list updates constantly and can be hard to read while it's jumping around. Before recording anything, click the **Name** column header (or **Memory**, if you'd rather sort by what's using the most RAM) to sort the list — this won't stop it from updating, but it keeps things from reordering under you while you read.

### Step 4 — Record CPU Usage

Look at the current CPU usage percentage.

**Current CPU usage:** 11%

### Step 5 — Record Memory Usage

Find how much RAM is currently in use, out of your total installed RAM (the same total you looked up in Part A).

**RAM currently in use:** 87%

**Total installed RAM (from Part A):** 16GB

### Step 6 — List Five Running Processes

List five processes running right now. For each, write your best guess at what it is or does — you don't need to be 100% correct, just reason it out. If you spot something on the cheat sheet below, you can use that, but try at least a couple you don't recognize.

*Cheat sheet — common processes you'll likely see (not exhaustive, just a starting reference):*

| Process Name | Usually Seen On | What It Generally Is |
|---|---|---|
| explorer.exe | Windows | The Windows desktop and file browser itself — normal, always running |
| svchost.exe | Windows | A generic host for background Windows services — several running at once is normal |
| Antimalware Service Executable | Windows | Windows Defender scanning files in the background — normal |
| dwm.exe | Windows | Desktop Window Manager — handles visual effects like transparency and window animations |
| System Idle Process | Windows | Not a real program — represents how much CPU is doing *nothing* right now |
| WindowServer | Mac | Manages everything drawn on your screen — always running |
| Finder | Mac | The Mac desktop and file browser itself — normal, always running |
| mdworker / mds | Mac | Spotlight's background indexing service — normal, can spike briefly after installing apps |
| launchd | Mac | The very first process Mac starts — manages and launches other background services |

*Your five processes:*

| # | Process Name | What I Think It Does |
| --- | --- | --- |
| 1 | WMI Provider Host | Helps the hardware, OS, and software work together |
| 2 | Intel Graphics Software | Allows for graphics on the computer  |
| 3 | Windows Wireless Lan | Connects the computer to the internet |
| 4 | Windows Hello Security Process | OS security |
| 5 | Intel Rapid Storage Technology | Helps the RAM or is the RAM |

### Step 7 — Screenshot and Embed

This step happens directly on GitHub, not through this worksheet — there's no upload field here, since screenshots are added through GitHub's own upload UI.

1. Go to your portfolio repository on GitHub.com and navigate to `assets/screenshots/week-02/`.
2. Click **Add file → Upload files**, then drag in your screenshot (name it something descriptive, like `machine-exploration.png`).
3. Commit the upload.
4. Click on the uploaded image to open it, then click the **Raw** button. Copy the URL from your browser's address bar.
5. After you submit this worksheet, it will be committed to your repo. Go back to GitHub, open the committed file, click the pencil (edit) icon, and paste your raw URL into the embed line below:

```markdown
![Task Manager / Activity Monitor screenshot](paste your raw image URL here)
```

**My Screenshot** (added directly on GitHub after you submit):

### Step 8 — Connect the Numbers

In your own words, explain how the real numbers you found in Part A (OS version, RAM, storage) relate to what you just watched live in Part B. Which number describes hardware, and which describes the OS?

```
Part B shows exactly how the RAM and storage are being utilized. It also shows more components of the OS. 
```

---

## Analysis Questions

### Analysis Question 1

Pick one process from your list in Part B, Step 6. Is it "software" in the sense Lab 01 used that word? Explain how it depends on the OS and on hardware to actually run.

```
Windows Hello Security Process is software that relies on both the operating system (OS) and hardware to run. When a user enters their password, the OS receives it and coordinates with the hardware to verify it. The password is temporarily stored in RAM while the CPU processes it and compares it to the stored password. The CPU gives the password to the OS, and the OS decides whether to unlock the computer or keep it locked. If the password is incorrect, the software notifies the user and prompts them to try again. When a new password is entered, it is again temporarily stored in RAM while the CPU compares it to the securely stored information. If it is correct, the OS allows the software to unlock the computer.
```

### Analysis Question 2

Your CPU usage number changes constantly, even when you're not doing anything. Explain, in your own words, why watching this number matters for security work — not just for performance. (Hint: think about what it might mean if a process you don't recognize suddenly spikes CPU usage.)

```
I initially assumed that the hardware and operating system would use a large percentage of the CPU, but I learned that this is not the case. As I worked through this assignment, I remembered having a computer issue several years ago and someone suggested checking the CPU usage to see if the computer had a virus. As demonstrated in this activity, only a small amount of CPU is used. If an unauthorized process suddenly begins using a significant amount of CPU, it can be sign that there is malware or malicious program. Understanding and monitoring these numbers are important for security work because irregular changes can be a sign of a threat. 
```

### Analysis Question 3

Compare what you saw in Task Manager/Activity Monitor to the diagram you built in Lab 01. What's the same? What did watching your machine live show you that a static diagram couldn't?

```
The diagram and the activity are similar because they both share information about the system architecture however, the diagram is static but the Task Manager showed live, specific, and more in-depth information. The diagram shows general layers while the Task Manager is individualized to the component of the computer. Task Manager can be used to determine the root of an issue by giving details about the systems on the computer. If an issue can not be troubleshooted based on the information in the task manager, it is possible that the issue may be with the hardware or a software program that is external (like a website) from the computer. 
```

---

## Submission Checklist

- [x] OS version, installed RAM, and total/free storage looked up and recorded (Part A)

- [x] Task Manager or Activity Monitor opened and list sorted before recording (Part B)

- [x] Current CPU usage recorded

- [x] Current RAM usage recorded, alongside total RAM from Part A

- [x] Five running processes listed, each with a reasoned guess at what it does

- [x] Screenshot uploaded to `assets/screenshots/week-02/` via GitHub and embedded directly in the committed file

- [x] Connection explanation written (Part B, Step 8 — minimum 2 sentences)

- [x] All three Analysis Questions answered (minimum sentence counts met)

---

*CyberVisionaries Institute · Cyber Foundations · Tier I*
