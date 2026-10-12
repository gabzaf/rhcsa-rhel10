# Day 3

**Course:** [Red Hat RHCSA RHEL 10 with Exam Labs](https://learning.oreilly.com/course/red-hat-rhcsa/9780135493137/) by Sander van Vugt (Pearson, O'Reilly Learning)

## Contents

- [Managing Network Configuration](#managing-network-configuration)
  - [IPv4 networking](#ipv4-networking)

---

## Managing Network Configuration

### IPv4 networking

![IPv4 Networking](images/day-03-ipv4-networking.webp)

Show the IP addresses of all interfaces:

```bash
ip a
```

![ip a](images/day-03-ip-a.png)

- `lo`: the loopback interface, used internally by services that use IP to communicate with one another. There I will always find the IP address `127.0.0.1` (`inet`) and `::1` (`inet6`).
- `enp0s3`: the name of my network device.
  - `altname`: an alternative name for the same device (`enx080027867b53`, based on the MAC address)
  - `inet 10.0.2.15/24`: the most important part, the IPv4 address and subnet mask
  - `dynamic`: the address was given by a DHCP server
  - `link/ether`: MAC address; `inet6 fd17:...`: IPv6 address; `inet6 fe80::...`: link-local IPv6, only valid on the local network
- `ip a` is short for `ip address show`.
