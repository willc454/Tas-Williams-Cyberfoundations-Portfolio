# Week 6 Notes — Cloud Heights: Cloud VMs, SSH, VNets & Layers

**Student Name:** Catasia Williams

**Date Completed:** August 23, 2026

Summarize this week's key concepts in your own words — not copy-pasted definitions. This week moved from the simulated Grid into a real cloud environment, so focus on what you personally observed as well as what each term means.

> **Cloud Heights Security Rule:** Your Bastion shareable link and Cloud Heights password are private access credentials. Never paste either into this file, a screenshot, your GitHub repository, Circle, or a chat message.

## Key Concepts This Week

- **Cloud** — other people's computers, professionally operated and reached over a network
- **Datacenter** — the physical facility where cloud computing equipment lives
- **Region** — a geographic area where a cloud provider operates datacenters
- **Virtual machine (VM)** — a computer created in software; in Cloud Heights, your VM runs on hardware in a real datacenter
- **IaaS / PaaS / SaaS** — different levels of cloud service: rent the room, rent the workshop, or rent the finished service
- **Shared responsibility model** — the cloud provider secures the building and underlying platform; the customer is still responsible for what belongs to them
- **Provisioning** — creating and preparing a resource so it is ready to use
- **Golden image / snapshot** — a known starting point that can be used to create consistent machines
- **Snapshot vs backup** — a snapshot is a point-in-time copy used for recovery or cloning; a backup is a separate recovery copy with a different purpose
- **Azure Bastion** — the guarded front desk that gives you browser-based SSH access without giving your VM a public IP
- **Bastion shareable link** — sensitive access information that must never be committed to GitHub or exposed in screenshots
- **SSH (Secure Shell)** — remote command-line access to another machine
- **SSH client and server** — the client starts the connection; the server listens and answers
- **Port 22** — the standard numbered door used by SSH
- **Host / fingerprint verification** — the verify-before-approve habit when connecting to a host for the first time
- **Authentication** — proving that you are the account you claim to be
- **Remote session / remote shell** — the live command-line session running on another machine
- **Getting TO vs getting INTO a machine** — network reachability and authentication are different problems
- **`hostname`** — asks which machine you are on
- **`whoami`** — asks which account you are using
- **`pwd`** — asks where you are in the filesystem
- **Private IP address** — an address used inside a private network rather than directly on the public internet
- **Virtual network (VNet)** — the private cloud neighborhood where resources communicate
- **Subnet** — a smaller address range inside a VNet; a floor inside the larger building
- **NAT / outbound translation** — lets a privately addressed machine communicate outward without giving the machine its own public IP
- **Network Security Group (NSG)** — the network guard post that controls what traffic is allowed; you take control of these rules in Week 7
- **Known-good reference point** — a target whose expected behavior gives you something reliable to compare against
- **Grid Beacon** — the known-good Cloud Heights host at `10.60.6.4`
- **The silent Azure gateway** — Azure's default gateway may not answer ICMP ping even when the network is healthy
- **OSI model** — the seven-layer vocabulary used to organize network and application behavior
- **TCP/IP model** — the more compact layer model commonly used by practitioners
- **Layers** — a way to separate different jobs in a communication path so troubleshooting can be systematic
- **Encapsulation** — information travelling inside other information, like a letter inside an envelope inside a mailbag
- **The Ladder Rule in the real cloud** — work outward, prove what works, use the route and a known-good target, and never let one silent tool response choose the culprit by itself

## My Cloud Heights Command Table

You used these commands on a real Ubuntu machine this week. Instead of memorizing syntax, write down the **question each command answers** or the job it performs.

| Command | What question does it answer / what does it do? |
| --- | --- |
| `hostname` | Identify the name of the machine |
| `whoami` | Identify the user using the machine |
| `pwd` | Shows current location |
| `ip addr` | Show IP address |
| `ip route` | Shows how traffic leaves the machine by providing the default gateway |
| `ping` | Tests if the device can be reached |
| `traceroute` | Shows network paths/hops from and to your chosen destinations |
| `dig` | Uses DNS to provide IP address associated with a hostname |
| `curl` | Connections to a service or application to determine if the application or service is working |
| `ssh` | Stands for Secure Shell. A program/tool that opens encrypted connection to another machine |
| `exit` | Closes the remote shell and returns to the machine but the VM keeps running |

## In My Own Words

### 1. Getting TO vs Getting INTO

Explain the difference between getting **TO** a machine and getting **INTO** a machine. Use something you personally observed in Cloud Heights as evidence.

```
Getting to a machine indicates that the network is working. Getting into a machine requires authentication using credentials (such as usernames and passwords). 
```

### 2. The Silent Gateway

Your Azure gateway did not answer `ping`, but your VM was still healthy. Explain how you proved the network was working and what this taught you about interpreting tool output.

```
The Azure gateway did not answer ping because it was designed not to respond to ICMP requests. I proved the network was working by using ping for a known-good target (the Beacon). This taught me that  a failed ping does not always mean a network is broken.
```

### 3. Private on the Inside, Connected to the Outside

Explain how your Cloud Heights VM can reach the internet even though it has only a private IP address. Then explain how **you** reach the VM from outside its VNet.

```
The VM has a private address and can reach the internet through Azure Bastion. Azure Bastion provides secure connections for the VM. The VM can be reached from outside its VNET through this secure connection which allows for the VM to not need a public address. The traffic between the browser and the VM is scrambled in transit so nothing in between can read it. 

```

### 4. VNet vs Subnet

Explain the difference between a VNet and a subnet using the Cloud Heights building/floor analogy. Then explain why separating systems into smaller network ranges can help security.

```
A VNet is a virtual network that provides a private network within the cloud and controls communication; it cannot be reached from outside of the cloud without permission. A subnet is a slice of the VNet. The VNet can be described as a physical building and a subnet can be described as one floor in the building. The subnet separates systems into smaller network ranges. Segmentation through the use of subnets helps secure networks by maintaining boundaries and controlling traffic. If a machine is compromised on one floor or an error is made, segmentation can help limit the impact to that subnet and help keep it within the subnet's boundary instead of allowing it to spread throughout the entire network.

```

### 5. The Ladder Rule Has a Map Now

The Ladder Rule never used the words OSI or TCP/IP. Explain how the layer models give you a map for the same troubleshooting process you have already been using.

```
The layer models map troubleshooting by starting with the basic, lower-level functions and progressively moving the investigation outward and to higher-level functions to more specific parts of the network proving what does work along the way. 
```

---

## Submission Checklist

- [x] I summarized the Week 6 concepts in my own words, not copied definitions

- [x] I completed my Cloud Heights command table

- [x] I explained getting TO vs getting INTO a machine

- [x] I documented what the silent Azure gateway taught me

- [x] I explained the Cloud Heights private-network design

- [x] I connected the Ladder Rule to network layers

- [x] I checked that my Bastion shareable URL does not appear anywhere in this file

- [x] I checked that my Cloud Heights password does not appear anywhere in this file

- [x] This file is committed to my portfolio repo at `week-06/notes.md`

---

*CyberVisionaries Institute — Cyber Foundations, Tier I*
