# Week 2 Lab 01 — Cybersecurity Landscape & Digital Infrastructure Overview

**Student Name:** Catasia Williams

**Date Completed:** July 25, 2026

**Module:** 1 — Digital Infrastructure & CLI | **Week:** 2  
**Submission Path:** `week-02/labs/lab-01-hardware-os-software-diagram.md`

---

## Overview

In this lab, you build a working mental model of the system you'll be securing throughout this course: the hardware, operating system, and software layers that make up every computer, and where the cybersecurity field fits around them. This lab has two parts. Part A connects this week's material to the CyberFoundations City map. Part B has you build and explain a diagram of how a computer's hardware, OS, and software layers interact.

**No terminal or command line is required this week** — that starts in Week 3.

---

## Lab Environment

| Component | Details |
|---|---|
| Environment | Browser-based Lab Portal (Module 1 orientation) |
| Required Materials | CyberFoundations City map; a diagram tool of your choice (hand-drawn and photographed, or any digital tool) |

**Prerequisite:** Portfolio repo created from the CyberFoundations student template in Week 1. Fill out this worksheet here in the Lab Portal, then hit Submit to commit it directly to your repo at `week-02/labs/lab-01-hardware-os-software-diagram.md`.

---

## Part A — CyberFoundations City & the Cybersecurity Landscape

The CyberFoundations City map is your visual guide to the next 11 weeks. Each district represents a module of this course. This part connects this week's material to the map you were introduced to in Week 1.

### Step 1 — Open the Lab Portal Orientation Module

From your Student Dashboard, open the **Module 1 orientation** module.

### Step 2 — Complete the Orientation Walkthrough

Work through the orientation content. It covers the same hardware/OS/software material as this week's lessons from a different angle — use it to check your understanding, not to replace the lessons.

### Step 3 — Locate This Week's District on the City Map

Open the CyberFoundations City map (introduced in Week 1, Lesson 6). Identify which district corresponds to Module 1 — Digital Infrastructure & CLI.

**District name:**

```
The Foundry District
```

**Why this district fits this week's topics (1–2 sentences):**

```
The Foundry District fits this week's topics because it represents the foundational stage of our learning journey. The rest of our learning will build upon the core of what is inside a computer, operating systems, and the cybersecurity landscape. 
```

---

## Part B — Hardware, OS, and Software Diagram

A computer is a stack of layers: physical hardware at the bottom, an operating system managing that hardware in the middle, and the software you actually use on top. This part has you draw that stack and explain it in your own words.

### Step 1 — Identify the Layers

Before drawing anything, name one example of what lives at each layer.

**Hardware layer — one example component (e.g., CPU, RAM, or storage):**

```
RAM - RAM is the temporary high speed memory that supports the program(s) that are being used and is cleared when the computer is turned off. 
```

**Operating system layer — name an OS (e.g., Windows, Linux, or macOS):**

```
Linux - Linux is an open-source operating system that is typically used in business settings to run and manage servers, security, and cloud systems. 
```

**Software layer — one example application (e.g., a web browser or word processor):**

```
Web browser - A web browser allows users to access and use the internet. 
```

### Step 2 — Sketch Your Diagram

Sketch a simple diagram (hand-drawn and photographed, or built in any digital tool) showing how the hardware, OS, and software layers stack and interact. Arrows or labels showing "what talks to what" matter more than visual polish. If you'd like a free browser-based option instead of hand-drawing, try [draw.io](https://www.drawio.com/) — no account required to get started.

### Step 3 — Upload and Embed Your Diagram

This step happens directly on GitHub, not through this worksheet — there's no upload field here, since screenshots and diagrams are added through GitHub's own upload UI, the same way as every other week.

1. Go to your portfolio repository on GitHub.com and navigate to `assets/screenshots/week-02/`.
2. Click **Add file → Upload files**, then drag in your diagram image (name it something descriptive, like `hardware-os-software-diagram.png` — no spaces, lowercase, no timestamps).
3. Commit the upload.
4. Click on the uploaded image to open it, then click the **Raw** button. Copy the URL from your browser's address bar.
5. After you submit this worksheet, it will be committed to your repo. Go back to GitHub, open the committed file, click the pencil (edit) icon, and paste your raw URL into the embed line below:

```markdown
![Hardware/OS/software diagram](paste your raw image URL here)
```

**My Diagram** (added directly on GitHub after you submit):

### Step 4 — Explain Your Diagram

In your own words — not a copied definition — explain how the three layers interact. Reference your own diagram directly.

**Explanation (minimum 3 sentences):**

```
The hardware is the foundation of a computer. It is needed in order for a user to do the things they want to do. The hardware consists of the motherboard, CPU, RAM and storage to ensure the system can be powered on and there is memory and storage for the operating systems and software to be functional and usable. They manage the hardware, provide a GUI, and handles files. Windows and MacOS operating systems are typically found in day to day computers while Linux is mostly used for servers. Operating systems allows users to multitask by allowing several software systems to run at once. Most users really enjoy the software. Software is the day to day applications and the reason most people turn on their devices. If your computer screen looks anything like mine (with many software programs running and multiple internet tabs open) then we should be thankful for all three of the systems!
```

---

## Analysis Questions

Answer each question in your own words. These questions connect what you did in Parts A and B to the bigger picture of this course.

### Analysis Question 1

If the operating system crashed on the computer you diagrammed, which layer(s) would stop working, and which (if any) would keep working? Explain your reasoning.

```
The applications such as web browsers, music players, and document editors would stop working because they depend on the OS to open files, utilize memory, access the internet, and communicate with hardware for things like memory and storage. The operating system can be seen as the connecting glue or connector between the software and the hardware.
```

### Analysis Question 2

Pick one piece of software you use daily. Trace it down through the OS to the hardware it ultimately depends on. What would happen to that software if the hardware layer failed?

```
I use Microsoft Word  daily. If the hardware layer failed Microsoft Word will not be able to function. It relies on the OS to process the requests such as open the program, open files, save files, and see graphics. The hardware layer provides the physical resources needed for Word to run and for users to create and edit documents. Below is how Word relies on the hardware and what would happen if the hardware layer failed:

CPU: processes Word’s instructions and handles editing tasks; Word won't be able to process commands.
RAM: temporarily stores the document and information while Word is open; Microsoft Word can freeze or crash.
Storage saves document and files; Word may not open
GUI: provides graphics, text, and images on the screen; I won't be able to see word or if it is open I won't be able to see any of its graphics. 

```

### Analysis Question 3

Explain, in your own words, why a cybersecurity professional needs to understand all three layers — hardware, OS, and software — rather than just the software layer where most visible attacks (like phishing emails) happen.

```
A cybersecurity professional need to understand hardware, operating systems, and software because they are interdependent. Software depends on the OS and the hardware to operate and function properly. Cybersecurity professionals need to understand of the entire ecosystem because to ensure they know the depth of security that is needed and to understand how deep vulnerabilities may go. 
```

---

## Lab Report Questions

Answer each question in complete sentences.

**1. What is the cybersecurity landscape, and why does it matter to someone starting this course?**

```
The cybersecurity landscape encompasses all the elements that  are within cybersecurity. It matters to someone starting this course because the can get an understanding of the various aspects of cybersecurity since it is multimodal. The landscape helps students to connect different concepts and elements. 
```

**2. Which CyberFoundations City district did you identify in Part A, and how does its theme connect to the hardware/OS/software material in Part B?**

```
The Foundry connects to the hardware/OS/software material in Part B because the material is the foundation of the skills we are learning. 

```

**3. Of the three layers (hardware, OS, software), which one do you think is hardest to secure, and why?**

```
I think the OS is the hardest to secure because it is responsible for connecting the hardware to the software. A vulnerable OS can cause more significant issues than vulnerable software because the OS can be used to access and control the entire system. A vulnerability to an individual software application can be isolated with a lower chance of direct access to the entire system. 

```

---

## Submission Checklist

- [x] Lab Portal Module 1 orientation completed

- [x] District identified and explained

- [x] Hardware, OS, and software layer examples listed

- [x] Diagram uploaded to `assets/screenshots/week-02/` via GitHub and embedded directly in the committed file

- [x] Diagram explanation written in your own words (minimum 3 sentences)

- [x] All three Analysis Questions answered (minimum sentence counts met)

- [x] All three Lab Report Questions answered in complete sentences

---

*CyberVisionaries Institute · Cyber Foundations · Tier I*
