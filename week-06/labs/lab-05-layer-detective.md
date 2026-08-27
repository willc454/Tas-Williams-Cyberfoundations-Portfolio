# Week 6 Lab 05 — Layer Detective

**Student Name:** Catasia Williams

**Date Completed:** August 23, 2026

**Module:** 2 — Networking & Cloud Foundations | **Week:** 6  
**Submission Path:** `week-06/labs/lab-05-layer-detective.md`

---

## Overview

**This is a SHORT lab — 20 to 30 minutes — and it needs no VM.** No Cloud Heights session, no simulator, no screenshot. This is a thinking lab: you take the evidence you have already collected in Weeks 5 and 6 and sort it into layers.

This is an **independent** lab.

---

## Lab Environment / Pre-Lab Check

| Component | Details |
|---|---|
| Environment | This worksheet only — nothing to start, nothing to connect to |
| Prerequisite | Week 5 labs and Week 6 Labs 01–04 |
| Screenshot | None required |

---

## Part A — The Seven-Row Table

Fill in every row. For the last column, name one **real thing you personally saw** in Weeks 5–6 that belongs at that layer.

| # | Layer name | One-line job | Real thing from Weeks 5–6 |
| --- | --- | --- | --- |
| 7 | Application | Network services that applications use to communicate and the things you actually interact with (the request, the shell) | The HTTP request; a log-in that was authentication or failed authentication; the DNS resolving a name |
| 6 | Presentation | How data is formatted, encoded or encrypted for systems to understand it. Puts data in shape so that the other side can use | HTTPS is secured so data is encrypted during transmission and interpreted by the receiver |
| 5 | Session | Establishes, maintains, and terminates communication between systems. Starts, holds, and end a conversation between 2 applicatons | The SSH session. Connected to another VM using ssh and received a remote shell. The SSH session allowed you to continue entering commands on that remote machine . Started in one VM, used ssh to enter another VM, and then used exit to leave the nested session and return to the outer shell. |
| 4 | Transport | Runs the conversation between two machines by using TCP/UDP and ports | The TCP handshake that established the connection to the ports |
| 3 | Network | Gets messages between addresses, masks, gateway, routes. Uses IP addresses and routing to move traffic through networks.  | Using 'ping' to whether an IP address is reachable; 'ip route' to show where network traffic should be sent |
| 2 | Data Link | Transmits data reliably. Moves data between the machine and another device on the network. Gets a message across one local hop from your machine to the thing next to it. | Cloud Heights communicating with the Beacon (the known-good target). |
| 1 | Physical | Moves raw signal (electricity, light, radio) | Joining wi-fi |

---

## Part B — Case Files

For each case, name the layer where the problem lives, and name the evidence proving the layers **below** it were already working.

### Case File 1 — The Name That Went Nowhere

A hostname lookup fails, but pinging the machine's IP address directly succeeds.

Layer:

```
Layer 7 - Application Layer
Rung 4
```

Evidence that the layers below were working:

```
The machine's IP address was successfully pinged which proves that that lower layers were working. When the hostname lookup fails, this points to an issue with the DNS translating the hostname to an IP address. 
```

### Case File 2 — Permission Denied

`ssh` to a host returns `Permission denied` after a password prompt.

Layer:

```
Layer 7 - Application Layer
Rung 5
```

Evidence that the layers below were working:

```
Reachability was proven because the network was able to reach the host and the SSH responded. The TCP handshake was completed and the session opened. The failure happened during authentication; after the service was reached. 
```

### Case File 3 — The Cable Story

A machine reports no link on its interface and has no address at all.

Layer:

```
Layer 1 - Physical Layer

```

Evidence and reasoning:

```
There is no link and no address indicating that no signals are being transmitted. 
```

### Case File 4 — Ping Works, The Page Does Not

`ping` to a server succeeds, but `curl http://<that server>` returns nothing useful.

Layer:

```
None
```

Evidence that the layers below were working:

```
The platform's ICMP is designed to not provide an output for this. 
```

### Case File 5 — Wrong Neighbourhood

A machine has an address, but its default route points somewhere that cannot forward its traffic.

Layer:

```
Layer 3 - Network
Rung 2 
```

Evidence and reasoning:

```
The issue is with the default gateway because the machine's IP address was already confirmed. 
```

---

## Part C — The Silent Gateway Case

In Lab 03 the Azure default gateway did not answer your ping. However, your VM had a valid default route configured, and your local communication with the Grid Beacon — the ping replies, the HTTP banner, and `TRACE ID: CF-NET-0604` — succeeded.

A failed gateway ping is one piece of evidence — not automatically proof of a gateway or network failure. But the evidence you weigh against it has to be the right kind of evidence.

The Grid Beacon at `10.60.6.4` sits on the same local subnet as your VM (`10.60.6.0/26`). Reaching it proves **local-subnet connectivity** — that traffic never crosses the default gateway, so beacon success alone cannot prove the gateway forwarded anything. Your `ip route` output proves a **default route is configured** — your VM knows where it intends to send non-local traffic — but it does not prove the gateway forwarded that traffic. The evidence that demonstrates the **default path is functioning** is successful communication with a destination outside `10.60.6.0/26`, such as the outbound internet access through NAT that you examined in Lab 04.

### Step 1 — Rule on the Case

Is the failed gateway ping enough evidence to declare a network-layer failure? Explain your answer using the other evidence you collected. In your response, distinguish between:

- evidence that proves **local-subnet connectivity**
- evidence that proves a **default route is configured**
- evidence that supports **successful off-subnet connectivity**

```
The failed gateway ping is not enough evidence to declare a network-layer failure and other evidence must be collected:
A - Local-subnet connectivity: The ping to the Grid Beacon (The known-good test) was successful because a reply was received and, the curl to the Grid Beacon was also successful because the HTTP banner & Trace Id were received.

B - Default route is configured: The 'ip route' was successful which proves the default gateway was configured so the VM knows where to send traffic outside of its local subnet that is destined for other networks.

C - Successful off-subnet connectivity: Outbound internet access from the VM was successful through the NAT proving that that traffic can actually leave the VM's subnet and successfully use the default gateway to reach an external network. 
```

### Step 2 — Name the Correct Conclusion

For each of these four results, state what it actually proves: the Grid Beacon at `10.60.6.4` answering, the default route shown by `ip route`, a successful connection to a destination outside your local subnet, and the gateway's failed ping. Then state the rule you would give a junior colleague about the difference between an observation ("the gateway did not answer my ICMP probe") and a diagnosis ("the gateway is broken"):

```
The Grid Beacon at 10.60.6.4 answering proves local-subnet connectivity. The default route shown by 'ip route' proves that the default gateway is configured as the route out to reach other networks. A successful connection to a destination outside of the local subnet proves that traffic use the default to reach another gateway. The gateway's failed ping does not prove that the network or gateway is broken because the system may be designed not to respond an ICMP request. Therefore, this should not be solely treated as evidence. I would tell a junior colleague to collect evidence from their investigations and to be sure to distinguish between an observation and a diagnosis. I would tell my colleague to remember the Ladder Rule which is to test step by step, collect evidence, and use the evidence to determine what is broken. 
```

---

## Part D — Two Models, One Job

The OSI model has seven layers. The practical TCP/IP model most engineers speak day to day has four or five.

### Step 1 — Map Them

Briefly show how the seven OSI layers collapse into the practical model:

```
TCP/IP Model -  OSI layers
Application - OSI 7 (Application), OSI 6 (Presentation), OSI 5 (Session)
Transport - OSI 4 (Transport)
Internet - OSI 3 (Network)
Network Access - OSI 1 (Data Link and Physical)
```

### Step 2 — When Each Is Useful

Explain when the seven-layer vocabulary helps and when the practical model is the better tool:

```
You use the TCP/IP practical model to troubleshoot because it provides a simple map in a practitioner's head for understanding how network communication works. The OSI model provides more detail and is useful for documentation, certifications, and technical conversations when identifying specific layers. TCP/IP helps simplify troubleshooting, while OSI helps provide a more detailed vocabulary for describing where an issue occurs.
```

---

## Analysis Questions

**Analysis Question 1.** Explain the Ladder Rule using layer language. What does "test the near thing first" mean when the rungs are layers? *(Minimum 3 sentences.)*

```
The Ladder Rule means testing from the bottom and closest layer up in step by step phase working your way through each layer to collect concrete evidence of where the network problem is occurring. "Test the near thing first" means to start with the testing the things in the OSI layers closest to the machine then continue work through each step by step phase which extends to the outer layers. This provides evidence of they layers that are working and pinpoints where the issue is with evidence. 
```

**Analysis Question 2.** Why is "which layer is this?" a faster question than "what is broken?" when you are under pressure? *(Minimum 3 sentences.)*

```
Asking "which layer is this?" is more efficient because it is precise and points to an immediate location to help quickly provide information and identify the team needed to address the issue. The details of where the problem is occurring can then be shared. Identifying the layer helps focus on the investigation. 
```

**Analysis Question 3.** Pick one case file from Part B and describe the very next command you would run to confirm your ruling, and what result would change your mind. *(Minimum 2 sentences.)*

```
Case File 1 — The Name That Went Nowhere: A hostname lookup fails, but pinging the machine's IP address directly succeeds.

Since the ping to the IP address was successful this proves that the machine can be reached. The ping to the hostname failed which is can be an indication of a DNS failure so I would run 'dig [hostname]'. This would determine if the hostname can be resolved. If the dig returned the correct IP address that would change my mind because the successful dig proves the DNS is working. 
```

---

## Submission Checklist

- [x] All seven rows of the OSI table completed with a real Week 5–6 anchor each (Part A)

- [x] All five case files given a layer and supporting evidence (Part B)

- [x] Silent gateway case ruled on correctly (Part C)

- [x] OSI vs. practical TCP/IP model compared (Part D)

- [x] All three Analysis Questions answered (minimum sentence counts met)

- [x] No screenshot required for this lab

- [x] This file is committed to your portfolio repo at `week-06/labs/lab-05-layer-detective.md`

---

## GitHub Commit Subsection

1. Open **Week 6 → Lab 05: Layer Detective** in the Lab Portal.
2. Fill in the worksheet fields.
3. Click **Submit to GitHub** — the Portal commits to `week-06/labs/lab-05-layer-detective.md`.

---

*CyberVisionaries Institute · Cyber Foundations · Tier I*
