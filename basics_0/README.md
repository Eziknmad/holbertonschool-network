# Networking basics #0

## Description

This project covers the fundamentals of networking, including the OSI model, types of networks, MAC and IP addresses, TCP/UDP protocols, ports, and network diagnostics using ICMP/ping.

## Resources

- OSI model
- LAN / WAN / Internet
- MAC address
- IP address (IPv4 and IPv6)
- Localhost and subnets
- TCP and UDP
- TCP/UDP ports list
- ICMP / ping

## Learning Objectives

- What the OSI model is and how its 7 layers are organized
- What a LAN is (typical usage and geographical size)
- What a WAN is (typical usage and geographical size)
- What the Internet is
- What an IP address is and its two types (public/private)
- What localhost and subnets are
- Why IPv6 was created
- The difference between TCP and UDP
- What a port is, and the port numbers for SSH (22), HTTP (80), and HTTPS (443)
- How to use ping/ICMP to check network connectivity

## Requirements

- All Bash scripts are interpreted on Ubuntu 22.04
- All files end with a new line
- All Bash scripts must be executable
- Bash scripts must pass `shellcheck` without errors
- First line of all Bash scripts: `#!/usr/bin/env bash`
- Second line of all Bash scripts: a comment explaining what the script does

## Tasks

### 0. OSI model (`0-OSI_model`)

Answer file for multiple-choice questions about the OSI model:
1. What is the OSI model? → **2** (a conceptual model that characterizes communication functions without regard to internal structure)
2. How is the OSI model organized? → **2** (from the lowest to the highest level)

### 1. Types of network (`1-types_of_network`)

Answer file for multiple-choice questions about network types:
1. What type of network is a local computer connected to? → **3** (LAN)
2. What connects offices in different buildings a few streets apart? → **2** (WAN)
3. What network does a smartphone use when browsing (no WiFi)? → **1** (Internet)

### 2. MAC and IP address (`2-MAC_and_IP_address`)

Answer file for multiple-choice questions about MAC and IP addresses:
1. What is a MAC address? → **2** (the unique identifier of a network interface)
2. What is an IP address? → **1** (like a postal address for devices on a network)

### 3. UDP and TCP (`3-UDP_and_TCP`)

Answer file for multiple-choice questions about UDP and TCP:
1. TCP box statement → **1** (transfers data slowly but reliably)
2. UDP box statement → **2** (transfers data fast but may lose data)
3. TCP worker statement → **1** (Have you received boxes x, y, z? — acknowledgment)

### 4. TCP and UDP ports (`4-TCP_and_UDP_ports`)

Bash script that displays all active listening ports, including the PID and name of the program for each socket.

```bash
sudo ./4-TCP_and_UDP_ports
```

### 5. Is the host on the network (`5-is_the_host_on_the_network`)

Bash script that pings an IP address passed as an argument exactly 5 times.

```bash
./5-is_the_host_on_the_network 8.8.8.8
```

If no argument is provided, displays:
```
Usage: 5-is_the_host_on_the_network {IP_ADDRESS}
```

## Author

Holberton School — Networking Basics #0
