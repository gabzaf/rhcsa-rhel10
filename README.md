# rhcsa-rhel10

My RHCSA (EX200) exam prep on **Red Hat Enterprise Linux 10**: lab setup, daily study notes, command cheat sheets and labs.

> **Status:** 🟡 In progress: Module 3, Lesson 9 (October 2026)

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
| Guest OS | RHEL 10.2, ISO from the free Red Hat Developer Subscription; system not registered (like the exam) |
| VM       | 2 vCPU · 4 GB RAM · 20 GB system disk, BIOS firmware |
| Disk layout | `sda1` biosboot 1 MiB · `sda2` `/` 10 GiB (xfs) · `sda3` swap 1 GiB · ~9 GiB unused (Lesson 2 lab) |

## Repository structure

```
rhcsa-rhel10/
├── README.md          # this file: goal, plan, progress
├── notes/             # day-01.md … day-05.md, notes per study day
│   └── images/        # screenshots and course slides used in the notes
├── cheatsheets/       # quick command references per topic (planned)
└── labs/              # practice tasks + my solutions (planned)
```

## Study plan

Five intensive study days within the O'Reilly 10-day trial, plus review time.

| Day | Date | Course lessons | Notes | Done |
|-----|------|----------------|-------|------|
| 1   | 2026-10-05 – 06 | Modules 1–2, lessons 1–5: RHEL, installation, basic tasks, essential tools, bash | [day-01](notes/day-01.md) | ✅ |
| 2   | 2026-10-06 – 09 | Module 3, lessons 6–9: file management, text files, root/sudo, users and groups | [day-02](notes/day-02.md) | 🟡 |
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

_Planned, not written yet._

| Topic | File |
|-------|------|
| LVM | [cheatsheets/lvm.md](cheatsheets/lvm.md) |
| Users & groups | [cheatsheets/users.md](cheatsheets/users.md) |
| systemd | [cheatsheets/systemd.md](cheatsheets/systemd.md) |
| SELinux | [cheatsheets/selinux.md](cheatsheets/selinux.md) |
| firewalld | [cheatsheets/firewalld.md](cheatsheets/firewalld.md) |

## Lab log

| # | Lab | Result | Notes |
|---|-----|--------|-------|
| 2 | Installing RHEL | ✅ | Custom partitioning; needed a biosboot partition on a BIOS VM |
| 4 | Using essential tools | ✅ | man, useradd, passwd, vim |
| 5 | Using the bash shell | ✅ | Variable in `~/.bash_profile`, alias in `~/.bashrc`, `HISTFILESIZE` |
| 6 | Essential file management tools | ✅ | `tar -czf`, symlink in `/tmp`, broken link after removing the archive |
| 7 | Working with text files | ✅ | Fixed tasks 4–5: `grep -w`, no `-l` when lines are asked |
| 8 | Configuring sudo | ✅ | First try had wrong paths (`/user`) and a typo in `timestamp_type` |
| 9 | Managing users and groups | ⬜ | |

## 💡 Lessons learned

_Mistakes and things I'd do differently. Filled in as I go._

- A GPT disk needs a boot partition: `biosboot` (1 MiB) on BIOS, `/boot/efi` on UEFI.
- In `tar`, `f` goes last (`-czf`): it takes the next word as the file name.
- Use absolute targets for symlinks; relative ones resolve from the link's location.
- `sudo cmd > file`: the redirection is done by my shell, not by root. Use `sudo sh -c "..."` or `tee`.
- `usermod -G` without `-a` removes all other secondary groups.
- sudoers rules need exact full paths (`/usr/sbin/...`); check with `which`.
- `2>/dev/null` also hides my own syntax errors (missing `\;` in `find -exec`).

---

⚠️ This repo has my own notes and solutions, plus screenshots of course slides for personal study reference. No ISOs. The only passwords shown are throwaway ones from the lab VM.
