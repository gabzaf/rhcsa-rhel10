# rhcsa-rhel10

My RHCSA (EX200) exam prep on **Red Hat Enterprise Linux 10**: lab setup, daily study notes, command cheat sheets and labs.

> **Status:** 🟡 Just started (October 2026)

---

## Goal

Pass the **Red Hat Certified System Administrator (RHCSA, EX200)** exam on RHEL 10.

- **Exam:** EX200, performance-based, hands-on (no multiple choice)
- **Target exam date:** _TBD_

## Main resource

**Red Hat RHCSA (RHEL 10) with Exam Labs** by Sander van Vugt (Pearson, August 2025, RHEL 10 edition), a video course on O'Reilly Learning.

Supporting resources:

- [Official EX200 exam objectives](https://www.redhat.com/en/services/training/ex200-red-hat-certified-system-administrator-rhcsa-exam), the source of truth for what's on the exam
- `man` pages and `/usr/share/doc`, the only documentation available during the exam

## Lab environment

| Item     | Setup                                              |
|----------|----------------------------------------------------|
| Host     | Linux + VirtualBox                                 |
| Guest OS | RHEL 10 (free Red Hat Developer Subscription)      |
| VM       | 2 vCPU · 4 GB RAM · 20 GB system disk              |

## Repository structure

```
rhcsa-rhel10/
├── README.md          # this file: goal, plan, progress
├── notes/             # day-01.md … day-05.md, notes per study day
├── cheatsheets/       # quick command references per topic
└── labs/              # practice tasks + my solutions
```

## Study plan

Five intensive study days within the O'Reilly 10-day trial, plus review time.

| Day | Date | Course lessons | Notes | Done |
|-----|------|----------------|-------|------|
| 1   |      |                | [day-01](notes/day-01.md) | ⬜ |
| 2   |      |                | [day-02](notes/day-02.md) | ⬜ |
| 3   |      |                | [day-03](notes/day-03.md) | ⬜ |
| 4   |      |                | [day-04](notes/day-04.md) | ⬜ |
| 5   |      |                | [day-05](notes/day-05.md) | ⬜ |

For each lesson: **watch → reproduce in the VM → write notes → do the lab without notes**.

## Exam topics checklist

High-level areas covered by the RHCSA. Check them against the official objectives page, which may differ for RHEL 10.

- [ ] Essential tools: shell, redirection, `grep`, archives, file permissions, `man`
- [ ] Shell scripting basics
- [ ] Operating running systems: boot targets, processes, logs, tuning
- [ ] Local storage: partitions, LVM, swap
- [ ] File systems: create, mount, `/etc/fstab`, NFS / autofs
- [ ] Deploy, configure and maintain systems: software (`dnf`), scheduling, services, bootloader
- [ ] Basic networking: IPv4/IPv6 config, hostname, firewalld
- [ ] Users and groups: accounts, passwords, password aging, sudo
- [ ] Security: firewalld, SSH keys, SELinux (modes, contexts, booleans, ports)
- [ ] Recovery: reset root password, fix boot issues

## Cheat sheets

| Topic | File |
|-------|------|
| LVM | [cheatsheets/lvm.md](cheatsheets/lvm.md) |
| Users & groups | [cheatsheets/users.md](cheatsheets/users.md) |
| systemd | [cheatsheets/systemd.md](cheatsheets/systemd.md) |
| SELinux | [cheatsheets/selinux.md](cheatsheets/selinux.md) |
| firewalld | [cheatsheets/firewalld.md](cheatsheets/firewalld.md) |

## Lab log

| # | Lab | Result | Time | Notes |
|---|-----|--------|------|-------|
|   |     |        |      |       |

## 💡 Lessons learned

_Mistakes and things I'd do differently. Filled in as I go._

---

⚠️ This repo has only my own notes and solutions. No course material, no ISOs, no credentials.
