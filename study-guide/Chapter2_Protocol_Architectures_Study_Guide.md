# CHAPTER 2: PROTOCOL ARCHITECTURES
## Exam-Oriented Study Guide

**Based on:** Professor's lecture slides (Protocol architectures slides 1-45)  
**Exam Weight:** CRITICAL (⭐⭐⭐) - Approximately 30-40% of exam questions  
**Study Priority:** HIGHEST - Master this chapter completely

---

## 📋 CHAPTER OVERVIEW

This is the **MOST IMPORTANT** chapter for your exam. Protocol architectures, especially the OSI model and TCP/IP, appear in 30-40% of all exam questions.

**Main Topics:**
1. Protocol Fundamentals (Syntax, Semantics, Timing)
2. Layered Architecture Principles
3. OSI 7-Layer Reference Model (Each layer in detail)
4. Services: Connection-Oriented vs Connectionless
5. PDU Creation and Encapsulation
6. Terminal vs Relay Systems
7. Protocol vs Service Distinction

---

# PART 1: PROTOCOL FUNDAMENTALS

## 🎯 SLIDES 1-4: What is a Protocol?

### CCITT/ITU-T Definition

**Communication:** Transfer of information according to pre-established conventions (requires agreement)

**Protocol:** Formal definition of procedures adopted to guarantee communication between two or more objects on the same hierarchical level

### The Three Essential Elements of a Protocol (CRITICAL!)

**Every protocol consists of exactly THREE components:**

#### 1. SEMANTIC RULES
**Definition:** Field meaning  
**Examples:**
- Commands
- Answers
- Control information
- What actions to take

**Think:** The "meaning" of each field

#### 2. SYNTACTIC RULES
**Definition:** Message formats  
**Examples:**
- Field order
- Field sizes
- Data structure
- Header organization

**Think:** The "structure" of messages

#### 3. TIMING
**Definition:** When and how fast  
**Examples:**
- Transmission speed
- Timeout values
- Synchronization
- Response times

**Think:** The "when" and "how fast"

### 📊 Exam Pattern (HIGHEST FREQUENCY!)

**Most Common Question:**
"The three fundamental elements that constitute a protocol are: ___"

**Correct Answers (various forms):**
- A) **Semantics, Syntax, Timing** ✓
- B) **Format, Meaning, Timing** ✓ (alternative wording)
- C) **Syntactic rules, Semantic rules, Timing** ✓

**WRONG Answers to Avoid:**
- "Services, Functions, Timing" ❌
- "Algorithms, Services, Timing" ❌
- "Algorithms, Formats, Entities" ❌

### 🔑 Must Memorize

**Mnemonic: "SST"**
- **S**emantics (meaning)
- **S**yntax (format)
- **T**iming (when/speed)

### ⚠️ Common Exam Trap

Students often confuse "protocol elements" with "architecture concepts"
- Protocol = Semantics, Syntax, Timing
- Architecture = Layers, services, interfaces (different concept!)

---

## 🎯 SLIDES 4: Protocol Architecture Fundamentals

### Why Layered Architectures?

**Four Main Reasons:**

1. **Separation among functions**
   - Each layer handles specific tasks
   - Clear responsibility boundaries

2. **Simple design**
   - Complex problem divided into manageable pieces
   - Each layer can be designed independently

3. **Simple management**
   - Easier to maintain and update
   - Can replace one layer without affecting others

4. **Simple standardization**
   - Each layer can be standardized separately
   - Interoperability easier to achieve

### Network Architecture Definition

**A network architecture defines:**
- The communication process
- The relation among objects
- The functionalities to support communication
- The structure of the functions

**Key Principle:** Protocol hierarchies define a network architecture

---

# PART 2: OSI REFERENCE MODEL

## 🎯 SLIDES 5-7: OSI Model Introduction

### Historical Context

**OSI (Open System Interconnection):**
- Defined as **ISO IS 7498**
- Later as **CCITT/ITU-T X.200**
- **First layered model** in networking
- **Universal principles** accepted worldwide

**Important Note:** Not all protocol architectures conform to OSI, but its principles are universally accepted

### The 7 OSI Layers (Top to Bottom)

| Layer | Number | Name | Mnemonic |
|-------|--------|------|----------|
| Application | 7 | Application | **A**ll |
| Presentation | 6 | Presentation | **P**eople |
| Session | 5 | Session | **S**eem |
| Transport | 4 | Transport | **T**o |
| Network | 3 | Network | **N**eed |
| Data Link | 2 | Data Link | **D**ata |
| Physical | 1 | Physical | **P**rocessing |

### Comparison with Other Architectures

The slides show OSI compared to:
- **DECNET** (Digital Equipment Corporation)
- **ARPA** (Internet Protocol Suite)
- **SNA** (IBM Systems Network Architecture)
- **B-ISDN** (ATM-based architecture)

**Exam Focus:** Primarily on OSI and Internet (TCP/IP) models

---

## 🎯 SLIDES 8: OSI vs Internet Protocol Suite

### Layer Mapping (CRITICAL for Exams!)

| OSI Model | Internet Protocol Suite | Protocols |
|-----------|------------------------|-----------|
| **Application (7)** | **Application** | NFS, Telnet, FTP, SMTP, SNMP |
| **Presentation (6)** | ↑ (included) | XDR, RPC |
| **Session (5)** | ↑ (included) | - |
| **Transport (4)** | **Transport** | TCP, UDP |
| **Network (3)** | **Internet** | IP, ICMP, ARP, RARP, Routing protocols |
| **Data Link (2)** | **Unspecified** | (Implementation dependent) |
| **Physical (1)** | **Unspecified** | (Implementation dependent) |

### Key Differences

**OSI:** 7 distinct layers  
**Internet:** 4-5 layers (combines upper 3 OSI layers into Application layer)

**📊 Exam Pattern:**
"In TCP/IP, which OSI layers are combined into the Application layer?"  
**Answer:** Application, Presentation, and Session (Layers 5, 6, 7)

---

# PART 3: LAYERED ARCHITECTURE CONCEPTS

## 🎯 SLIDES 11-15: Systems, Layers, and Entities

### Network Components

#### 1. System
**Definition:** Node in the network  
**Examples:** Terminals, switches, routers, hosts  
**Composed of:** Subsystems

#### 2. Subsystem (Layer)
**Definition:** Implements specific functions  
**Contains:** Entities  
**Structure:** Higher layers use services from lower layers

#### 3. Entity
**Definition:** Active element in a subsystem  
**Functions:**
- Runs the functions of the layer
- Interacts within the same layer
- Implements the protocol

### Layering Principle (FUNDAMENTAL!)

**Each layer (N):**
- **Provides** services to the higher layer (N+1)
- **Uses** services from the lower layer (N-1)
- **Plus** its own functionalities
- **Enhances/integrates** the service offered by lower layers

**Three Roles:**
- **Service provider:** Layer N
- **Service user:** Layer N+1
- **SAP (Service Access Point):** Interface between layers

### 📊 Exam Pattern (VERY COMMON!)

**Question:** "In the OSI model, the relationship between the Nth layer and the N+1 layer is:"

**CORRECT Answer:** "Layer N provides services for Layer N+1" ✓

**WRONG Answers:**
- "Layer N+1 adds a header to Layer N" ❌ (describes encapsulation, not relationship)
- "Layer N utilizes services from Layer N+1" ❌ (backwards!)
- "N layer has no effect on N+1 layer" ❌ (completely wrong)

---

## 🎯 SLIDES 16-17: Services - Connection-Oriented vs Connectionless

### Two Types of Services (CRITICAL!)

#### 1. Connection-Oriented (CO) Service

**Three Phases:**
1. **Connection establishment** (preliminary agreement)
2. **Data transfer**
3. **Connection release**

**Characteristics:**
- Agreement between network and endpoints before data transfer
- Reliable (usually)
- Ordered delivery
- State maintained

**Examples:**
- TCP (Transport layer)
- Virtual circuits
- Telephone calls

#### 2. Connectionless (CL) Service

**Operation:**
- Data sent without any preliminary agreement
- Each data unit treated independently
- No connection setup/teardown

**Characteristics:**
- Best effort
- No guarantees
- Simpler
- Less overhead

**Examples:**
- UDP (Transport layer)
- IP (Network layer)
- Postal mail system

### 📊 Exam Pattern

**Question:** "IP protocol provides ___ service"  
**Answer:** **Connectionless datagram service** ✓

**Question:** "TCP provides ___ service"  
**Answer:** **Connection-oriented reliable service** ✓

### ⚠️ Common Exam Trap

**TRAP:** "IP is connection-oriented"  
**CORRECT:** IP is connectionless (TCP provides connection-oriented service)

---

## 🎯 SLIDES 18-20: SAP (Service Access Point)

### SAP Definition

**SAP (Service Access Point):**
- Interface through which N-service is offered to (N+1)-entities
- Each (N)-SAP associated with at most one (N)-entity
- Like a "door" or "socket" between layers

**Analogy:** Think of SAP as a numbered door between floors of a building

### Protocol Communication

**Info exchange among (N)-entities occurs via an (N)-protocol**

**Structure:**
```
(N+1) Entity ←→ (N+1) Entity
     ↓               ↓
   (N) SAP       (N) SAP
     ↓               ↓
(N) Entity ←→ (N) Entity
   (via N-protocol)
```

**Key Point:** Entities at same layer communicate logically, but physically data goes down and up the stack

---

# PART 4: PDU CREATION AND ENCAPSULATION

## 🎯 SLIDES 26-33: Protocol Data Units

### Key Terms (MUST MEMORIZE!)

#### 1. SDU (Service Data Unit)
**Definition:** Data at layer N (user data from upper layer)  
**Think:** The "payload" or "data" being carried

#### 2. PCI (Protocol Control Information)
**Definition:** Control information added by layer N  
**Also called:** Header (sometimes trailer too)  
**Think:** The "envelope" with addressing and control info

#### 3. PDU (Protocol Data Unit)
**Definition:** PCI + SDU  
**Formula:** **PDU = PCI + SDU** (MEMORIZE THIS!)  
**Think:** The complete "package" at this layer

### Encapsulation Process (CRITICAL!)

**Going DOWN the layers (Transmission):**

```
Layer 7 (Application):    [Data]
                          ↓ Add Layer 7 header
Layer 6 (Presentation):   [L6-PCI][Data]
                          ↓ Add Layer 6 header
Layer 5 (Session):        [L5-PCI][L6-PCI][Data]
                          ↓ Add Layer 5 header
Layer 4 (Transport):      [L4-PCI][L5-PCI][L6-PCI][Data]
                          ↓ Add Layer 4 header
Layer 3 (Network):        [L3-PCI][L4-PCI][L5-PCI][L6-PCI][Data]
                          ↓ Add Layer 2 header
Layer 2 (Data Link):      [L2-PCI][L3-PCI]...[Data][L2-Trailer]
                          ↓ Convert to bits
Layer 1 (Physical):       Bits or symbols
```

**Key Principle:** Each layer treats upper layer PDU as a "black box" (closed envelope) and adds its own PCI

**Going UP the layers (Reception):**
- Reverse process
- Each layer removes its own header
- Passes SDU to upper layer

### 📊 Exam Pattern

**Question:** "PDU consists of ___"  
**Answer:** PCI + SDU ✓

**Question:** "What does each layer add to data?"  
**Answer:** Header (PCI - Protocol Control Information) ✓

---

## 🎯 SLIDE 33: Segmentation and Concatenation

### Operations on Data Units

#### Segmentation
**Definition:** Breaking one SDU into multiple PDUs

**Two Ways:**
1. Many (N)-PDUs from one (N)-SDU
2. Many (N-1)-SDUs from one (N)-PDU

**Why needed:**
- MTU (Maximum Transmission Unit) limitations
- Network constraints
- Efficiency

**Disadvantages:**
- More overhead (each segment needs header)
- Need reassembly at receiver
- **One piece lost → whole data lost**

#### Concatenation
**Definition:** Combining multiple SDUs into one PDU

**Opposite of segmentation**

### 📊 Exam Pattern

**Question:** "Segmentation is harmful because ___"  
**Correct answers:**
- More overhead ✓
- Need to reassembly ✓
- One piece lost → whole data lost ✓

---

# PART 5: OSI LAYER DESCRIPTIONS

## 🎯 SLIDES 36-45: The Seven OSI Layers in Detail

### LAYER 1: PHYSICAL LAYER

**Functions:**
- Provides mechanical, physical, functional, and procedural means
- Activates, maintains, and disables physical connections
- Permits transfer of binary digits between data link entities

**Data Unit:** **Bits or symbols**

**Defines:**
- Transmission codes
- Connectors
- Voltage levels
- Pin assignments
- Cable specifications

**Examples:**
- Ethernet cables
- Fiber optic specifications
- RS-232
- V.24

**Devices operating at Layer 1:**
- Hub (passive)
- Repeater

### 📊 Exam Pattern
**Question:** "Physical layer data unit is ___"  
**Answer:** **Bits** ✓

---

### LAYER 2: DATA LINK LAYER

**Functions:**
- Provides functional and procedural means to transfer data among network entities
- Handles malfunctions and failures at physical level

**Main Functions:**
1. **Transmission error detection and correction**
2. **Flow control**
3. **Data unit delimitation** (framing)

**Data Unit:** **Frame**

**Two Sublayers:**
- **MAC (Media Access Control):** Addresses who can transmit
- **LLC (Logical Link Control):** Provides interface to network layer

**Examples:**
- Ethernet (IEEE 802.3)
- PPP (Point-to-Point Protocol)
- HDLC
- Wi-Fi (IEEE 802.11 MAC)

**Devices operating at Layer 2:**
- Switch
- Bridge

### 📊 Exam Pattern
**Question:** "Data link layer is responsible for ___"  
**Answers:**
- Error detection/correction ✓
- Flow control ✓
- Framing ✓

**Question:** "Data link layer data unit is ___"  
**Answer:** **Frame** ✓

### ⚠️ Critical Exam Point
**Switch operates at Layer 2** (NOT Layer 3!)

---

### LAYER 3: NETWORK LAYER

**Functions:**
- Provides means to setup, maintain, and close connections among transport layer entities

**Main Functions:**
1. **Routing** (path determination)
2. **Flow control and congestion control**
3. **Pricing** (billing)

**Data Unit:** **Packet**

**Key Responsibility:** Getting data from source to destination across multiple networks

**Examples:**
- IP (Internet Protocol)
- ICMP
- Routing protocols (OSPF, RIP, BGP)

**Devices operating at Layer 3:**
- Router

### 📊 Exam Pattern
**Question:** "Routing is a function of ___ layer"  
**Answer:** **Network layer (Layer 3)** ✓

**Question:** "Network layer data unit is ___"  
**Answer:** **Packet** ✓

**Question:** "Which device works at network layer?"  
**Answer:** **Router** ✓

---

### LAYER 4: TRANSPORT LAYER

**Key Characteristic:** **First (lower) layer with end-to-end meaning**

**Functions:**
- Compensates possible lack of QoS in network layer connections

**Main Functions:**
1. **Error control**
2. **Control of sequence** (ordering)
3. **Flow control**

**Additional Functions:**
- Multiplexing and subdivision of connections
- Fragmentation of messages into packets
- Reassembly

**Data Unit:** **Segment**

**Two Main Protocols:**

**TCP (Transmission Control Protocol):**
- Connection-oriented
- Reliable
- Ordered delivery
- Flow control
- Error control

**UDP (User Datagram Protocol):**
- Connectionless
- Unreliable (best effort)
- No ordering
- Lower overhead

### 📊 Exam Pattern
**Question:** "Transport layer is responsible for ___"  
**Answers:**
- End-to-end reliable data transfer ✓
- Error control ✓
- Sequence control ✓

**Question:** "First layer with end-to-end meaning?"  
**Answer:** **Transport layer (Layer 4)** ✓

**Question:** "Transport layer data unit is ___"  
**Answer:** **Segment** ✓

---

### LAYER 5: SESSION LAYER

**Functions:**
- Provides one session connection to presentation layer entities
- Organizes communication among presentation layer entities
- Provides structure and synchronizes data exchange
- Permits suspending, recovering, and terminating data transfer
- Masks interruptions at service level

**Key Services:**
- Dialog control (half-duplex or full-duplex)
- Synchronization (checkpoints)
- Session management

**Data Unit:** **Data**

**Examples:**
- Session establishment/termination
- Checkpointing for long transfers

**Note:** Often combined with other layers in practical implementations

### 📊 Exam Pattern
**Frequency:** LOW (few questions)  
**Question:** "Session layer provides ___"  
**Answer:** Synchronization, dialog control, session management

---

### LAYER 6: PRESENTATION LAYER

**Functions:**
- Solves compatibility issues regarding data formats
- Solves issues of data syntax translation
- May provide data encryption services

**Key Services:**
- Data format conversion
- Character encoding (ASCII, EBCDIC, Unicode)
- Compression
- Encryption

**Data Unit:** **Data**

**Examples:**
- XDR (External Data Representation)
- SSL/TLS encryption
- JPEG, MPEG encoding

**Note:** Often combined with application layer in practice

### 📊 Exam Pattern
**Frequency:** LOW (few questions)  
**Question:** "Presentation layer handles ___"  
**Answer:** Data format translation, encryption

---

### LAYER 7: APPLICATION LAYER

**Functions:**
- Provides application processes with means to access OSI environment
- User-visible services

**Examples of Services:**
- **File transfer** (FTP)
- **Virtual terminal** (Telnet)
- **E-mail** (SMTP, POP3)
- **Web browsing** (HTTP)
- **Network management** (SNMP)

**Data Unit:** **Data**

**Protocols at this layer:**
- HTTP, HTTPS
- FTP, SFTP
- SMTP, POP3, IMAP
- DNS
- SNMP
- Telnet, SSH

### 📊 Exam Pattern (HIGH FREQUENCY!)
**Question:** "Which protocol operates at application layer?"  
**Answers:** HTTP, FTP, SMTP, DNS, Telnet, SNMP (all correct)

**Question:** "FTP is used for ___"  
**Answer:** **File transfer** ✓

**Question:** "SMTP is used for ___"  
**Answer:** **Sending email** ✓

---

# PART 6: TERMINAL VS RELAY SYSTEMS

## 🎯 SLIDE 37: System Types

### Terminal System (End System)

**Characteristics:**
- Contains **ALL 7 layers**
- Source or destination of data
- Hosts the application

**Examples:**
- Desktop computer
- Laptop
- Smartphone
- Server
- Any device running applications

**Layer Stack:**
```
[7] Application
[6] Presentation
[5] Session
[4] Transport
[3] Network
[2] Data Link
[1] Physical
```

### Relay System (Intermediate System)

**Characteristics:**
- Contains **only lower layers** (typically 1-3)
- Forwards data between networks
- Does NOT host applications

**Examples:**
- **Router:** Layers 1-3
- **Switch:** Layers 1-2
- **Bridge:** Layers 1-2
- **Repeater:** Layer 1 only

**Layer Stack (Router):**
```
[3] Network
[2] Data Link
[1] Physical
```

### Communication Path

```
TERMINAL A          RELAY           TERMINAL B
[7] App                            [7] App
[6] Pres                           [6] Pres
[5] Sess                           [5] Sess
[4] Trans                          [4] Trans
[3] Net         [3] Net            [3] Net
[2] DL          [2] DL             [2] DL
[1] Phy         [1] Phy            [1] Phy
  ↓───────────────↓─────────────────↓
     Transmission Media
```

**Key Points:**
- Only lower layers in relay systems
- Upper layers (4-7) only in terminal systems
- Data goes down at source, up at destination
- Relay systems process up to their highest layer only

### 📊 Exam Pattern

**Question:** "Router operates at which layers?"  
**Answer:** **Layers 1, 2, and 3** ✓

**Question:** "Terminal system contains ___ layers"  
**Answer:** **All 7 layers** ✓

**Question:** "Relay system is used for ___"  
**Answer:** **Forwarding data** ✓

---

# SUMMARY: EXAM-CRITICAL POINTS FOR CHAPTER 2

## 🎯 MUST MEMORIZE (HIGHEST PRIORITY!)

### The Three Protocol Elements
**Answer for ANY exam question about protocol fundamentals:**
1. **Semantics** (meaning)
2. **Syntax** (format)  
3. **Timing** (when/speed)

### OSI Layer Functions (One-line Summary)

| Layer | Name | Function | Data Unit |
|-------|------|----------|-----------|
| **7** | **Application** | User services | Data |
| **6** | **Presentation** | Data format translation | Data |
| **5** | **Session** | Dialog control, synchronization | Data |
| **4** | **Transport** | End-to-end reliable transfer | **Segment** |
| **3** | **Network** | Routing, path determination | **Packet** |
| **2** | **Data Link** | Error detection, framing, flow control | **Frame** |
| **1** | **Physical** | Bit transmission | **Bits** |

### Layer Relationship
**CRITICAL:** Layer N provides services to Layer N+1

### PDU Formula
**PDU = PCI + SDU** (Must know!)

### Data Unit Names by Layer
- Physical: **Bits**
- Data Link: **Frames**
- Network: **Packets**
- Transport: **Segments**
- Upper layers: **Data**

### Device-to-Layer Mapping
- **Hub/Repeater:** Layer 1 (Physical)
- **Switch/Bridge:** Layer 2 (Data Link)
- **Router:** Layer 3 (Network)
- **Gateway:** All layers (up to 7)

### Service Types
- **Connection-Oriented (CO):** Setup → Transfer → Release (TCP, Virtual Circuit)
- **Connectionless (CL):** No setup, independent data units (UDP, IP, Datagram)

### OSI vs TCP/IP Mapping
- **OSI 7+6+5** = **TCP/IP Application**
- **OSI 4** = **TCP/IP Transport**
- **OSI 3** = **TCP/IP Internet**
- **OSI 2+1** = **TCP/IP Network Access**

---

## ⚠️ COMMON EXAM TRAPS

### Trap 1: Protocol Elements
**WRONG:** "Services, Functions, Timing"  
**RIGHT:** "Semantics, Syntax, Timing" ✓

### Trap 2: Layer Relationship
**WRONG:** "Layer N+1 provides services to Layer N"  
**RIGHT:** "Layer N provides services to Layer N+1" ✓

### Trap 3: Device Layers
**WRONG:** "Switch operates at Network Layer"  
**RIGHT:** "Switch operates at Data Link Layer (Layer 2)" ✓

### Trap 4: IP Service Type
**WRONG:** "IP provides connection-oriented service"  
**RIGHT:** "IP provides connectionless service" ✓

### Trap 5: End-to-End Layer
**WRONG:** "Network layer provides end-to-end service"  
**RIGHT:** "Transport layer is first layer with end-to-end meaning" ✓

### Trap 6: Data Unit Names
**WRONG:** Calling everything "packet"  
**RIGHT:** Bits (L1), Frames (L2), Packets (L3), Segments (L4)

### Trap 7: Routing Layer
**WRONG:** "Routing is done at Transport layer"  
**RIGHT:** "Routing is a Network layer (Layer 3) function" ✓

### Trap 8: Encapsulation
**WRONG:** "Remove header before sending to lower layer"  
**RIGHT:** "Add header, pass entire PDU to lower layer" ✓

---

## 📊 EXAM WEIGHT DISTRIBUTION

### CRITICAL (Study exhaustively - 70% of Chapter 2 questions):
- ✅ Three protocol elements (Semantics, Syntax, Timing)
- ✅ Layer N serves Layer N+1 relationship
- ✅ OSI layer functions (all 7 layers)
- ✅ Data unit names (bits, frames, packets, segments)
- ✅ Device-layer mapping (hub, switch, router)
- ✅ PDU = PCI + SDU formula
- ✅ Connection-oriented vs Connectionless
- ✅ Transport layer = end-to-end

### HIGH (Study thoroughly - 20%):
- Layer-specific functions (what each layer does)
- Encapsulation process
- Terminal vs Relay systems
- OSI vs TCP/IP mapping
- Protocol vs Service distinction

### MEDIUM (Understand well - 10%):
- SAP (Service Access Point)
- Segmentation and concatenation
- Why layered architectures
- Network architecture definition
- Upper layers (Session, Presentation)

---

## 🎓 STUDY STRATEGY FOR CHAPTER 2

### Day 1: Core Concepts
- Memorize the 3 protocol elements
- Learn Layer N → N+1 relationship
- Understand layering principle

### Day 2: OSI Layers 1-4
- Master Physical, Data Link, Network, Transport
- Memorize functions and data units
- Practice device-layer matching

### Day 3: OSI Layers 5-7 + Services
- Learn Application, Presentation, Session
- Connection-oriented vs Connectionless
- Protocol examples (HTTP, FTP, TCP, UDP, IP)

### Day 4: PDU and Integration
- PDU = PCI + SDU formula
- Encapsulation process
- Terminal vs Relay systems
- Review all traps

### Day 5: Practice Questions
- Test yourself on all concepts
- Focus on common trap scenarios
- Speed drills on device-layer mapping

---

## 📝 QUICK REFERENCE FLASHCARDS

### Q: Three protocol elements?
**A:** Semantics, Syntax, Timing

### Q: Layer N relationship with N+1?
**A:** Layer N provides services to Layer N+1

### Q: Physical layer data unit?
**A:** Bits

### Q: Data link layer data unit?
**A:** Frames

### Q: Network layer data unit?
**A:** Packets

### Q: Transport layer data unit?
**A:** Segments

### Q: Hub operates at which layer?
**A:** Layer 1 (Physical)

### Q: Switch operates at which layer?
**A:** Layer 2 (Data Link)

### Q: Router operates at which layer?
**A:** Layer 3 (Network)

### Q: Routing is function of which layer?
**A:** Network layer (Layer 3)

### Q: First layer with end-to-end meaning?
**A:** Transport layer (Layer 4)

### Q: PDU formula?
**A:** PDU = PCI + SDU

### Q: IP provides what type of service?
**A:** Connectionless datagram service

### Q: TCP provides what type of service?
**A:** Connection-oriented reliable service

### Q: Data link layer main functions?
**A:** Error detection/correction, Flow control, Framing

### Q: How many layers in terminal system?
**A:** All 7 layers

### Q: How many layers in router (relay system)?
**A:** 3 layers (Physical, Data Link, Network)

---

**END OF CHAPTER 2: PROTOCOL ARCHITECTURES**

**Status:** ✅ Complete - Ready for exam preparation  
**Importance:** ⭐⭐⭐ HIGHEST PRIORITY - 30-40% of exam  
**Next Chapter:** Window Protocols (ARQ Techniques)

