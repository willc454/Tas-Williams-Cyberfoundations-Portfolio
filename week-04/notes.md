# Week 4 Notes — Permissions, Searching, and Virtual Machines

**Student Name:** Catasia Williams

**Date Completed:** August 9, 2026

Summarize this week's key concepts in your own words — not copy-pasted definitions.

## Key Concepts This Week

- File permissions: read/write/execute × owner/group/other, and reading `ls -l`
- Changing permissions with `chmod` (symbolic and numeric) — and THE GATEKEEPER'S RULE
- Windows ACLs, read with `Get-Acl`/`icacls`
- Wildcards (`*`, `?`, `[ ]`) and searching inside files with `grep`/`Select-String`
- Virtual machines: host vs. guest, the hypervisor, Type 1 vs. Type 2, isolation
- The VM lifecycle: create, start, stop (deallocate), snapshot, delete — and what each costs
- Golden snapshots — how your Weeks 6–12 lab machines are made

## In My Own Words

**Decode `-rw-r-----` audience by audience: who can do what to this file?**

```
The first audience is the owner, the second audience is the group, and the third audience is others. The owner can read and write on this file and the group can read this file. The others audience does not have any permission to the file. 
```

**What is a hypervisor, and what are its two jobs?**

```
The hypervisor is a software that bridges the host VM to the guest VMs. It allocates the hosts resources (CPU time, memory, disk) amongst the guest VMs. It also ensures that each of the guest VMs remains isolated from the others. 
```

**A stopped VM still costs a little money. What is it paying for, and what's the only way to reach a true zero?**

```
A stopped VM still has costs because it is still active. That cost can be described as the locker fee because the VM is still utilizing the host's resources even though it is stopped. The only way to reach a true zero cost is to delete the VM which stops all usage of the host's resources, deletes all data, and is permanent. 
```

---

## Submission Checklist

- [x] I summarized each concept in my own words, not copied definitions

- [x] I answered all three "In My Own Words" prompts

- [x] This file is committed to my portfolio repo at `week-04/notes.md`
