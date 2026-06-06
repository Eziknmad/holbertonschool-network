# What Happens When You Type https://www.google.com in Your Browser and Press Enter?

*Published on Medium / LinkedIn*

---

## Introduction

You type `https://www.google.com` into your browser and press Enter. Within a fraction of a second, Google's homepage appears. It feels instant — but underneath that simplicity, an extraordinary series of events has already unfolded. Your request traveled across networks, passed through security checkpoints, was handled by multiple specialized servers, and returned with a fully rendered page.

This post breaks down every step of that journey, from the moment your finger lifts off the Enter key to the moment the page loads on your screen.

---

## Step 1 — DNS Request: Translating a Name into an Address

Your browser does not know where "www.google.com" lives on the internet. It only understands IP addresses — numerical identifiers like `142.250.80.46`. The **Domain Name System (DNS)** acts as the internet's phonebook, translating human-readable domain names into IP addresses.

When you press Enter, the browser first checks its own cache to see if it already knows the IP address for `www.google.com`. If not, it asks your operating system's DNS resolver. The OS checks its own cache and the `hosts` file. If still not found, the query travels to your **ISP's DNS resolver** (a recursive resolver), which then queries:

1. A **Root Name Server** — the authoritative top of the DNS hierarchy, which returns a referral to the `.com` TLD name servers
2. A **TLD Name Server** (for `.com`) — which returns a referral to Google's authoritative name servers
3. **Google's Authoritative Name Server** — which returns the actual IP address for `www.google.com`

The IP address travels back through the chain and is cached at each level for future lookups. Your browser now has a destination.

---

## Step 2 — TCP/IP: Establishing the Connection

With the IP address in hand, your browser needs to open a reliable communication channel to Google's server. This is done using the **TCP/IP protocol stack**.

**IP (Internet Protocol)** handles routing: it breaks your request into packets and routes each one across networks to the destination IP. Packets may take different paths and arrive out of order.

**TCP (Transmission Control Protocol)** handles reliability: it guarantees that packets arrive, are reassembled in order, and that missing packets are retransmitted.

Before any data is exchanged, TCP performs a **three-way handshake**:

1. **SYN** — Your browser sends a synchronize packet to Google's server, saying "I want to connect"
2. **SYN-ACK** — Google's server acknowledges and sends back its own synchronize signal
3. **ACK** — Your browser confirms, completing the handshake

A reliable connection is now open on **port 443** (the standard port for HTTPS traffic).

---

## Step 3 — Firewall: The Traffic Filter

Before your request reaches Google's servers, and before Google's response reaches you, traffic passes through **firewalls** on both ends.

A firewall is a security system — hardware or software — that monitors incoming and outgoing network traffic and applies rules to allow or block packets. Firewalls operate at different layers:

- **Network-level firewalls** filter by IP address and port number
- **Application-level firewalls** inspect the content of packets more deeply

On your end, your router or OS-level firewall ensures no unauthorized traffic comes in. On Google's end, their firewalls reject requests that don't match expected patterns, block known malicious IP ranges, and help prevent attacks like DDoS (Distributed Denial of Service). Only legitimate traffic that passes all rules is allowed through.

---

## Step 4 — HTTPS/SSL: Encrypting the Connection

Since the URL begins with `https://`, the connection must be **encrypted**. This is handled by **TLS (Transport Layer Security)**, formerly known as SSL. HTTPS is simply HTTP running over TLS.

After the TCP handshake, a **TLS handshake** occurs:

1. Your browser sends a "Client Hello" — listing the TLS versions and cipher suites it supports
2. Google's server responds with a "Server Hello" — selecting the cipher suite and presenting its **SSL certificate**
3. Your browser verifies the certificate against a trusted **Certificate Authority (CA)** — confirming you are actually talking to Google and not an impersonator
4. Both sides derive a **shared session key** using asymmetric cryptography (without ever sending the key over the network)
5. All subsequent communication is encrypted using that session key with **symmetric encryption** (much faster than asymmetric)

From this point on, everything — your request, Google's response, all data — is encrypted in transit and cannot be read by anyone intercepting the traffic.

---

## Step 5 — Load Balancer: Distributing the Request

Google handles billions of requests per day. No single server could handle that volume. When your request arrives at Google's network, it first hits a **load balancer** — a system that distributes incoming traffic across a pool of servers.

The load balancer sits between the public internet and Google's internal server fleet. It evaluates the incoming request and forwards it to an available server using one of several algorithms:

- **Round Robin** — requests are distributed one by one to each server in rotation
- **Least Connections** — requests are sent to the server currently handling the fewest active connections
- **IP Hash** — requests from the same client are consistently routed to the same server

The load balancer also performs **health checks** — regularly pinging each server to confirm it is online. If a server goes down, the load balancer stops sending traffic to it. This eliminates a single point of failure (SPOF) and ensures high availability.

---

## Step 6 — Web Server: Handling the HTTP Request

The request reaches one of Google's **web servers**. The web server (commonly Nginx or Apache, though Google uses its own infrastructure) is responsible for:

1. Receiving the HTTP request
2. Parsing the request headers, method (GET), and path (`/`)
3. Deciding how to respond

For a simple static file (like an image or CSS stylesheet), the web server can respond directly by retrieving the file from disk. For dynamic content like Google's homepage — which is personalized, may show different results, and connects to live data — the web server passes the request to the **application server**.

---

## Step 7 — Application Server: Generating Dynamic Content

The **application server** contains the business logic of the application. It runs the backend code that:

1. Processes your request parameters (search query, user session, location, preferences)
2. Applies application logic (what results are relevant, what ads to show, what language to use)
3. Makes decisions about what data to retrieve

For Google Search, this involves ranking algorithms, personalization systems, and infrastructure that serves billions of queries. For a simpler web app, this might be a Python, Node.js, or Java backend processing a form submission.

The application server does not store long-term data itself. To build a complete response, it queries the **database**.

---

## Step 8 — Database: Retrieving the Data

The **database** is the persistent storage layer. When the application server needs data (search index results, user account information, cached content), it sends a query to the database.

Google's infrastructure uses a combination of:

- **Relational databases** (SQL-based) for structured data like user accounts
- **NoSQL databases** for massive-scale distributed data storage
- **In-memory caches** (like Redis or Memcached) to serve frequently accessed data without hitting the disk

The database returns the requested data to the application server, which uses it to construct the full HTML response.

---

## The Return Journey

The application server sends the assembled HTML back to the web server. The web server wraps it in an HTTP response with status code `200 OK`. The response travels back through the load balancer, out through Google's network, across the internet in TCP/IP packets, through your firewall, back to your browser — all still encrypted via TLS.

Your browser decrypts the response, parses the HTML, requests additional resources (CSS, JavaScript, images) — each triggering a similar process — and renders the final page on your screen.

All of this happens in under 200 milliseconds.

---

## Summary

| Step | Component | What It Does |
|---|---|---|
| 1 | DNS | Translates `www.google.com` to an IP address |
| 2 | TCP/IP | Opens a reliable connection via three-way handshake |
| 3 | Firewall | Filters traffic; blocks unauthorized or malicious requests |
| 4 | HTTPS/SSL | Encrypts the connection via TLS handshake |
| 5 | Load Balancer | Distributes the request across multiple servers |
| 6 | Web Server | Receives and handles the HTTP request |
| 7 | Application Server | Runs business logic; generates dynamic content |
| 8 | Database | Retrieves the data needed to build the response |

---

## Sources

- Mozilla Developer Network — [How the Web Works](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/How_the_Web_works)
- Cloudflare — [What is DNS?](https://www.cloudflare.com/learning/dns/what-is-dns/)
- Cloudflare — [What is TLS/SSL?](https://www.cloudflare.com/learning/ssl/transport-layer-security-tls/)
- IBM — [What is a Load Balancer?](https://www.ibm.com/topics/load-balancing)
- IETF RFC 793 — Transmission Control Protocol
- IETF RFC 8446 — TLS 1.3

---

*Written by Kevin Galarza Arzon | Holberton School Aguadilla*
