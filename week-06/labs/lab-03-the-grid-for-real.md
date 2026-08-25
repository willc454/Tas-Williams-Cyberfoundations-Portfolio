# Week 6 Lab 03 — The Grid, For Real

**Student Name:** Catasia Williams

**Date Completed:** August 21, 2026

**Module:** 2 — Networking & Cloud Foundations | **Week:** 6  
**Submission Path:** `week-06/labs/lab-03-the-grid-for-real.md`

---

> ### 🔒 Cloud Heights Security Rule
> Your Bastion link and Cloud Heights password are **private access credentials**. Never paste either into a worksheet, screenshot, GitHub repository, Circle post, or chat message. When taking screenshots, crop out the browser address bar and all login information.

---

## Overview

In Week 5 you ran `ip addr`, `ip route`, `ping`, and `traceroute` in a simulator that always behaved. Today you run the same toolkit against real cloud infrastructure that does **not** always behave the way the textbook implies — and you learn to tell "broken" apart from "normal."

This is an **independent** lab. It tells you what to accomplish; you choose the commands. Expect about 40 minutes.

---

## Lab Environment / Pre-Lab Check

| Component | Details |
|---|---|
| Environment | Cloud Heights — live Ubuntu 22.04 VM, reached through Azure Bastion |
| Commands used | `ip addr`, `ip route`, `ping`, `traceroute`, `curl` |
| Known-good target | **Grid Beacon — `10.60.6.4`** |
| Prerequisite | Week 6 Labs 01–02 |

---

## Part A — Where You Actually Are

### Step 1 — Read Your Own Address

Run the command that lists your interfaces and addresses.

Command and output:

```
ip addr
```

Your private IPv4 address and prefix length:

```
inet: 10.60.6.22/26
```

### Step 2 — Read Your Route

Run the command that shows the routing table.

Command and output:

```
ip route
```

Your default gateway:

```
default via 10.60.6.1
```

### Step 3 — Compare to Week 5

Compare this live Ubuntu output to what the CLI Simulator produced in Week 5. What looks the same, what looks different, and what surprised you:

```
The live Ubuntu output is more detailed/characters that what the CLI Simulator produced. The information is essentially the same. The command provides the same results the look of the output is just different. I was surprised that there was so much details with the Ubuntu output. 
```

---

## Part B — The Gateway That Does Not Answer

### Step 1 — Ping the Gateway

Ping the default gateway address you recorded. Let it run a few seconds, then stop it.

Command and output:

```
ping 10.60.6.1
```

### Step 2 — Interpret It Correctly

You almost certainly got **no replies**. In Azure, the platform gateway commonly does not answer ICMP. This is **expected platform behaviour** and by itself proves nothing about whether your machine or network is broken.

Explain why "the gateway did not answer ping" is weak evidence:

```
The gateway did not answer ping is weak evidence because the Azure platform gateway may be configured not to respond to ICMP requests. The platform may still be functioning normally and route traffic even though it does not provide a response to ping. This can't immediately be treated as a network failure and more evidence should be collected through using the ladder rule by checking the VM's connection using the ip addr command, checking the routing information by using ip route, checking a known-good target, and using the curl command to test if the known-good target's service is working.

```

---

## Part C — The Known-Good Target

The **Grid Beacon** at `10.60.6.4` is a machine that is known to be up and known to answer. When your first probe fails, you test against something known-good before you conclude anything.

### Step 1 — Ping the Beacon

```
ping 10.60.6.4
```
Output:

```
PING 10.60.6.4 (10.60.6.4) 56(84) bytes of data.
64 bytes from 10.60.6.4: icmp_seq=1 ttl=64 time=1.65 ms
```

### Step 2 — Trace the Path

```
traceroute 10.60.6.4
```
Output:

```
traceroute to 10.60.6.4 (10.60.6.4), 30 hops max, 60 byte packets
 1  * grid-beacon.internal.cloudapp.net (10.60.6.4)  2.035 ms  1.958 ms
```

### Step 3 — Ask the Application

```
curl http://10.60.6.4
```
Output:

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GRID BEACON | CVI CyberFoundations</title>
    <style>
        body {
            background: #071426;
            color: #d9f7ef;
            font-family: monospace;
            max-width: 850px;
            margin: 80px auto;
            padding: 30px;
        }
        .beacon {
            border: 1px solid #31d6a6;
            padding: 35px;
        }
        h1 { color: #31d6a6; }
        .label { color: #8ca8ff; }
        .status { color: #31d6a6; }
        .classified {
            margin-top: 30px;
            border-top: 1px solid #31445e;
            padding-top: 20px;
        }
    </style>
</head>
<body>
<div class="beacon">

    <h1>GRID BEACON</h1>

    <p><span class="label">NODE:</span> grid-beacon</p>
    <p><span class="label">NETWORK:</span> CVI Training Grid</p>
    <p><span class="label">STATUS:</span>
       <span class="status">ONLINE</span></p>

    <p>
        Network beacon established.<br>
        If you reached this node, your route is operational.
    </p>

    <div class="classified">
        <p>INVESTIGATION CHECKPOINT</p>

        <p>
            Observe the path that brought you here.
            The destination is only part of the story.
        </p>

        <p>TRACE ID: CF-NET-0604</p>
    </div>

</div>
</body>
</html>

```

> ### ⚠️ Grid Beacon not responding?
> The Grid Beacon is shared course infrastructure and should normally be available. First, confirm your Cloud Heights VM shows **Running** and that you completed the preceding network checks. Then retry the command once after a minute or two.
>
> If the Grid Beacon still does not respond, **stop this part of the lab and contact your instructor.** Record that the shared service was unavailable; do not treat the result as evidence that your VM or your work is incorrect.
>
> Do not change networking, NSGs, firewall rules, routes, DNS, or any Azure settings to try to reach the beacon.
>
> *Instructor note: a confirmed Grid Beacon outage is an environment issue, not a student error. Affected students may complete this portion of Lab 03 after the service is restored, with no penalty.*

### Step 4 — Record the Application Evidence

The beacon returns a banner and a trace ID. Record exactly what you received:

```
Banner:GRID BEACON | CVI CyberFoundations
trace ID: CF-NET-0604
```

Explain the difference between what the `ping` proved and what the `curl` proved:

```
The ping command proved that the VM could reach grid-beacon and receive a response over the network (the ICMP response) proving network connectivity. The curl command proved that the machine could actually connect to the web service on grid-beacon and receive an HTTP response. The ping command confirms network reachability and the curl command confirms that the web service is accessible. 
```

### Step 5 — Capture Your Evidence

Two screenshots, both cropped to the terminal only:

**Required filename:** `vm-toolkit-live.png` — your `ip addr` and `ip route` output

![Live VM toolkit — ip addr and ip route](https://raw.githubusercontent.com/willc454/Tas-Williams-Cyberfoundations-Portfolio/refs/heads/main/assets/screenshots/week-06/vm-toolkit-live.png)

**Required filename:** `beacon-reply.png` — your beacon ping/traceroute/curl evidence

![Grid Beacon reply](https://raw.githubusercontent.com/willc454/Tas-Williams-Cyberfoundations-Portfolio/refs/heads/main/assets/screenshots/week-06/beacon-reply.png)

---

## Part D — Rewrite the Ladder Rule

Week 5 taught the Ladder Rule: test the near thing before the far thing. Real infrastructure adds a wrinkle — a silent rung is not automatically a broken rung.

Rewrite the Ladder Rule in your own words so that it survives real cloud infrastructure. Your version must include both **route/path evidence** and **a known-good target**:

```
The ladder rule is to test the closet part of the network first and not to assume that a failed response means that that part is broken. Best practice is to use commands route/path evidence to determine if traffic is reaching the target destination by using a known-good target for the test. A known-good target can be used as evidence that helps determine if the network is actually working before deciding to investigate further. 
The Rung Ladder:
Rung 1 - Link and Address: Check if computer has a working network connection and valid IP address.
Rung 2 - Gateway: Checks if the computer can reach its default gateway to communicate with other networks.
Rung 3 - Remote Host: Checks if the destination can be reached.
Rung 4 - Name Resolution: Checks if the hostname can be translated to the correct IP address using DNS.
Rung 5 - Service and Application: Checks if the port is open and the application responding.
```

---

## Analysis Questions

**Analysis Question 1.** Your ping to the gateway failed and your ping to the beacon succeeded. What does that pair of results, taken together, prove about your machine's networking? *(Minimum 3 sentences.)*

```
A failed ping to the gateway does not necessarily mean that my machine's networking is broken. Since the ping to the beacon succeeded, it proves that my machine can send network traffic and receive a response from another system. Together, these results show that my machine has working network connectivity, even though the gateway itself did not respond to the ping.
```

**Analysis Question 2.** Why is `traceroute` useful even when `ping` already answered? What extra thing does it show you? *(Minimum 2 sentences.)*

```
Ping is useful to know if the destination responds and the response time. Traceroute is useful because it provides additional information by showing the network path and each hop (and respective time) the traffic takes to reach the destination. This can help identify where a connection issue is.
```

**Analysis Question 3.** A service is unreachable and ping to it succeeds. Where would you look next, and why is "the network is fine" an incomplete answer? *(Minimum 3 sentences.)*

```
A successful ping only proves that the device or server can be reached over the network; it does not prove that the specific service can be accessed. A successful ping only proves that the web server can be reached over the network; it does not prove that the specific service can be accessed. For example, if a user reports that they can’t access the company website and I successfully ping the web server, I know that the web server is indeed reachable. However, I still need to determine if the web server is accepting connections. I would then have to check the HTTPS port (443) to determine if the web service can be reached, since I already know that the web server itself can be reached.
```

**Analysis Question 4.** Something already controls what is allowed to reach your machine in Cloud Heights. If you could decide those rules, what would you want to allow, what would you want to block, and who in an organization should get to make that decision? *(Minimum 3 sentences.)*

```
I would want to allow only what is absolutely necessary and default to the least privilege best practice. I would allow SSH authorization for employees who absolutely need remote access to the VM to perform their job functions. I would also allow necessary port connections for services the VM needs to use. I would block other types of port connections that are not necessary for the VM's functions. Administrators should make these decisions.
```

---

## Submission Checklist

- [x] `ip addr` output recorded and own private IP/prefix identified (Part A)

- [x] `ip route` output recorded and default gateway identified (Part A)

- [x] Live output compared to the Week 5 simulator (Part A, Step 3)

- [x] Gateway pinged and the silent result interpreted correctly (Part B)

- [x] Beacon `ping`, `traceroute`, and `curl` all run and recorded (Part C)

- [x] Beacon banner and TRACE ID recorded (Part C, Step 4)

- [x] `vm-toolkit-live.png` and `beacon-reply.png` captured, cropped, uploaded to `assets/screenshots/week-06/` (Part C, Step 5)

- [x] Ladder Rule rewritten with route evidence + known-good target (Part D)

- [x] All four Analysis Questions answered (minimum sentence counts met)

- [x] This file is committed to your portfolio repo at `week-06/labs/lab-03-the-grid-for-real.md`

---

## GitHub Commit Subsection

1. Open **Week 6 → Lab 03: The Grid, For Real** in the Lab Portal.
2. Fill in the worksheet fields and upload both screenshots to `assets/screenshots/week-06/`.
3. Click **Submit to GitHub** — the Portal commits to `week-06/labs/lab-03-the-grid-for-real.md`.

---

*CyberVisionaries Institute · Cyber Foundations · Tier I*
