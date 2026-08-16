# Week 5 Lab 02 — The Grid Outage (CLI Simulator)

**Student Name:** Catasia Williams

**Date Completed:** August 15, 2026

**Module:** 2 — Networking & Cloud Foundations | **Week:** 5  
**Submission Path:** `week-05/labs/lab-02-the-grid-outage.md`

---

## The Ticket

> **TICKET #GRID-0412 — PRIORITY: HIGH**
> **Reported by:** Foundry District operations staff
> **Summary:** Foundry staff report they cannot reach the relay station. Multiple people, multiple machines, since this morning. No changes reported on their end.
> **Assigned to:** you.
>
> **You are on call.** Find out what is actually broken and write it up.

---

## Overview

Lab 01 handed you the tools. This lab hands you a problem and gets out of your way.

Somewhere on The Grid, something is down. Your job is not to guess which thing — your job is to **find out**, one rung at a time, and then write down what the evidence says. This is the first time in this course you're being asked to do real diagnostic work rather than follow a recipe, and it is a genuine skill. You already have everything you need.

**The method is the Ladder Rule from Lesson 4:**

1. **Check yourself** — do you have a valid address?
2. **Check your gateway** — can you get out of your own neighbourhood?
3. **Check the target by NAME.**
4. **Check the target by IP.**
5. **Trace the path.**

*Work outward, one rung at a time, and let the evidence pick the culprit.*

The reason the ladder exists is that instinct is a terrible investigator. Instinct wants to name a villain in the first thirty seconds — "it's DNS," "it's the firewall," "it's the router" — and then spend an hour proving itself right. Evidence is slower and it is correct. **Do not decide what is broken until Part E.** Run the rungs in order, record what each one actually said, and let the finding assemble itself.

You will also be told, partway through, what somebody else thinks the problem is. Treat that the way you'd treat any other claim: test it.

---

## Lab Environment / Pre-Lab Check

| Component | Details |
|---|---|
| Environment | CyberFoundations CLI Simulator (browser-based, inside the Lab Portal) |
| Shell | **bash** throughout this lab |
| Prerequisite | Week 5, Lessons 1–4 completed; Lab 01 completed first (this lab assumes those tools) |
| Commands used | `ip addr`, `ip route`, `ping`, `dig`, `traceroute` |

**Before you start:** log into the Lab Portal, open **Week 5 → CLI Simulator**, and load the **"The Grid — Outage Response (Bash)"** scenario. It boots you into the same workstation you used in Lab 01, on the same segment, with the same gateway. Only one thing about The Grid has changed since yesterday. Find it.

---

## Part A — Establish Your Baseline

Rungs 1 and 2 of the ladder. It is tempting to skip straight to the thing users complained about — resist that. If you don't establish that *your own machine and your own way out are healthy*, then every failure you find afterwards is ambiguous. You won't know whether the target is broken or whether you are.

### Step 1 — Check Yourself

Confirm your workstation still holds a valid address on The Grid, and that you know where its traffic leaves from.

Run `ip addr` for your address, then `ip route` for your gateway — the same two commands you used in Lab 01. (Remember: addresses and routes live in different places, so it takes both.)

The full `ip addr` output:

```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 02:1a:7c:44:0b:5e brd ff:ff:ff:ff:ff:ff
    inet 10.20.5.42/24 brd 10.20.5.255 scope global eth0
       valid_lft forever preferred_lft forever
```

The full `ip route` output:

```
default via 10.20.5.1 dev eth0
10.20.5.0/24 dev eth0 proto kernel scope link src 10.20.5.42
```

Your IPv4 address and default gateway, pulled out of those two results:

```
IPv4: 10.20.5.42/24
Default gateway: 10.20.5.1
```

### Step 2 — Check Your Gateway

Ping your default gateway. This is the door out of your neighbourhood — if this fails, nothing past it means anything.

Command you ran:

```
student@ivy-workstation:/home/student$ ping 10.20.5.1
```

Output (the full ping result, including the summary line):

```
PING 10.20.5.1 (10.20.5.1) 56(84) bytes of data.
64 bytes from grid-gateway (10.20.5.1): icmp_seq=1 ttl=64 time=1.000 ms
64 bytes from grid-gateway (10.20.5.1): icmp_seq=2 ttl=64 time=1.200 ms
64 bytes from grid-gateway (10.20.5.1): icmp_seq=3 ttl=64 time=1.100 ms
64 bytes from grid-gateway (10.20.5.1): icmp_seq=4 ttl=64 time=1.300 ms

--- 10.20.5.1 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3005ms
rtt min/avg/max/mdev = 1.000/1.150/1.300/0.100 ms
```

### Step 3 — State What the Baseline Proves

Two healthy results is not "nothing happened." It's a finding, and it eliminates an entire category of causes before you've touched the target once.

What your baseline rules out, and why that matters before you go further:

```
The baseline rules out incorrect or missing IP address, incorrect subnet configuration, inactive network interface, missing default gateway, and a gateway that is not working. The gateway can be reached and there are no packet loss. This matters before going further because if the gateway can't be reached, nothing else tried will work. Since the gateway network can be reached, the basic network configuration is working. 
```

---

## Part B — Test the Target

Rungs 3 and 4. This is the fork in the road, and the two tests must be run **in this order** and read **as a pair**. Either one alone tells you almost nothing. Together they tell you almost everything.

### Step 1 — Test the Target by Name

Ping `relay-station.grid.local` — the host the Foundry staff say they can't reach.

Command you ran:

```
student@ivy-workstation:/home/student$ ping relay-station.grid.local
```

Output (the full ping result, including the summary line):

```
PING relay-station.grid.local (10.20.5.30) 56(84) bytes of data.

--- relay-station.grid.local ping statistics ---
4 packets transmitted, 0 received, 100% packet loss, time 3005ms
```

### Step 2 — Read That Output Carefully Before You Move On

There are two separate things happening in a ping, and this output separates them for you. Look at the **first line**, then look at the **summary line**, and notice that they do not agree about whether things are going well.

Did the name turn into an IP address — and if so, which one? Then: what did the packet loss say?

```
The first line shows relay-station.grid.local resolved to IP address 10.20.5.30. The summary line shows 4 packets were transmitted and none of them were received so there was 100% packet loss. The latency is 3005ms.
```

### Step 3 — Ask DNS Directly

Ping *told* you the name resolved, but it told you in passing, on one line, while it was busy doing something else. Ask the question on its own so the answer is unambiguous — and so you have it in writing when you escalate.

Run `dig relay-station.grid.local`.

Command you ran:

```
student@ivy-workstation:/home/student$ dig relay-station.grid.local
```

Output (the full dig result):

```
; <<>> DiG 9.18.24 <<>> relay-station.grid.local
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 41207
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0

;; QUESTION SECTION:
;relay-station.grid.local.			IN	A

;; ANSWER SECTION:
relay-station.grid.local.	3600	IN	A	10.20.5.30

;; Query time: 1 msec
;; SERVER: 10.20.5.10#53(10.20.5.10)
```

Look at the `status:` field in the header and the `ANSWER SECTION`. Does DNS know this host, and if so, what address does it hand back?

What the status field said, and the A record it returned:

```
DNS knows this host and the address it hands back is 10.20.5.30 (for relay-station.grid.local)
The status field said, "no error". 
The A record it returned is 10.20.5.30
```

This is the single most quotable piece of evidence in the whole investigation, because it settles a question your colleague is about to raise.

### Step 4 — Test the Target by IP

Now take the IP address out of that first line and ping it directly: `10.20.5.30`. You are deliberately removing name lookup from the equation.

Command you ran:

```
student@ivy-workstation:/home/student$ ping 10.20.5.30
```

Output (the full ping result, including the summary line):

```
PING 10.20.5.30 (10.20.5.30) 56(84) bytes of data.

--- 10.20.5.30 ping statistics ---
4 packets transmitted, 0 received, 100% packet loss, time 3005ms
```

### Step 5 — State What the Combination Proves

Now put the two results side by side. The by-name test and the by-IP test each had a job:

- The by-name test asks: *can this name be turned into a number, and does that number answer?*
- The by-IP test asks: *forget names entirely — does that number answer?*

Work through it. If the name failed to become a number, that would point one direction. If the name became a number just fine but the number won't answer, that points somewhere else entirely. And if you removed the name from the equation altogether and the failure **didn't change**, then whatever is broken was never about the name.

What the two tests together prove — and, just as importantly, what they rule out:

```
The by-name test and the by IP-test are used together. Both tests show that DNS is working because the hostname successfully resolves to 10.20.5.30. The by-IP test then shows that the same destination has 100% packet loss even without using DNS. 
The tests rule out: DNS not working because relay-station.grid.local successfully resolved to 10.20.5.30; Hostname being incorrect or unknown because DNS returned a valid A record for relay-station.grid.local; and Rules out DNS causing the connection failure because pinging 10.20.5.30 directly, without using DNS, still resulted in 100% packet loss.

```

---

## Part C — Trace the Path

Rung 5. Ping tells you *whether* something answers. Traceroute tells you *how far your traffic got before it stopped* — it lists each hop along the way, and a row of `* * *` means the path died at that point.

One traceroute on its own is hard to read if you've never seen a healthy one. So you'll run two, and compare.

### Step 1 — Trace to the Broken Target

Run `traceroute relay-station.grid.local`.

Command you ran:

```
student@ivy-workstation:/home/student$ traceroute relay-station.grid.local
```

Output (the full trace, including the timeout rows):

```
traceroute to relay-station.grid.local (10.20.5.30), 8 hops max, 60 byte packets
  1  grid-gateway (10.20.5.1)  1.000 ms  1.200 ms  1.100 ms
  2  * * *
  3  * * *
  4  * * *
  5  * * *
  6  * * *
  7  * * *
  8  * * *
```

The last hop that answered, and what happened after it:

```
The last hop that answered was 1 and after that the traceout stopped receiving responses. The traffic successfully reached the gateway at hop 1, but no response was received from anything beyond the gateway.
```

### Step 2 — Trace to a Known-Good Target for Comparison

Now trace to a host you have no reason to suspect — `cloud-heights.grid.local`, out on the far edge of The Grid. (You'll be spending a lot of time in Cloud Heights next week. Consider this an introduction.)

Command you ran:

```
student@ivy-workstation:/home/student$ traceroute cloud-heights.grid.local

```

Output (the full trace):

```
traceroute to cloud-heights.grid.local (10.20.7.80), 8 hops max, 60 byte packets
  1  grid-gateway (10.20.5.1)  1.000 ms  1.200 ms  1.100 ms
  2  grid-core (10.20.0.1)  4.000 ms  4.200 ms  4.100 ms
  3  cloud-heights.grid.local (10.20.7.80)  12.000 ms  12.200 ms  12.100 ms
```

The complete list of hops, in order:

```
10.20.5.1 
10.20.0.1
10.20.7.80
```

### Step 3 — Compare the Two Traces

The comparison is the whole point of running two. One trace completed and one didn't — and where each one stopped is the evidence.

Pay attention to whether the **first hop** was the same in both. If traffic to the broken target and traffic to the healthy target both got through the same first hop successfully, that tells you something specific about which part of the path is fine.

What the comparison tells you about where the problem is — and where it is not:

```
The first hop was the same in both traces. Both destinations have the same first hop: grid-gateway (10.20.5.1).The gateway responds successfully for both destinations. This indicates that this part of the path is fine because traffic to the broken target and traffic to the healthy target both got through the first hop. This shows the computer's connection to the default gateway is working. Therefore, the problem is not between the computer and the gateway. The problem should be farther along The Grid's network path after 10.20.5.1.
```

---

## Part D — The Colleague's Theory

A more experienced colleague on the on-call channel reads your notes and jumps in:

> "Oh, I've seen this one. It's the relay station's DNS entry — it's `relay-station-old.grid.local` that everything actually points at, and that name is busted. This is a DNS problem, not a host problem. Go check it."

They sound confident. They may even be senior to you. **Test the claim anyway.** In security work, "somebody confident said so" is not evidence, and the fastest way to be respectfully wrong-footed is to accept a theory you could have checked in ten seconds.

### Step 1 — Test the Colleague's Host

Ping `relay-station-old.grid.local`.

Command you ran:

```
student@ivy-workstation:/home/student$ ping relay-station-old.grid.local
```

Output (the exact error or result — copy it precisely):

```
ping: relay-station-old.grid.local: Name or service not known
```

### Step 2 — Explain Why This Is a Different Kind of Failure

This result does **not** look like Part B. Compare them closely:

- In Part B, the name became a number, and then the packets went nowhere.
- Here, you never got a number at all.

Those are two genuinely different failures, at two different stages, and confusing them is one of the most common mistakes in network troubleshooting. In Lesson 2 you met the pair: **a name that doesn't resolve at all** versus **a name that resolves perfectly to a host that's dead**. One is the directory not having an entry. The other is the directory being completely correct about an address where nobody answers the door.

For context: `relay-station-old.grid.local` was decommissioned. It was retired on purpose, its directory entry was removed on purpose, and it has nothing to do with today's ticket. A retired name failing to resolve is *expected behaviour*, not an outage.

Explain, in your own words, why this failure is a different kind from the one in Part B — and why it is not the cause of today's outage:

```
In Part B, relay-station.grid.local successfully resolved to an IP address but there was 100% packet loss. This  failure is different because now relay-station-old.grid.local was intentionally decommissioned and its DNS entry was intentionally removed resulting in a name that doesn't resolve at all and therefore no IP address. 
```

### Step 3 — Say How You'd Reply to Your Colleague

You now know they're wrong. Being right is easy; being useful about it is a professional skill. Write the reply you'd actually send — polite, specific, and grounded in what you ran rather than in who's more senior. Point at the evidence, not at the person.

Your reply to your colleague:

```
Hi Mrs. Colleague: Thanks for your assistance. I ran 'ping relay-station-old.grid.local' and this is the output I received: Name or service not known. I did some further research and learned that 'relay-station-old.grid.local' was decommissioned and  its directory entry was removed. I believe this resolves the issue. Please let me know if there is anything else we should investigate. 
```

### Step 4 — One Control Test Before You Write It Up

You are about to tell people something is broken. Before you do, prove that *not everything* is broken — otherwise the first question you'll be asked is whether the problem is you.

Ping a host you already know is healthy: `foundry-archive.grid.local`.

Command you ran:

```
student@ivy-workstation:/home/student$ foundry-archive.grid.local

```

Output (the full ping result):

```
bash: foundry-archive.grid.local: command not found
```

Why this matters: a report that says "the relay station is unreachable" is weaker than one that says "the relay station is unreachable **while every other host I tested answers normally**." The second version has already ruled out the boring explanations, and it's the difference between a ticket that gets acted on and one that gets handed back to you.

### Step 5 — Capture Your Evidence (REQUIRED screenshot)

Take a screenshot of your simulator session showing your evidence trail — at minimum the failed ping by name, the successful `dig`, the failed ping by IP, and the failed traceroute. **This screenshot is required.** Name it `cli-grid-outage.png`. You'll upload it and record its filename via the GitHub Commit section below.

An incident note with no attached evidence is just an opinion. This is the attachment.

---

## Part E — Write the Finding

This is the part that makes you a security professional rather than someone who can run commands.

Everything you've done so far is raw evidence. Nobody upstream of you — not your team lead, not the Foundry staff who filed the ticket, not the person who picks this up on the next shift — is going to read six terminal outputs and work out the conclusion themselves. Your job is to hand them the conclusion **and** the reason to believe it.

This is your first incident-report rep. You will do many more; Week 12's capstone asks you to write these for real. So we're giving you the structure now, while the stakes are low. Fill in each field — this is not a blank page, it's a form, and every professional incident note answers these same four questions.

**Keep it short and specific.** A good finding is a paragraph, not an essay. Write what you can defend.

### Step 1 — What Is Broken

One or two sentences. Name the specific thing that is not working. Be precise about *what* is down — not "the network," not "the relay station area," but the actual component your evidence points at.

Your statement of what is broken:

```
The relay station at 10.20.5.30 is unreachable. DNS resolves relay-station.grid.local correctly to 10.20.5.30, but the destination does not respond to ping.
```

### Step 2 — What Evidence Proves It

List the specific tests you ran and what each one returned. This is where your Parts B and C outputs earn their keep. Someone reading this should be able to re-run your tests and reach the same conclusion without asking you a single question.

Your evidence, test by test:

```
ping 10.20.5.1 → Returned 4/4 replies with 0% packet loss, confirming the local gateway is reachable.
ping relay-station.grid.local → Resolved to 10.20.5.30, but returned 100% packet loss.
ping 10.20.5.30 → Returned 100% packet loss, confirming the failure occurs even without DNS.
dig relay-station.grid.local → Returned NOERROR and an A record of 10.20.5.30 from DNS server 10.20.5.10.
traceroute relay-station.grid.local → Reached 10.20.5.1 (grid-gateway) at hop 1, then received no responses from later hops.
traceroute cloud-heights.grid.local → Reached 10.20.5.1 (grid-gateway) at hop 1, 10.20.0.1 at hop 2, and 10.20.7.80 at hop 3. This shows the network path beyond the gateway works for the healthy destination.
```

### Step 3 — What You Ruled Out, and How

Just as important as what you found. Say explicitly which possible causes you eliminated and which specific test eliminated each one. At minimum, address: your own workstation, your local network path out, name resolution, and the colleague's theory.

Ruling out possibilities is what separates a finding from a guess. A reader who sees only your conclusion has to trust you. A reader who sees what you eliminated can *check* you.

What you ruled out and the evidence that ruled it out:

```
Workstation: Ruled out as the cause because 'ip addr' showed the correct IP address 10.20.5.42/24 and an active eth0 interface.
Local network path: Ruled out because 'ping 10.20.5.1' was successful and reached the gateway with 0% packet loss.
Name resolution/DNS: Ruled out because 'dig relay-station.grid.local' returned NOERROR and the A record 10.20.5.30. Also, pinging the IP directly ('ping 10.20.5.30') also produced the same 100% packet loss.
The gateway as the problem: Ruled out because the healthy destination (cloud-heights.grid.local) successfully traveled through the same first hop, 10.20.5.1, and reached 10.20.7.80 at hop 3.

```

### Step 4 — What Should Happen Next

One or two sentences. Based on your finding, who or what needs to be looked at, and by whom? You don't have the access to fix this yourself — and that's normal. Knowing exactly what to escalate, and to whom, is the deliverable.

Your recommended next step:

```
10.20.5.30 and the network path beyond hop 1 should be escalated. 

10.20.5.30 should be investigated because both ping relay-station.grid.local and ping 10.20.5.30 resulted in 100% packet loss.

The network path beyond hop 1 should be investigated because traceroute successfully reached the gateway at 10.20.5.1, but received no responses after that point. The healthy destination ('cloud-heights.grid.local') reached hop 2 and hop 3, showing that the network can work beyond the gateway, but the path toward 10.20.5.30 is still failing.
```

---

## Analysis Questions

**Analysis Question 1.** In Part B you pinged the target by name and then by IP. Explain why running *both* is necessary — describe what a person would wrongly conclude if they had run only the by-name test and stopped there. *(Minimum 3 sentences.)*

```
Running both tests shows whether the problem is with the name lookup or the connection to the destination. If only the by-name test were run, the failure could be mistakenly blamed on DNS. The by-IP test shows that the same failure happens when DNS is completely removed from the test. It is easy to assume the issue is with the DNS but running both these tests removes the assumption and helps prove what and where the error is. 
```

**Analysis Question 2.** A name that returns "Name or service not known" and a name that resolves fine but never replies to a ping are two different failures with two different causes. Describe each one in plain English — what is actually going wrong in each case — and explain why treating them as the same problem would send a troubleshooter down the wrong path. *(Minimum 3 sentences.)*

```
A name that returns “Name or service not known” means the name could not be matched to an IP address, so the computer does not know where to send the traffic. This can happen because of a nonexistent name, typo, or decommissioned host and often corresponds to NXDOMAIN, which means the domain or name does not exist. A name that resolves fine to an IP address but does not reply to ping means the computer knows where the destination is, but the destination is not responding. Treating them as the same problem could cause an investigation of DNS when DNS is actually working and the problem is with reaching the destination. It is good practice to look up the name first and then test the IP address. If the name does not resolve, the problem is with name resolution. If an IP address is returned but the destination does not respond, the problem is beyond the name resolution.
```

**Analysis Question 3.** Part A asked you to confirm your own address and your gateway before touching the reported problem at all — even though the ticket had nothing to do with your workstation. Defend that step to a colleague who thinks it's a waste of time on an urgent ticket. *(Minimum 3 sentences.)*

```
Checking the workstation first is important because it establishes a baseline before investigating the reported problem. Confirming the IP address and gateway quickly shows whether the workstation's basic network connection is working. On an urgent ticket, this increases efficiency by preventing wasted time investigating the wrong part of the network and helps narrow down where the problem actually is.
```

**Analysis Question 4.** Your colleague was confident, possibly senior, and wrong. Describe how you decided their theory was wrong, and what you think that says about how much weight confidence should carry compared to evidence in security work. Where relevant, consider what would have happened if you had simply accepted their theory and reported it upward. *(Minimum 3 sentences.)*

```
I decided the theory was wrong by testing the hostname (relay-station.grid.local) in question which resulted in “Name or service not known". Testing the hostname is a simple, low effort way to start the investigation. It is also good practice for starting an investigation so this should be a routine habit. Although the colleague has more experience, somethings things change without everyone being updated or human error where someone can forget something changed. If I had simply accepted their theory and reported it upward, this could have been a waste of resources, as well as, a poor reflection of my skillset. 
```

---

## Submission Checklist

- [x] Own address and gateway confirmed (Part A, Step 1)

- [x] Gateway pinged successfully and output recorded (Part A, Step 2)

- [x] Baseline reasoning stated — what a healthy baseline rules out (Part A, Step 3)

- [x] `relay-station.grid.local` pinged by name; resolution and packet loss both read (Part B, Steps 1–2)

- [x] `dig relay-station.grid.local` run; status and A record recorded (Part B, Step 3)

- [x] `10.20.5.30` pinged directly; output recorded (Part B, Step 4)

- [x] The combined proof of the tests stated in writing (Part B, Step 5)

- [x] `traceroute relay-station.grid.local` run; last responding hop identified (Part C, Step 1)

- [x] `traceroute cloud-heights.grid.local` run; all hops listed in order (Part C, Step 2)

- [x] The two traces compared and interpreted (Part C, Step 3)

- [x] `relay-station-old.grid.local` tested and its exact error recorded (Part D, Step 1)

- [x] Explained why the decoy is a different kind of failure (Part D, Step 2)

- [x] Reply to the colleague drafted, grounded in evidence (Part D, Step 3)

- [x] Control test run against a healthy host before escalating (Part D, Step 4)

- [x] **REQUIRED:** `cli-grid-outage.png` uploaded to `assets/screenshots/week-05/` and its filename recorded (Part D, Step 5)

- [x] Incident note complete — what's broken, evidence, ruled out, next step (Part E, Steps 1–4)

- [x] All four Analysis Questions answered (minimum sentence counts met)

- [x] This file is committed to your portfolio repo at `week-05/labs/lab-02-the-grid-outage.md`

---

## GitHub Commit Subsection

This lab's written answers are submitted through the **CyberFoundations Lab Portal**.

1. Go to the CyberFoundations Lab Portal and sign in.
2. Open **Week 5 → Lab 02: The Grid Outage**.
3. Fill in the worksheet fields — they match the commands, outputs, and questions in this file, in the same order.
4. Connect your GitHub account if you haven't already (one-time setup), and select your portfolio repo.
5. Click **Submit to GitHub**. The Portal commits the completed file to `week-05/labs/lab-02-the-grid-outage.md` for you.

**📸 REQUIRED — your evidence screenshot.** Your incident note in Part E needs something to point at:

1. Go to your portfolio repository on GitHub.com and navigate to `assets/screenshots/week-05/` (create the folder if this is your first Week 5 screenshot).
2. Click **Add file → Upload files**, drag in your screenshot, named `cli-grid-outage.png` (lowercase, hyphens, no spaces).
3. Scroll down and click **Commit changes**.
4. Click the uploaded image's filename to open it and confirm your evidence is readable at full size — if the terminal text is too small to read, retake it.
5. Record the filename below so your grader knows to look for it.

The screenshot filename you uploaded:

```
cli-grid-outage.png
```

Your screenshot lives in `assets/screenshots/week-05/` in your repository, alongside the rest of your Week 5 evidence. It does not need to be linked inside this worksheet.

---

*CyberVisionaries Institute · Cyber Foundations · Tier I*
