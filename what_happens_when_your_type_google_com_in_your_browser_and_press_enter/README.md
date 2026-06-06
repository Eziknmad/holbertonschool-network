# What Happens When You Type google.com in Your Browser and Press Enter

## Description

This project explores the full journey of a web request — from the moment you press Enter to the moment Google's homepage appears on your screen. It is a classic software engineering interview question that tests a candidate's understanding of the entire web stack.

## Requirements

- Blog post published on Medium or LinkedIn
- Blog post written in English
- README.md at the root of the project folder
- A diagram illustrating the full request flow

## Tasks

### Task 0 — What happens when... (`0-blog_post`)

Write a blog post explaining what happens when you type `https://www.google.com` in your browser and press Enter.

The post must cover:

| Topic | Description |
|---|---|
| DNS request | How the browser resolves `www.google.com` to an IP address |
| TCP/IP | How the connection is established between client and server |
| Firewall | How traffic is filtered and secured at network boundaries |
| HTTPS/SSL | How the connection is encrypted via TLS handshake |
| Load-balancer | How Google distributes the request across multiple servers |
| Web server | How the server receives and handles the HTTP request |
| Application server | How dynamic content is generated |
| Database | How data is retrieved to build the response |

**File:** `0-blog_post` — contains the URL of the published blog post.

---

### Task 1 — Everything's better with a pretty diagram (`1-what_happen_when_diagram`)

Add a schema/diagram to illustrate the full request flow.

The diagram must show:
- DNS resolution
- Request hitting the server IP on the appropriate port
- Traffic is encrypted
- Traffic goes through a firewall
- Request is distributed via a load balancer
- Web server answers the request by serving a web page
- Application server generates the web page
- Application server requests data from the database

**File:** `1-what_happen_when_diagram` — contains the URL of the uploaded diagram image.

## Repository

- GitHub repository: `holbertonschool-network`
- Directory: `what_happens_when_your_type_google_com_in_your_browser_and_press_enter`
