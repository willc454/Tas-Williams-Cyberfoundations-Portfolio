# Week 5 Notes — The Grid: Addresses, Names, Ports, and Diagnostics

**Student Name:** Catasia Williams

**Date Completed:** August 16, 2026

Summarize this week's key concepts in your own words — not copy-pasted definitions.

## Key Concepts This Week

- IP addresses — the dotted-quad number every device on a network needs (`10.20.5.42` on The Grid)
- The subnet mask — the answer to "which addresses are my neighbours?" (`/24` = `255.255.255.0`)
- The default gateway — the door out of your neighbourhood (`10.20.5.1` on The Grid)
- Private vs public addresses — `10.x`, `172.16–31.x`, and `192.168.x` are *inside* addresses
- DNS — the Grid's Directory Board: a name goes in, an IP address comes out
- NXDOMAIN vs a host that resolves but is down — two different failures with two different causes
- DHCP — the Address Office: leases, why addresses change, why a laptop "just works" on a new network
- Ports — the numbered doors on a building: 22 SSH, 53 DNS, 80 HTTP, 443 HTTPS, 3389 RDP, 25 SMTP
- TCP vs UDP — a confirmed conversation vs a shout across the room
- The TCP handshake — SYN → SYN-ACK → ACK (packets 7, 8 and 9 in Lab 03)
- The diagnostic toolkit — `ping` (is it alive?), `traceroute` (where does it stop?), `dig` (what number is behind that name?)
- **THE LADDER RULE** — check yourself → check your gateway → check the target by NAME → check the target by IP → trace the path. *Work outward, one rung at a time, and let the evidence pick the culprit.*

## My Command Table

You learned the same five jobs twice this week — once in bash, once in PowerShell. Fill the pairs in from memory if you can, and check them afterwards. This table is worth keeping.

The bash command and its PowerShell equivalent for each job — show my own address, show my default gateway, test reachability, trace the path, look up a name:

```
Activity: Bash/Powershell
Show my address: ip addr / ipconfig
Show my default gateway: ip route / ipconfig
Test reachability: ping [address] / Test-Connection [address]
Trace the path: traceroute [address] / tracert [address]
Look up a name: dig [host name] / Resolve-DnsName [host name]
```

## In My Own Words

Your machine has three numbers: an address, a subnet mask, and a default gateway. Explain what each one is for, the way you'd explain it to someone who has never heard those words.

```
IP address: Identifies your specific machine on the network. For example, 10.20.5.42 is the address of your workstation.

Subnet mask: Tells your machine which other IP addresses are on the same local network. For example, /24 means addresses starting with 10.20.5 are on the same local network.

Default gateway: Tells your machine where to send traffic when the destination is outside the local network. For example, 10.20.5.1 is the gateway your workstation uses to reach other networks.
```

What does DNS actually do? Include the difference between a name that comes back "Name or service not known" (NXDOMAIN) and a name that resolves perfectly well to a host that never answers.

```
DNS translates a hostname into an IP address. 

“Name or service not known” (NXDOMAIN) means the name does not exist in DNS, so no IP address is returned. This could be caused by a typo, nonexistent hostname, or a decommissioned host.

When a name resolves but host does not answer means the DNS works correctly and provides an IP address, but the computer cannot get a response from that destination. The address is known but it can't be reached. The problem is can be  beyond the number look up like an issue network path, at the destination, or something blocking the connection.

```

An IP address gets your traffic to the right building. What does a port number add to that, and why would a defender care how many doors are open?

```
An IP address identifies the device. A port number identifies the specific service on that device that should receive the communication; for example, port 443 is commonly used for HTTPS.

A defender cares about how many ports are open because each open port provides a means for network traffic. More open ports means more networks that need to be secured because they present more opportunities for an attacker to find a weakness.
```

Write out THE LADDER RULE — all five rungs, in order — and say why running them in that order matters more than running them fast.

```
The Ladder Rule: 
Rung 1: Check your IP address (ip addr) — to ensure your machine has a valid address.

Rung 2: Check your gateway (ping [gateway]) — to ensure you can reach your gateway and get out of your local network.

Rung 3: Check the target by name (ping [hostname]) — to see if the hostname resolves to an IP address and whether that destination responds.

Rung 4: Check the target by IP address (ping [address]) — to test the destination without using the name.. If the IP works but the name doesn't, the problem is with the name/DNS; if both fail, the problem is not the name/DNS

Rung 5: Trace the path (traceroute [name or address]) — to see how far the traffic gets and where along the network path the problem may be. 

Completing this sequence matters more than the speed of solving an issue because each step rules out a potential issues (or validates an issue). Doing this allows for effective investigation and reducing the chance of investigating the wrong parts of the network. 
```

What is DHCP, and why does your laptop get an address automatically on a network it has never joined before, while a server like `grid-dns` keeps the same address permanently?

```
DHCP stands for Dynamic Host Configuration Protocol. The DHCP automatically gives an IP address, subnet mask, and default gateway. This automatic assignment does not require configuration which is why a laptop can get automatically get on a network it has never joined before without being configured. Some addresses are dynamic, leased and are renewable like the ones a laptop would receive when it connects at different locations. Some address are static and permanent so they are used for things like servers. These addresses typically need to be found on a regular basis so the address need to be readily found which is not the case for a personal laptop. 
```

---

## Submission Checklist

- [x] I summarized each concept in my own words, not copied definitions

- [x] I completed the bash-to-PowerShell command table

- [x] I answered all five "In My Own Words" prompts

- [x] This file is committed to my portfolio repo at `week-05/notes.md`

---

*CyberVisionaries Institute — Cyber Foundations, Tier I*
