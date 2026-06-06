# holbertonschool-network

## Description

This repository contains networking projects completed as part of the Holberton School curriculum. Each directory corresponds to a module covering core networking concepts and practical Bash scripting tasks.

## Modules

### [basics_0](./basics_0)

Covers the foundational networking concepts including the OSI model, network types (LAN/WAN/Internet), MAC and IP addresses, TCP/UDP protocols, ports, and ICMP-based connectivity checks.

| Task | File | Description |
|------|------|-------------|
| 0 | `0-OSI_model` | Multiple-choice answers about the OSI model |
| 1 | `1-types_of_network` | Multiple-choice answers about LAN, WAN, and Internet |
| 2 | `2-MAC_and_IP_address` | Multiple-choice answers about MAC and IP addresses |
| 3 | `3-UDP_and_TCP` | Multiple-choice answers about TCP and UDP protocols |
| 4 | `4-TCP_and_UDP_ports` | Bash script that displays all active listening ports with PID/program |
| 5 | `5-is_the_host_on_the_network` | Bash script that pings an IP address 5 times |

### [basics_1](./basics_1)

Covers localhost, the hosts file, IP address resolution, and practical network tools (`nc`, `ip`, `telnet`, `awk`, `cut`).

| Task | File | Description |
|------|------|-------------|
| 0 | `0-change_your_home_IP` | Bash script that overrides `localhost` → `127.0.0.2` and `facebook.com` → `8.8.8.8` via `/etc/hosts` |
| 1 | `1-show_attached_IPs` | Bash script that displays all active IPv4 addresses using `ip -4 addr show` |
| 2 | `2-port_listening_on_localhost` | Bash script that opens a listening TCP socket on `127.0.0.1` port 98 using `nc` |

### [what_happens_when_your_type_google_com_in_your_browser_and_press_enter](./what_happens_when_your_type_google_com_in_your_browser_and_press_enter)

Explores the full journey of a web request — from pressing Enter to Google's homepage appearing on screen. Covers every layer of the web stack through a published blog post and a request flow diagram.

| Task | File | Description |
|------|------|-------------|
| 0 | `0-blog_post` | URL of a published blog post explaining the full web request flow (DNS, TCP/IP, Firewall, HTTPS/SSL, Load Balancer, Web Server, Application Server, Database) |
| 1 | `1-what_happen_when_diagram` | URL of a diagram illustrating the complete request flow from browser to database |

## Author

Kevin Galarza Arzon — Holberton School Aguadilla
