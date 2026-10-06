# Day 2

**Course:** [Red Hat RHCSA RHEL 10 with Exam Labs](https://learning.oreilly.com/course/red-hat-rhcsa/9780135493137/) by Sander van Vugt (Pearson, O'Reilly Learning)

## Contents

- [Module 3: Performing Basic System Management Tasks](#module-3-performing-basic-system-management-tasks)
  - [FHS (Filesystem Hierarchy Standard)](#fhs-filesystem-hierarchy-standard)
  - [Finding files](#finding-files)
  - [Mounts and devices](#mounts-and-devices)

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

### Finding files

Always use `find`, because it's the most flexible.

Search the whole file system (`/`) by name:

```bash
find / -name "hosts"
find / -name "*hosts*"
```

- `-name "hosts"`: exact name match
- `-name "*hosts*"`: any name containing `hosts` (`*` is a wildcard; keep the quotes so the shell doesn't expand it)

As a regular user, `find /` prints many `Permission denied` errors. Run it with `sudo`, or hide the errors with `2> /dev/null`.

Find files in `/etc` that contain the text `student`:

```bash
sudo find /etc -exec grep -l student {} \;
```

- `-exec <command> {} \;`: runs a command on each file found. `{}` is replaced by the file name, and `\;` ends the command.
- `grep -l`: prints only the names of files that contain the text, not the matching lines.

Add `-type f` (`find /etc -type f -exec ...`) to search only regular files and avoid `Is a directory` errors.

Hide the error messages by sending STDERR (`2>`) to `/dev/null`:

```bash
sudo find /etc -exec grep -l student {} \; 2> /dev/null
```

Copy every file that contains `student` to a directory:

```bash
mkdir -p find/contents
sudo find /etc -exec grep -l student {} \; -exec cp {} find/contents/ \; 2> /dev/null
```

- The second `-exec` runs only if the first one succeeds, so only files where `grep` found `student` are copied.
- Each `-exec` needs its own `\;` at the end. Without it, `find` fails with `missing argument to -exec`, and `2> /dev/null` hides that error, so nothing happens and nothing is shown.
- The target directory must exist first (`mkdir -p`).

Pass the results to another command with `xargs`. Find files in `/etc` that contain `127.0.0.1`:

```bash
sudo find /etc/ -name '*' -type f | xargs grep "127.0.0.1"
```

- `xargs` takes the file names from the pipe and passes them as arguments to `grep`. For example, if `find` outputs:

  ```
  /etc/hosts
  /etc/fstab
  /etc/passwd
  ```

  `xargs` turns that into one command:

  ```bash
  grep "127.0.0.1" /etc/hosts /etc/fstab /etc/passwd
  ```

  Without `xargs`, `grep` would search the *text* of the file names coming through the pipe, not the files themselves.
- `-name '*'` matches everything, so it can be left out.
- `sudo` applies only to `find`; `grep` runs as your user, so some files give `Permission denied`. Use `sudo xargs grep` to read them all.

Run the whole pipeline as root with `sudo sh -c`:

```bash
sudo sh -c "find /etc/ -name '*' -type f | xargs grep 127.0.0.1"
```

`sudo` normally applies only to the first command of a pipe. `sh -c "..."` starts a new shell as root that runs the entire command line, so both `find` and `grep` run as root and there are no `Permission denied` errors.

### Mounts and devices

Show what's mounted and which block devices exist:

```bash
mount
findmnt
lsblk
```

- `mount`: lists all mounted file systems (device, mount point, type, options). Long and hard to read, because it includes many virtual file systems.
- `findmnt`: the same information as a tree, showing which mount sits under which. Easier to read.
- `lsblk`: lists block devices (disks and partitions, such as `sda`, `sda1`) with their size, type and mount point.

`mount` output is huge because most of it is virtual file systems (`proc`, `sysfs`, `cgroup`, `tmpfs`…). Ways to filter it:

```bash
mount | grep '^/dev'   # only real disks
mount -t xfs           # only one file system type
findmnt --real         # tree without virtual file systems
findmnt /              # what's mounted at one place
df -h                  # sizes and free space
```
