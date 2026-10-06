# Day 2

**Course:** [Red Hat RHCSA RHEL 10 with Exam Labs](https://learning.oreilly.com/course/red-hat-rhcsa/9780135493137/) by Sander van Vugt (Pearson, O'Reilly Learning)

## Contents

- [Module 3: Performing Basic System Management Tasks](#module-3-performing-basic-system-management-tasks)
  - [FHS (Filesystem Hierarchy Standard)](#fhs-filesystem-hierarchy-standard)

---

## Module 3: Performing Basic System Management Tasks

### FHS (Filesystem Hierarchy Standard)

The FHS defines where things live on a Linux system. The directories that matter most:

| Directory | Contains |
|-----------|----------|
| `/` | Root of the file system; everything starts here |
| `/boot` | Kernel and files needed to boot (GRUB config, initramfs) |
| `/etc` | System configuration files (`/etc/passwd`, `/etc/fstab`, service configs) |
| `/home` | Home directories of regular users (`/home/anna`) |
| `/root` | Home directory of the root user |
| `/var` | Variable data that changes while the system runs: logs (`/var/log`), mail, caches, web content (`/var/www`) |
| `/tmp` | Temporary files, cleaned up automatically |
| `/usr` | Programs, libraries and documentation (`/usr/bin`, `/usr/share/doc`, man pages) |
| `/opt` | Optional third-party software |
| `/dev` | Device files (disks such as `/dev/sda`, terminals) |
| `/proc`, `/sys` | Virtual file systems with kernel and hardware info (e.g. `/proc/cpuinfo`) |
| `/run` | Runtime data since the last boot (PID files, sockets) |
| `/mnt`, `/media` | Mount points: `/mnt` for manual mounts, `/media` for removable media |

On RHEL, `/bin`, `/sbin` and `/lib` are links to their `/usr` versions.

For the full list, run `man hier`.
