# Networking basics #1

## Description

This project builds on networking fundamentals by focusing on localhost, the hosts file, IP address assignment, and practical network tools (`ifconfig`, `nc`, `telnet`, `cut`). Scripts are written in Bash and run on Ubuntu 22.04.

## Resources

| Resource | What it teaches |
|----------|----------------|
| What is localhost | `localhost` → loopback address `127.0.0.1`; traffic never leaves the machine |
| What is 0.0.0.0 | Means *all local IPv4 interfaces*; used when a server wants to listen everywhere |
| What is the hosts file | `/etc/hosts` maps hostnames to IPs *before* DNS is consulted |
| Netcat examples | `nc` opens raw TCP/UDP connections; useful for listening on ports and sending data |
| `man ifconfig` | Displays active network interfaces and their assigned IP addresses |
| `man telnet` | Connects to host:port to verify a service is reachable |
| `man nc` | Netcat — listen or connect; send/receive raw data over TCP/UDP |
| `man cut` | Parses specific columns/fields from text output |

## Learning Objectives

- What is `localhost` / `127.0.0.1`
- What is `0.0.0.0`
- What is `/etc/hosts` and how hostname resolution works
- How to display your machine's active network interfaces

## Requirements

- All scripts interpreted on Ubuntu 22.04
- All files end with a new line
- All Bash scripts must be executable (`chmod +x`)
- Scripts must pass `shellcheck` (version 0.7.0) without errors
- First line: `#!/usr/bin/env bash`
- Second line: a comment explaining what the script does

---

## Tasks

### 0. Change your home IP — `0-change_your_home_IP` ✅

**Concept:** `/etc/hosts` is read by the OS before any DNS query. Each line follows the format `IP  hostname`. Modifying it lets you override what any hostname resolves to on this machine.

**What the script does:**
- Makes `localhost` resolve to `127.0.0.2` (instead of the default `127.0.0.1`)
- Makes `facebook.com` resolve to `8.8.8.8`

**How to run:**
```bash
sudo ./0-change_your_home_IP
```

**How to verify:**
```bash
ping -c 1 localhost    # should show 127.0.0.2
ping -c 1 facebook.com # should show 8.8.8.8
```

**Resource used:** *What is the hosts file* — `/etc/hosts` overrides DNS; `sed -i` edits it in-place safely.

---

### 1. Show attached IPs — `1-show_attached_IPs` ✅

**Concept:** `ifconfig` lists all network interfaces. Each active interface has an `inet` line showing its IPv4 address. `grep 'inet '` (with a trailing space) excludes `inet6` lines, and `awk '{print $2}'` extracts the IP — always the second field in `ifconfig` output.

**What the script does:**
- Prints every active IPv4 address on the machine (loopback + all network interfaces)

**How to run:**
```bash
./1-show_attached_IPs
```

**Example output:**
```
10.0.2.15
127.0.0.1
```

**Resource used:** `man ifconfig` — network interface configuration and address display.

---

### 2. Port listening on localhost — `2-port_listening_on_localhost` ✅

**Concept:** `nc` (Netcat) can open a raw TCP socket and listen for incoming connections. Once a client connects, anything typed in either terminal is sent to the other — making it ideal for testing that a port is reachable on `localhost`.

**What the script does:**
- Opens a listening TCP socket on `localhost` port `98`
- Accepts one connection and relays text both ways until closed

**How to test (requires two terminals):**

Terminal 1 — start the listener:
```bash
sudo ./2-port_listening_on_localhost
```

Terminal 2 — connect and send a message:
```bash
telnet localhost 98
```

Anything typed in Terminal 2 appears in Terminal 1. Press `Ctrl+C` to stop the listener.

**Resource used:** *Netcat examples* — `nc -l` puts Netcat into listen mode; `localhost` scopes it to the loopback interface so only local connections are accepted.
