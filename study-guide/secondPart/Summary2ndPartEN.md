# YYG
## WAS
### HERE

# Network Layer – Exam-Oriented Summary

## Role of the Network Layer
- Encapsulates segments coming from the transport layer into **IP datagrams**
- Performs encapsulation at the sender and decapsulation at the receiver
- **All routers examine the header of every IP datagram passing through them**

---

## Forwarding vs Routing (VERY COMMON IN EXAMS)
- **Forwarding**:  
  - Local decision
  - Determines **which output port** a packet is sent to
- **Routing**:  
  - Global decision
  - Determines **the path** from source to destination
⚠️ Trap: Routing algorithm ≠ forwarding table

---

## Datagram Network vs Virtual Circuit (VC)
### Datagram Network (Internet)
- Connectionless
- Routers **do not maintain state**
- Packets are forwarded using the **destination IP address**
- Flexible, “best-effort” service

### Virtual Circuit (ATM, Frame Relay)
- Connection-oriented (setup & teardown required)
- Routers **maintain connection state**
- Packets carry a **VC number**
- Resources can be pre-allocated (predictable service)

⚠️ Trap: The modern Internet **does not use Virtual Circuits**

---

## IP Datagram Header – Critical Fields
- **TTL**: Decreased by 1 at each router → packet is dropped when it reaches 0
- **Header Length**: Can be variable due to IP options
- **Total Length**: Required for fragmentation
- **Protocol**: Indicates the upper-layer protocol (TCP=6, UDP=17)
- **Checksum**:
  - Covers **only the IP header**
  - **Recomputed at every router**

---

## IP Fragmentation
- If the MTU is smaller, the datagram is fragmented
- **Fragmentation occurs at routers**, **reassembly only at the destination**
- Fields:
  - **Identification**: Identifies fragments of the same datagram
  - **Fragment Offset**: Measured in units of 8 bytes
  - **MF (More Fragments)**: Set to 1 for all fragments except the last

⚠️ Trap: Fragmentation **does not exist in IPv6**

---

## IP Addressing – Basic Concepts
- An IP address belongs to an **interface**, not to a host
- A subnet = interfaces sharing the same subnet part
- Same subnet → **direct communication**
- Different subnet → **default gateway (router)** required

---

## Netmask & AND Operation (LOGIC, NOT MEMORIZATION)
- A host finds its own network by computing:

- If the destination produces the same result:
  - Same subnet → send directly
- Otherwise:
  - Send to the router

---

## CIDR & Longest Prefix Matching
- CIDR: `/x` → number of network bits
- Router:
  - Performs AND between destination IP and **all routing table entries**
  - The **longest matching prefix** is selected

⚠️ Trap: A more specific route always has priority

---

## ARP (Address Resolution Protocol)
- Purpose: **IP → MAC** address resolution
- ARP Request:
  - **Broadcast** (FF:FF:FF:FF:FF:FF)
- ARP Reply:
  - **Unicast**
- ARP messages are **not IP packets**, they are link-layer payloads
- ARP table entries **expire using TTL**

---

## DHCP (VERY COMMON)
### Purpose
- Provides IP address + netmask + default gateway + DNS

### Message Sequence
1. DHCP Discover → broadcast (255.255.255.255)
2. DHCP Offer
3. DHCP Request
4. DHCP ACK

⚠️ Traps:
- Before obtaining an IP, the client source IP = **0.0.0.0**
- DHCP uses **UDP** (ports 67/68)

---

## NAT (Network Address Translation)
- Private IP addresses are not routable on the Internet
- NAT:
  - Modifies **source IP + source port**
  - Destination IP **does not change**
- NAT table:  
  `(internal IP, port) ↔ (public IP, port)`

Advantages:
- IP address conservation
- Increased security

Disadvantages:
- Violates the end-to-end principle

---

## ICMP
- Used for error and control messages
- Examples:
  - Echo request/reply (ping)
  - Destination unreachable
  - TTL expired (used by traceroute)

### Traceroute Logic
- TTL = 1, 2, 3, ...
- Each router sends **ICMP Time Exceeded** when TTL reaches 0
- Terminates with **ICMP Port Unreachable** at the destination

---

## IPv6 – Differences Asked in Exams
- 128-bit address space
- Fixed **40-byte header**
- **No checksum**
- **No fragmentation at routers**
- Transition mechanism: **Tunneling (IPv6 inside IPv4)**



## SLIDE 2

# DNS (Domain Name System) – Exam-Oriented Summary

## What is DNS?

* Translates **domain names** used by humans into IP addresses
* A **distributed** and **hierarchical** system
* An **Application Layer** protocol

⚠️ Trap: DNS is **not a network layer** protocol

---

## Why Not a Centralized DNS?

* Single point of failure
* Traffic would be excessive
* Distant servers → high latency
* Difficult maintenance

➡️ **Does not scale**

---

## Services Provided by DNS

* Hostname → IP address translation
* **Host aliasing**

  * Alias ↔ canonical name
* **Mail server aliasing**
* **Load balancing**

  * One domain → multiple IP addresses

---

## DNS Hierarchy (VERY COMMON IN EXAMS)

1. **Root DNS Server**
2. **TLD DNS Server** (.com, .org, .edu, .tr, …)
3. **Authoritative DNS Server**
4. **Local DNS Server**

⚠️ Trap:

* Local DNS is **not an official part of the hierarchy**
* Provided by ISP / university

---

## Root DNS Server

* There are **13 logical root servers** worldwide
* Contacted when the local DNS cannot resolve a name
* Root server:

  * Responds with “I don’t know, but ask this server”

⚠️ Trap: Root servers **do not return IP addresses**

---

## TLD and Authoritative DNS

### TLD DNS Server

* Responsible for .com, .edu, .org, and country domains
* Indicates which authoritative DNS server is responsible

### Authoritative DNS Server

* Provides the **definitive (authoritative)** answer for a domain
* IP address mappings are stored here

---

## DNS Name Resolution

### Iterative Query (MOST COMMON)

* Local DNS queries servers step by step
* Each server:

  * Replies with “I don’t know, but ask this server”
* **Load is distributed**

### Recursive Query

* The queried server performs the entire resolution
* Causes **high load** on upper-level servers

⚠️ Trap: The Internet mostly uses **iterative queries**

---

## DNS Caching

* Learned mappings are **cached**
* Cache entries expire using **TTL**
* Until TTL expires:

  * Old IP address may be returned even if the IP has changed

⚠️ Trap: DNS operates on a **best-effort** basis

---

## DNS Resource Records (RR) (MEMORIZATION QUESTION)

**Format:**
(name, value, type, TTL)

### Important Types

* **A**

  * name = hostname
  * value = IP address
* **NS**

  * domain → authoritative DNS server
* **CNAME**

  * alias → canonical name
* **MX**

  * domain → mail server

⚠️ Trap:

* CNAME **does not provide an IP address**
* Alias points to another name

---

## DNS Protocol

* Query and reply use the **same message format**
* Usually uses **UDP**
* TCP:

  * Used for zone transfers

⚠️ Trap: DNS **does not always use TCP**

---

## Adding Records to DNS (Logic Question)

1. Register the domain with a registrar
2. Provide authoritative DNS server information
3. **NS and A records** are added to the TLD server
4. On the authoritative server:

   * A record (www)
   * MX record (mail)

---

## DNS Security Issues

### DDoS

* Attacks on root servers (unsuccessful so far)
* Attacks on TLD servers are more dangerous

### Redirect / Poisoning

* Fake DNS replies are sent
* DNS cache is poisoned

### DNS Amplification

* Small query with spoofed source IP
* Large reply sent to the target

---

## Common Exam Traps

* DNS is **distributed + hierarchical**
* DNS is an **application layer** protocol
* Iterative ≠ Recursive
* CNAME ≠ A
* Root servers **do not return IP addresses**
* Cache + TTL → outdated IP may be returned

## SLIDE 3

# Network Analysis Tools – Exam-Oriented Summary

## General Notes

* Tools are available on both **UNIX and Windows** systems
* However:

  * Options may not be the same
  * Outputs may not be exactly identical
* In exams, **only the basic purpose and logic** are asked, not all options

---

## Ping

* Purpose: Test whether a host is **active at the network layer**
* Uses ICMP

  * Echo Request
  * Echo Reply

### Ping Logic

* Source → ICMP Echo Request
* Destination → ICMP Echo Reply
* If a reply is received: **the host is reachable**

⚠️ Trap:

* If ping fails, **the exact reason cannot be determined**

  * There may be a path problem
  * The return path may be different (asymmetric routing)
  * A firewall may be blocking ICMP

### RTT (Round Trip Time)

* Time between sending the Echo Request and receiving the Echo Reply
* Used as a measure of “distance” between hosts

---

## Traceroute / Tracert

* Purpose: Show the **possible path** from source to destination
* Lists the routers along the path

### Operating Principle (VERY COMMON)

1. A packet with TTL = 1 is sent
2. The first router sets TTL to 0 and returns **ICMP Time Exceeded**
3. TTL is increased to 2, 3, ...
4. Each router reveals itself via ICMP

⚠️ Trap:

* A router may reply using **a different interface IP address**

---

## ARP

* Purpose: **View and modify the ARP cache**
* Shows IP ↔ MAC address mappings

### Basic Operations

* Display cache
* Remove entries from the cache
* Add static IP–MAC mappings

⚠️ Trap:

* Dynamic ARP entries are **not permanent**

---

## Route / Netstat -r

* Purpose: **View and modify the routing table**
* Available on both Windows and UNIX (syntax differs)

### Information Shown in the Routing Table

* Network destination
* Netmask
* Gateway
* Interface

⚠️ Trap:

* Default route: `0.0.0.0 / 0.0.0.0`

---

## Ipconfig (Windows)

* Displays IP stack information

### Important Uses

* IP address, netmask, gateway
* DNS servers
* DHCP status
* View / clear local DNS cache

⚠️ Trap:

* `ipconfig` is **Windows-only**

---

## Ip (UNIX)

* Displays / modifies IP configuration on UNIX systems

### Basic Uses

* Interface information
* Routing table

⚠️ Trap:

* The `ip` command is the modern replacement for `ifconfig` and `route`

---

## Nslookup

* Purpose: **Query DNS servers**

### Operating Modes

* Interactive
* Non-interactive

### Commonly Asked Record Types

* A
* PTR
* CNAME
* MX

⚠️ Trap:

* Nslookup is used for **DNS debugging**

---

## Tcpdump / Windump

* Text-based **packet analyzer**
* Displays summary information of packets

### Basic Features

* Interface selection
* Filtering support
* Capture can be written to a file

⚠️ Trap:

* If `-n` is not used, **DNS lookup** is performed

---

## Tcpdump Filtering Logic (VERY COMMON)

* Protocol-based: arp, ip, tcp, udp, icmp
* Host-based: src, dst, host
* Port-based filtering
* Boolean operators: and, or, not

---

## Wireshark

* Graphical **packet sniffer & analyzer**
* Based on libpcap / WinPcap

### Filter Types

* Capture filter → tcpdump syntax
* Display filter → different syntax

⚠️ Trap:

* Capture filter ≠ Display filter

---

## Common Exam Topics

* Ping → ICMP
* Traceroute → TTL + ICMP Time Exceeded
* ARP → IP–MAC mapping
* Default route logic
* Viewing DNS cache
* Tcpdump filters
* Difference between Wireshark capture and display filters


## SLIDE 4

# Transport Layer (TCP / UDP) – Exam-Oriented Summary

## Role of the Transport Layer

* Provides **logical communication** between **application processes** running on different hosts
* Transport protocols run on **end systems** (not on routers)
* Sender:

  * Breaks application messages into **segments**
* Receiver:

  * Reassembles segments and delivers them to the application

⚠️ Trap:

* Network layer → **host-to-host** communication
* Transport layer → **process-to-process** communication

---

## Multiplexing / Demultiplexing (VERY COMMON)

* **Multiplexing (sender)**:

  * Adds a **transport header** to data coming from multiple applications
* **Demultiplexing (receiver)**:

  * Delivers incoming segments to the correct application

### UDP Demultiplexing

* Uses only the **destination port**
* Same port → same socket

### TCP Demultiplexing

* Performed using a **4-tuple**:

  * Source IP
  * Source Port
  * Destination IP
  * Destination Port
* Same server port (e.g. 80) → **different sockets** for different clients

⚠️ Trap:

* TCP ≠ UDP demultiplexing

---

## Well-Known Ports

* Port range: **0 – 1024**
* Reserved by ICANN
* Example:

  * TCP 80 → HTTP
* Client ports:

  * **Chosen randomly**

---

## UDP (User Datagram Protocol)

* **Connectionless**
* **Best-effort** service
* Packets may:

  * Be lost
  * Arrive out of order

### UDP Characteristics

* No handshake → low latency
* No connection state
* Small header
* **No congestion control**

### Where Is UDP Used?

* Streaming (loss-tolerant applications)
* DNS
* SNMP

⚠️ Trap:

* UDP is not reliable
* If reliability is needed, it must be implemented at the **application layer**

---

## UDP Segment Structure

* Source port
* Destination port
* Length
* Checksum

### UDP Checksum

* Detects bit errors
* Uses one’s complement sum

⚠️ Trap:

* Checksum **detects** errors, it does not correct them

---

## Reliable Data Transfer (RDT)

* Goal: Provide reliable communication over an **unreliable channel**
* Mechanisms used:

  * ACKs
  * Sequence numbers
  * Timeouts
  * Retransmissions

### Pipelined Protocols

#### Go-Back-N (GBN)

* Receiver sends only **cumulative ACKs**
* Timeout → **all unacknowledged packets** are retransmitted

#### Selective Repeat (SR)

* Receiver sends **individual ACKs** for each packet
* Timeout → only the missing packet is retransmitted

⚠️ Trap:

* The difference between GBN and SR is very commonly asked

---

## TCP (Transmission Control Protocol)

* **Connection-oriented**
* **Reliable, in-order byte stream**
* Full duplex
* Point-to-point

### What TCP Provides

* Reliable data transfer
* Flow control
* Congestion control

⚠️ TCP Does NOT Provide:

* Delay guarantees
* Bandwidth guarantees

---

## TCP Segment Structure (MEMORIZATION QUESTION)

* Sequence number
* Acknowledgement number
* Receive window (rwnd)
* Flags: SYN, ACK, FIN, RST
* Checksum

⚠️ Trap:

* Sequence numbers count **bytes**, not segments

---

## TCP Reliable Data Transfer

* Uses cumulative ACKs
* Uses a single retransmission timer (for the oldest unacknowledged segment)

### Retransmission Triggers

* Timeout
* **3 duplicate ACKs → Fast Retransmit**

---

## RTT and Timeout Calculation

* SampleRTT: measured RTT
* EstimatedRTT:

  * Exponential weighted moving average

EstimatedRTT = (1 − α) · EstimatedRTT + α · SampleRTT

* TimeoutInterval = EstimatedRTT + 4 · DevRTT

⚠️ Trap:

* Timeout too short → unnecessary retransmissions
* Timeout too long → slow reaction

---

## TCP Flow Control

* Goal: Prevent receiver buffer overflow
* Receiver:

  * Advertises **rwnd (receive window)**
* Sender:

  * In-flight data ≤ rwnd

⚠️ Trap:

* Flow control ≠ congestion control

---

## TCP Connection Management

### 3-Way Handshake (VERY COMMON)

1. Client → SYN
2. Server → SYN + ACK
3. Client → ACK

### Connection Termination

* Uses FIN flags
* Each side closes the connection independently

---

## Congestion Control

* Definition:

  * Sending more data than the network can handle

### Symptoms

* Packet loss
* Long delays

⚠️ Trap:

* Congestion control ≠ flow control

---

## TCP Congestion Control (AIMD)

* **Additive Increase**:

  * cwnd increases linearly every RTT
* **Multiplicative Decrease**:

  * cwnd is halved when loss is detected

### Slow Start

* Initially cwnd = 1 MSS
* Doubles every RTT

### TCP Reno vs Tahoe

* Reno:

  * 3 duplicate ACKs → cwnd / 2
* Tahoe:

  * In all cases cwnd = 1

---

## TCP Fairness

* If K TCP connections share the same bottleneck:

  * Average throughput ≈ R / K

⚠️ Trap:

* UDP does not perform congestion control → breaks fairness
* Parallel TCP connections break fairness

---

## Common Exam Traps

* TCP = reliable, UDP = best-effort
* TCP is a byte-stream protocol (no message boundaries)
* 4-tuple TCP demultiplexing
* Difference between GBN and SR
* Flow control ≠ congestion control
* Fast retransmit = 3 duplicate ACKs


## SLIDE 5
# Application Layer – Exam-Oriented Summary

## Purpose of the Application Layer

* Provides communication between **application processes** running on **different hosts**
* Operates only on **end systems**
* **Routers do not run application-layer protocols**

⚠️ Trap:
Application layer ≠ Network core
Applications run on **hosts**, routing is done by **routers**

---

## Network Application Architectures (VERY COMMON)

### Client–Server Architecture

**Server:**

* Always-on
* **Permanent IP address**
* Uses data centers for scalability

**Client:**

* Communicates with the server
* May be intermittently connected
* Can have a dynamic IP address
* **Clients do not communicate directly with each other**

⚠️ Trap:

* No client–client communication

---

### P2P (Peer-to-Peer) Architecture

* No always-on server
* End systems communicate **directly** with each other
* **Self-scalability**:

  * New peer = new capacity
* Peers:

  * Frequently disconnect
  * Have changing IP addresses

⚠️ Disadvantages:

* Difficult management
* Complex security

⚠️ Trap:

* P2P applications still contain **client and server processes**

---

## Process Concept

* **Process**: A program running within a host
* Same host:

  * Inter-process communication via the OS
* Different hosts:

  * Communication via **message exchange**

**Client process:**

* Initiates communication

**Server process:**

* Waits for incoming connections

---

## What Does an Application Layer Protocol Define?

* Message types (request / response)
* Message format (syntax)
* Message meaning (semantics)
* Rules for **when and how** messages are sent

### Open vs Proprietary Protocols

**Open protocol:**

* Defined in RFCs
* Interoperable
* Examples: HTTP, SMTP

**Proprietary protocol:**

* Closed
* Example: Skype

---

## Application Requirements from the Transport Layer (MEMORIZATION QUESTION)

### Data Integrity

* File transfer, web → **no loss tolerated**
* Audio/video → **loss tolerant**

### Timing (Delay)

* VoIP, online games → **low delay required**

### Throughput

* Video → minimum throughput required
* Elastic applications → use whatever throughput is available

### Security

* Encryption
* Authentication
* Integrity

---

## TCP vs UDP – From the Application Perspective

| Feature            | TCP            | UDP            |
| ------------------ | -------------- | -------------- |
| Reliability        | Yes            | No             |
| Congestion Control | Yes            | No             |
| Delay              | Higher         | Lower          |
| Usage              | Web, FTP, Mail | DNS, Streaming |

⚠️ Trap:

* TCP is not secure by itself → security is provided by SSL/TLS

---

## HTTP (HyperText Transfer Protocol)

* **Application layer protocol**
* **Client–Server** model
* Uses TCP (port 80)
* **Stateless**

⚠️ Trap:

* HTTP servers **do not store client state**

---

## Non-Persistent vs Persistent HTTP (VERY COMMON)

### Non-Persistent HTTP

* 1 TCP connection → 1 object
* **2 RTT** per object
* Poor performance

### Persistent HTTP

* Single TCP connection
* Multiple objects
* Fewer RTTs

⚠️ Trap:

* HTTP/1.1 → persistent by default

---

## HTTP Request Message

* ASCII format
* Components:

  * Request line
  * Header lines
  * (Optional) body

**Methods:**

* GET
* POST
* HEAD
* PUT
* DELETE

---

## HTTP Response Message

* Status line
* Header lines
* Data (HTML, image, etc.)

### Important Status Codes (MEMORIZATION)

* 200 OK
* 301 Moved Permanently
* 400 Bad Request
* 404 Not Found
* 505 HTTP Version Not Supported

---

## Cookies (State Management Mechanism)

Used because HTTP is stateless

**4 components:**

1. HTTP response header
2. HTTP request header
3. Cookie file in the browser
4. Backend database on the server

**Purposes:**

* Authorization
* Shopping cart
* User tracking

⚠️ Trap:

* Cookies raise **privacy concerns**

---

## Web Cache (Proxy Server)

* Client → cache
* If object is in cache:

  * No need to contact origin server
* Purpose:

  * Reduce delay
  * Reduce access link load

⚠️ Trap:

* Cache acts as both **client and server**

---

## Conditional GET

* Checks whether cached content is up to date
* Header:

  * `If-Modified-Since`
* Response:

  * 304 Not Modified

⚠️ Advantage:

* Object is not retransmitted

---

## FTP (File Transfer Protocol)

* Client–Server
* Uses TCP
* Server port: **21**

### FTP Connections (VERY COMMON)

* **Control connection**:

  * Port 21
  * Commands
* **Data connection**:

  * Separate TCP connection for each transfer
  * Port 20

⚠️ Trap:

* FTP is **stateful**

---

## Electronic Mail – Components

1. User Agent
2. Mail Server
3. SMTP

### SMTP

* TCP port 25
* Push protocol
* ASCII text
* Persistent connection

⚠️ Trap:

* SMTP is used **only to send mail**
* It is not used to read mail

---

## Mail Access Protocols

### POP3

* Download & delete
* Stateless
* Mail not stored on the server

### IMAP

* Mail remains on the server
* Folder support
* Stateful

### HTTP Mail

* Gmail, Yahoo
* Accessed via browser

⚠️ Trap:

* Difference between POP3 and IMAP is frequently asked

---

## P2P File Distribution – BitTorrent

* File is divided into **chunks**
* Tracker provides peer list
* Rarest-first chunk selection
* **Tit-for-tat** upload strategy

⚠️ Trap:

* Peers both download and upload data

---

## Distributed Hash Table (DHT)

* (Key, value) pairs
* Key is hashed into an integer
* Key is assigned to the **closest successor peer**

⚠️ Trap:

* Circular DHT
* Lookup complexity:

  * O(N) → O(log N) using shortcuts

---

## Common Exam Topics

* Client–Server vs P2P
* Stateless vs Stateful
* Non-persistent vs persistent HTTP
* Advantages of web caching
* FTP control vs data connections
* SMTP vs POP3 vs IMAP
* BitTorrent tit-for-tat
* DHT successor logic

## SLIDE 6

# Multimedia Networking – Exam-Oriented Summary

## What Is Multimedia Networking?

* Studies the transmission of **audio**, **video**, and **real-time communication** applications over networks
* Unlike classical data applications, the following are much more critical:

  * **Delay**
  * **Jitter** (delay variation)
  * **Packet loss**

⚠️ Trap:
Multimedia applications do **not** require high throughput, but **timely delivery**

---

## Types of Multimedia (VERY COMMON)

### Streaming Stored Audio / Video

* Content is pre-recorded
* The client starts playback before the entire file is downloaded
* Examples: YouTube, Netflix

### Live Streaming

* Content is generated live
* Low delay tolerance
* Example: Live sports broadcasts

### Conversational Voice / Video

* Interactive communication
* **Very low delay tolerance**
* Examples: VoIP, video calls

---

## Audio – Basic Concepts

* Analog audio is converted to digital using **sampling**
* Telephone: 8000 samples/sec
* CD: 44100 samples/sec
* Quantization → **quantization error**

⚠️ Trap:
Sampling rate ↑ → quality ↑ → bitrate ↑

---

## Video – Basic Concepts

* Video = a **sequence of frames** displayed at a constant rate
* Example: 24 frames/sec
* Digital image = array of pixels

### Video Coding

* Goal: **reduce bitrate**
* Types of redundancy:

  * **Spatial coding** (within the same frame)
  * **Temporal coding** (between frames)

---

## CBR vs VBR (VERY COMMON)

### CBR (Constant Bit Rate)

* Fixed encoding rate
* More predictable for the network

### VBR (Variable Bit Rate)

* Bitrate varies depending on scene complexity
* Better quality, harder network management

---

## Challenges of Streaming Stored Video

* Requirement for continuous playout
* Network delay is variable (jitter)
* Solutions:

  * Client-side buffer
  * Playout delay

⚠️ Trap:
Increasing buffer size increases delay

---

## Streaming over UDP

* Data is sent at the encoding rate
* Advantage: low delay
* Disadvantages:

  * Packet loss
  * No congestion control

---

## Streaming over HTTP/TCP

* Video transferred using HTTP GET
* TCP provides congestion control and retransmissions
* Result:

  * More stable delivery
  * Higher delay

---

## DASH (Dynamic Adaptive Streaming over HTTP) (VERY COMMON)

### Server

* Video is divided into chunks
* Stored at multiple bitrates
* Provides a manifest file

### Client

* Measures available bandwidth
* Requests chunks at an appropriate bitrate
* Bitrate can change over time

⚠️ Advantage:
Adaptive quality and TCP compatibility

---

## Content Distribution Network (CDN)

* Content is stored on geographically distributed servers
* Goals:

  * Reduce delay
  * Distribute traffic load

⚠️ Trap:
A single server does not scale

---

## Voice over IP (VoIP)

* End-to-end delay:

  * < 150 ms → good
  * > 400 ms → poor
* Packet loss of 1–10% can be tolerated

### Types of Loss

* Network loss (due to congestion)
* Delay loss (packet arrives too late)

---

## RTP (Real-Time Protocol)

* Carries real-time audio and video
* Runs on top of UDP
* Provides:

  * Payload type
  * Sequence number
  * Timestamp

⚠️ Trap:
RTP does **not** provide QoS guarantees

---

## RTP Header – Critical Fields

* Payload Type → codec information
* Sequence Number → packet loss detection
* Timestamp → synchronization
* SSRC → stream source identifier

---

## SIP (Session Initiation Protocol)

* Call setup and management
* User location
* HTTP-like syntax
* Default port: 5060

⚠️ Trap:
SIP = signaling
RTP = media transport

---

## Network Support for Multimedia

### Best Effort

* No QoS guarantees
* Simple

### Differentiated Services

* Traffic classes
* Packet marking

### Per-Connection QoS

* Flow-based guarantees
* Complex, rarely used

---

## Common Exam Traps

* Streaming ≠ downloading
* UDP → low delay, high loss
* TCP → reliable but higher delay
* DASH → adaptive bitrate
* SIP ≠ RTP
* RTP ≠ QoS
* Why CDNs are needed
* Delay ≠ jitter


# YYGWASHERE
## YYGWASHERE
### YYGWASHERE
