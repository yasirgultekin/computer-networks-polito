# CHAPTER 1: NETWORK FUNDAMENTALS
## Exam-Oriented Study Guide

**Based on:** Professor's lecture slides (Slides 1-170)  
**Exam Weight:** Medium (⭐⭐) - Approximately 10-15% of exam questions  
**Study Priority:** Foundation concepts - essential for understanding later chapters

---

## 📋 CHAPTER OVERVIEW

This chapter covers the fundamental building blocks of computer networks. While not the highest-weighted chapter in exams, these concepts form the foundation for everything else.

**Main Topics:**
1. TLC Networks: Services and Functions
2. Network Topologies
3. TLC Services and Models (Client-Server, P2P)
4. Transmission Techniques
5. Sharing Techniques (Multiplexing)
6. Switching Techniques (Circuit vs Packet)
7. Signalling Techniques
8. Management Techniques
9. Quality of Service (QoS)

---

# PART 1: TLC NETWORKS - SERVICES AND FUNCTIONS

## 🎯 SLIDE 18-39: Basic Definitions and Network Functions

### Core Concepts

#### ITU-T Definitions (Memorize!)

**Communication:**
- Information transfer according to pre-established rules
- Requires agreement between parties

**Telecommunication:**
- Transmission and reception of signals representing:
  - Signs, text, images, sounds, information of any nature
- Via: cables, radio, optical, or electromagnetic media

**Telecommunication Service:**
- Offered by public or private provider to customers
- Satisfies specific telecommunication needs

**Functions in a Telecommunication Network:**
- Operations executed internally in the network
- Provide services to users
- **Hidden from end users**

### The Four Main Network Functions

#### 1. SIGNALLING
**Definition:** Exchange of control information for setup/release of calls

**Two Types:**
- **User Signalling:** Between user and network access node
  - Example: Dialing a phone number
  - Example: Lifting handset (signals willingness to call)
  
- **Network Signalling:** Among network nodes
  - Example: Nodes coordinating to establish path
  - Internal to network

**Key Points:**
- Actions order is important
- Timing is critical
- Includes: dialed digits, billing number, call-related info

**Historical Note:** 
- Early telephony: Voice-based signalling, manual switching
- Later: Strowger introduced direct selection via electromechanical switching

#### 2. SWITCHING
**Definition:** Interconnecting functional units, transmission channels, and circuits for the time needed to transfer signals

**Purpose:**
- Network identifies resources to connect two users
- In telephone networks: Circuit is established
- This is "Circuit Switching"

**Process:**
- Temporarily connects input to output
- Resources allocated on demand

#### 3. TRANSMISSION
**Definition:** Signal transfer from one point to one or several points

**When it occurs:**
- AFTER circuit is established via switching
- Two users exchange information
- Example: Voice conversation after phone call connected

#### 4. MANAGEMENT
**Definition:** All activities to keep network operational and efficient

**Functions:**
- Connecting new users
- Adding channels or nodes
- Upgrading or substituting devices (technological evolution)
- Reconfiguration after faults
- Performance monitoring
- Device control

### 📊 Exam Patterns

**Common Question Types:**
1. "What is signalling?" → Exchange of control information for call setup/release
2. "ITU-T defines telecommunication as ___" → Transmission/reception of signals via cables, radio, optical media
3. "Difference between service and function?" → Service = what users see; Function = internal operations

### ⚠️ Common Mistakes

1. **Confusing user and network signalling**
   - User signalling: User ↔ Network
   - Network signalling: Network node ↔ Network node

2. **Confusing services with functions**
   - Services: External (what provider offers customers)
   - Functions: Internal (how network implements services)

3. **Thinking transmission happens before switching**
   - WRONG order: Transmission → Switching
   - RIGHT order: Switching → Transmission

### 🔑 Must Memorize

- **Four main functions:** Signalling, Switching, Transmission, Management
- **ITU-T:** International Telecommunication Union - Telecommunication Sector (formerly CCITT until 1994)
- **Signalling implies routing**
- **Switching implies routing**

---

# PART 2: NETWORK TOPOLOGIES

## 🎯 SLIDES 40-61: Topology Fundamentals and Definitions

### Core Definitions (Critical for Exams!)

#### 1. Transmission Medium
**Definition:** Physical medium able to transport signals  
**Examples:**
- Coaxial cable
- Fiber optic
- Twisted pair
- Air (for wireless)

#### 2. Channel
**Definition:** 
- A single transmission medium, OR
- A chain of transmission media

**Example:** Fiber + amplifier + fiber = one channel

#### 3. Bandwidth (⚠️ TWO DIFFERENT MEANINGS!)

**CRITICAL DISTINCTION - Often Tested!**

**Meaning 1: Signal Theory (Physics)**
- **Definition:** Spectral width of a signal/channel
- **Unit:** Hz, MHz, GHz
- **Example:** "This cable has 100 MHz bandwidth"

**Meaning 2: Network Jargon (What we usually mean)**
- **Definition:** Amount of data (bits) per time unit
- **Proper name:** Bit Rate or Channel Speed
- **Unit:** bit/s, Mbps, Gbps
- **Example:** "My internet has 100 Mbps bandwidth"

**📊 Exam Pattern:** "Bandwidth in network jargon means ___"  
**Answer:** Bit rate / Amount of data per time unit (NOT spectral width!)

#### 4. Capacity
**Definition:** Maximum transmission speed of a medium (bit/s)

**Depends on:**
- Transmitter (TX) technology
- Receiver (RX) technology
- Medium quality

**Upper bound:** Limited by medium's physical bandwidth (in Hz)

#### 5. Channel Capacity
**Definition:** Capacity of the most constrained medium (bottleneck) among media composing the channel

**Example:**
- Chain: 100 Mbps → 10 Mbps → 100 Mbps
- Channel capacity = 10 Mbps (the bottleneck!)

#### 6. Offered Traffic
**Definition:** Amount of data per time unit that a source tries to transmit  
**Unit:** bit/s

#### 7. Throughput
**Definition:** Amount of offered traffic that network successfully delivers to destination  
**Unit:** bit/s

#### **Critical Constraints (Must Memorize!):**
```
Throughput ≤ Channel Capacity
Throughput ≤ Offered Traffic
```

**Example Scenarios:**

**Scenario 1:**
- Offered traffic = 10 Mbps
- Channel capacity = 100 Mbps
- **Throughput = 10 Mbps** (limited by offered traffic)

**Scenario 2:**
- Offered traffic = 100 Mbps
- Channel capacity = 10 Mbps
- **Throughput = 10 Mbps** (limited by channel capacity - bottleneck!)

### Network Definition

**Network:** A set of nodes and segments that offer connection among two or more points to make telecommunication possible

**Components:**
- **Node:** Point where switching occurs
- **Segment:** Either a transmission medium or a channel

**Graph Representation:** G = (V, A)
- **V:** Set of vertices (nodes - circles)
- **A:** Set of arcs/edges (segments - lines)
- **N = |V|:** Number of nodes
- **C = |A|:** Number of channels

---

## 🎯 SLIDES 45-47: Types of Channels

### 1. Point-to-Point Channel

**Characteristics:**
- Only 2 nodes connected to channel endpoints
- Channel used by both nodes (often equally)
- Exclusive use by two nodes
- No contention
- Simple protocols

**Examples:**
- Direct link between two routers
- Dedicated leased line
- Fiber connection between offices

**Diagram:**
```
Node A ←──────────→ Node B
      Point-to-Point
```

### 2. Multipoint Channel

**Characteristics:**
- One **master** and several **slaves**
- Asymmetric relationship
- Master controls access
- Slaves wait for permission

**Directions:**
- **Downstream:** Master → Slaves
- **Upstream:** Slaves → Master

**Examples:**
- Polling systems
- Some satellite systems
- Industrial control networks

**Diagram:**
```
        Master
          ↓↑
     ↙    ↓↑    ↘
Slave1  Slave2  Slave3
```

### 3. Broadcast Channel

**Characteristics:**
- Single channel shared by ALL nodes
- Information sent by one node received by ALL others
- Data must contain destination address
- Receivers filter by address
- **Logically point-to-point** (due to addressing)

**Real-World Analogy:** Classroom lecture
- Professor speaks (one sender)
- All students hear (all receive)
- But only YOU pay attention when YOUR name is called

**Examples:**
- Classic Ethernet
- WiFi
- Radio broadcasting

**Diagram:**
```
    Node A
      ↓
  ────┼─────  Broadcast Bus
  ↑   ↑    ↑
Node1 Node2 Node3
(All receive, filter by address)
```

### 📊 Exam Pattern

**Question:** "In a broadcast channel, data should contain ___"  
**Answer:** Destination address

**Question:** "Which channel type is used in classic Ethernet?"  
**Answer:** Broadcast channel

---

## 🎯 SLIDES 48-58: Network Topologies

### Mathematical Foundation

**Topology as Graph:** G = (V, A)
- **N = |V|:** Number of nodes
- **C = |A|:** Number of channels

**Edges can be:**
- **Directed:** Arrows (unidirectional channels)
- **Non-directed:** Lines (bidirectional channels)

---

### 1. FULLY MESHED TOPOLOGY

**Formula:** C = N(N-1)/2

**Description:** Every node directly connects to every other node

**Advantages:**
- ✅ Highly fault tolerant (many paths)
- ✅ Optimal routing (only one hop between any pair)
- ✅ Obvious minimum-distance routing choice

**Disadvantages:**
- ❌ Too many channels needed
- ❌ Cost grows as N²
- ❌ Impractical for large N

**Usage:**
- Only when N is small
- Example: Core nodes in national telephone network (N < 10)

**Calculation Example:**
```
N = 5 nodes
C = 5(5-1)/2 = 5×4/2 = 10 channels
```

**📊 Exam Pattern:**  
"5 nodes in fully meshed topology need ___ channels"  
**Answer:** 10

---

### 2. TREE TOPOLOGY

**Formula:** C = N - 1

**Description:** Hierarchical structure with minimum channels

**Advantages:**
- ✅ Smallest possible number of channels for connected topology
- ✅ Lowest cost
- ✅ Simple hierarchy

**Disadvantages:**
- ❌ Vulnerable to faults (one link failure disconnects subtrees)
- ❌ No routing alternatives
- ❌ Only ONE path between any node pair

**Usage:**
- Cost-sensitive applications
- Hierarchical organizations

**Calculation Example:**
```
N = 5 nodes
C = 5 - 1 = 4 channels
```

---

### 3. STAR TOPOLOGY (Two Types!)

#### A. Active Star (Switch)

**Formula:** C = N (star center not counted as node)

**Characteristics:**
- Star center actively processes frames
- Forwards based on destination address
- **Device:** Switch
- **OSI Layer:** Layer 2 (Data Link) ← **Critical for exams!**

**Behavior:**
- Receives frame from one node
- Reads destination MAC address
- Forwards ONLY to destination node
- **Result:** Reduces collisions, increases privacy

**Usage:**
- Modern LANs (most common today!)
- Data centers

#### B. Passive Star (Hub)

**Formula:** C = 1 (logically one broadcast channel, but N physical wires)

**Characteristics:**
- Star center passively propagates signals
- Broadcasts to ALL nodes
- **Device:** Hub
- **OSI Layer:** Layer 1 (Physical) ← **Critical for exams!**

**Behavior:**
- Receives signal from one node
- Regenerates and broadcasts to ALL other nodes
- **Result:** Shared collision domain (like broadcast bus)

**Usage:**
- Early LANs (obsolete now)
- Some distribution networks (optical splitters)

**Advantages (Both Types):**
- ✅ Low number of channels (vs mesh)
- ✅ Easy to add nodes
- ✅ Centralized management
- ✅ Easy troubleshooting

**Disadvantages (Both Types):**
- ❌ Single point of failure (if star center fails, entire network fails)

### 📊 Exam Pattern (CRITICAL!)

**Most Common Questions:**
1. "Hub works at which layer?" → **Layer 1 (Physical)**
2. "Switch works at which layer?" → **Layer 2 (Data Link)**
3. "In LANs, switches are used in ___ topology" → **Star (active star)**

### ⚠️ CRITICAL Exam Trap!

**WRONG:** "Switch works at Network Layer"  
**CORRECT:** Switch works at **Data Link Layer (Layer 2)**

**Remember:**
- Hub = Layer 1 (Physical) = Passive star = Broadcast
- Switch = Layer 2 (Data Link) = Active star = Selective forwarding
- Router = Layer 3 (Network) = Different topic!

---

### 4. RING TOPOLOGY

**Two Variants:**

#### Unidirectional Ring
**Formula:** C = N (or N/2 if counting pairs)
- Data flows in ONE direction only
- Each node receives from one neighbor, sends to next

#### Bidirectional Ring
**Formula:** C = N (for each direction, so 2N total links)
- Data can flow in BOTH directions
- Provides fault tolerance

**Advantages:**
- ✅ Two alternative paths between each node pair
- ✅ Fault tolerance (bidirectional variant)
  - Single link failure doesn't disconnect network
  - Ring "heals" by using other direction
- ✅ No collisions (with token passing)
- ✅ Fair access (deterministic)

**Disadvantages:**
- ❌ More complex than bus or star
- ❌ Delay increases with N
- ❌ Node failure can affect network (unless bypassed)

**Usage:**
- LANs: Token Ring (obsolete), FDDI
- MANs: SONET/SDH rings (still used!)
- **Bidirectional ring = simplest topology providing alternative paths**

**📊 Exam Pattern:**  
"Ring topology provides ___ alternative paths"  
**Answer:** Two (one in each direction)

---

### 5. BUS TOPOLOGY

**Two Variants:**

#### Active Bus
**Formula:** C = N - 1 (special case of tree)
- Nodes actively process signals
- Point-to-point connections in linear sequence

#### Passive Bus
**Formula:** C = 1 (broadcast channel)
- Single shared medium
- All transmissions broadcast to all nodes
- **Classic Ethernet topology** (10BASE2, 10BASE5)

**Advantages:**
- ✅ Shortest total cable length
- ✅ Simple to implement
- ✅ Easy to extend (tap into bus)
- ✅ Low cost

**Disadvantages:**
- ❌ Limited scalability
- ❌ Single point of failure (bus break disconnects segments)
- ❌ Collisions (shared medium)
- ❌ Performance degrades with more nodes
- ❌ Difficult troubleshooting

**Usage:**
- Early Ethernet: 10BASE2 (Thinnet), 10BASE5 (Thicknet)
- Modern: Rare (replaced by star topology)

---

### 6. MESHED TOPOLOGY

**Formula:** N - 1 < C < N(N-1)/2

**Description:**
- Between tree (minimum) and fully meshed (maximum)
- Not a regular topology
- **Most common in practice!**

**Advantages:**
- ✅ Flexible cost vs fault tolerance tradeoff
- ✅ Good fault tolerance (multiple paths)
- ✅ Load balancing (alternative paths)

**Disadvantages:**
- ❌ Complex routing (many alternative paths)
- ❌ Complex management

**Usage:**
- **Internet backbone**
- **Telephone networks**
- **Enterprise WANs**
- Most common because: best balance of cost vs reliability

**📊 Exam Pattern:**  
"Most commonly used topology in practice?"  
**Answer:** Meshed (partial mesh)

---

### Topology Comparison Table (Must Study!)

| Topology | Formula | Advantages | Disadvantages | Usage |
|----------|---------|------------|---------------|-------|
| **Fully Meshed** | C = N(N-1)/2 | Fault tolerant, optimal routing | Too many channels | Small N only |
| **Tree** | C = N-1 | Minimum channels, lowest cost | Vulnerable to faults, no alternatives | Cost-sensitive |
| **Active Star** | C = N | Low channels, easy management | Single point of failure | Modern LANs (switch) |
| **Passive Star** | C = 1 | Low cost, broadcast | Single point of failure | Early LANs (hub) |
| **Ring** | C = N | Two paths, fault tolerant | Complex, delay with N | SONET/SDH |
| **Bus** | C = N-1 or 1 | Shortest cable, simple | Limited scalability, collisions | Early Ethernet |
| **Meshed** | N-1 < C < N(N-1)/2 | Balanced cost/reliability | Complex routing | Internet, most common |

---

## 🎯 SLIDES 59-61: Physical vs Logical Topology

### Core Concept

**Physical Topology:**
- Actual layout of cables and devices
- Takes into account transmission media constraints
- How network LOOKS physically

**Logical Topology:**
- How data flows between nodes
- Logical interconnection
- How network BEHAVES logically

### Key Insight: They Can Differ!

**Example 1: Hub-based Ethernet**
- **Physical:** Star (all cables radiate from hub)
- **Logical:** Bus (hub broadcasts to all nodes)

**Example 2: Switch-based Ethernet**
- **Physical:** Star (all cables connect to switch)
- **Logical:** Point-to-point (switch forwards to specific destination)

**Example 3: Token Ring**
- **Physical:** Star (nodes connect to MAU device)
- **Logical:** Ring (token passes in circular fashion)

### 📊 Exam Pattern

**Question:** "Distinguish between physical and logical topology"  
**Answer:** Physical = cable layout/physical connections; Logical = data flow/communication pattern

---

# PART 3: TLC SERVICES

## 🎯 SLIDES 68-85: Service Taxonomy and Application Models

### Service Taxonomy

#### 1. Bearer Service
**Definition:** Permits transmission of information between network interfaces

**Characteristics:**
- Gives subscriber capacity to transmit signals
- Between certain access points (user-network interfaces)

**Example:** Point-to-point direct circuit

#### 2. Teleservices
**Definition:** Provide full capacity for communications via terminal and network functions

**Examples:**
- Phone calls
- Telefax

**Classification:**
- Base services
- Supplementary services

---

### Application Models

#### 1. CLIENT-SERVER MODEL

**Two Clearly Different Roles:**

**Client:**
- Starts interaction ("talks first")
- Asks for service (e.g., web page, email transfer)
- Activated when user requires service
- De-activated after service provided

**Server:**
- Provides requested service (send web page, store emails)
- Idle while waiting for clients
- Activated when device is switched on
- Always available

**Characteristics:**
- Most Internet applications follow this model
- Information usually stored in server (not always)

**Request-Reply Pattern:**
```
Client  →  Request  →  Server
Client  ←  Reply    ←  Server
```

**Examples:**
- Web browsing (client: browser, server: web server)
- Email (client: mail client, server: mail server)
- File transfer (client: FTP client, server: FTP server)

#### 2. PEER-TO-PEER (P2P) MODEL

**Characteristics:**
- More recently introduced in Internet
- All applications are **peers** (equal)
- Information distributed and shared among all peers
- Mainly used for interaction among large groups

**Examples:**
- File sharing networks
- Somewhat similar: Phone calls, fax (both parties equal)

### 📊 Exam Pattern

**Question:** "In client-server model, who talks first?"  
**Answer:** Client (initiates interaction)

**Question:** "Most Internet applications follow which model?"  
**Answer:** Client-server model

---

# PART 4: TRANSMISSION TECHNIQUES

## 🎯 SLIDES 86-99: Analog vs Digital, Serial vs Parallel

### 1. Analog vs Digital Transmission

#### Analog Transmission

**Definition:** Information transferred via signal that is:
- Continuous
- Limited
- Assuming infinite possible values

**Characteristics:**
- Information represented as continuous variation of electrical/optical parameter
- Signal can take any value within a range

#### Digital Transmission

**Definition:** Information transferred via signal that is:
- Not continuous
- Limited
- Assuming finite set of possible values

**Key Insight:** **Signals are physically continuous (analog)!**

**Difference is in the RECEIVER:**
- Receiver makes decision process
- Tries to rebuild discrete information
- **Clock synchronization is critical**

### From Analog to Digital (ADC Process)

**Two Steps:**

**1. Sampling Process**
- Take samples of analog signal at regular intervals
- **Lossless if sampling at frequency ≥ 2B** (where B = signal bandwidth)
- This is the Nyquist theorem

**2. Quantization Process**
- Assign digital value to each sample
- **Lossy** (quantization error)
- Error can be controlled by selecting number of levels

**Result:** Digital signal (sequence of bits)

**Example:** 0011 – 0011 – 0100 – 0100 – 0100 – 0100 – 0010 - 0010

---

### 2. Serial vs Parallel Transmission

#### Parallel Transmission

**Characteristics:**
- Information transferred in parallel over communication bus
- Multiple wires (e.g., 8 wires for 8 bits = 1 byte)
- Clock signals sent together with data
- Aligns receiver clock to transmitter clock

**Advantages:**
- Faster transmission
- Simultaneous bit transfer

**Disadvantages:**
- More expensive (more wires)
- Short distances only
- Clock skew issues

#### Serial Transmission

**Characteristics:**
- Information sent bit by bit on single channel
- Synchronization mechanisms between transmitter and receiver
- **More common in networks**

**Advantages:**
- Fewer wires needed
- Longer distances possible
- Lower cost

**Disadvantages:**
- Slower than parallel
- Requires synchronization

---

### 3. Asynchronous vs Synchronous Transmission

#### Asynchronous Transmission

**Characteristics:**
- Every byte (or packet) transmitted separately
- Reception clock synchronized for each data unit
- Compensates for clock skew

**Frame Structure:**
- **Start Bit (S):** Signals beginning of character
- **Data:** 5 to 8 bits
- **Parity Bit (P):** Error detection
- **Stop Bits:** 1, 1.5, or 2 bits
- **Line Idle** between characters

**Use Case:**
- Low-speed communication
- Sporadic data transmission
- Example: Old serial ports, RS-232

#### Synchronous Transmission

**Characteristics:**
- Data structured in frames
- Transmitter and receiver clocks continuously synchronized
- Correct bit detection even at high bit rates

**Advantages:**
- Reduced synchronization overhead
- Higher efficiency
- Better for continuous streams

**Reception Modes:**
- **Continuous reception:** On point-to-point channels (easier to keep clock synchronized)
- **Burst mode:** On broadcast/multipoint channels (receiver must adapt clock to different transmitters)

**Use Case:**
- High-speed networks
- Most modern communications
- Example: Ethernet, WiFi

### 📊 Exam Pattern

**Question:** "In digital transmission, what makes the difference?"  
**Answer:** The receiver (decision process)

**Question:** "Which is more common in networks: serial or parallel?"  
**Answer:** Serial transmission

---

# PART 5: SHARING TECHNIQUES

## 🎯 SLIDES 100-115: Multiplexing and Multiple Access

### Core Concepts

**Sharing of Resources:**
- **Channel sharing:** Multiplexing / Multiple access
- **Node sharing:** Switching techniques

### Multiplexing vs Multiple Access

**Multiplexing:**
- All flows access channel from single point
- **Single transmitter scenario**
- Centralized problem
- Examples: Radio from antenna, output link in router

**Multiple Access:**
- Flows access channel from different access points
- **Many transmitters active**
- Distributed problem
- **More complex task**
- Examples: LANs, mobile phones in cellular network

---

### Channel Sharing Techniques (Four Dimensions)

**1. Frequency (FDM - FDMA)**
**2. Time (TDM - TDMA)**
**3. Code (CDM - CDMA)**
**4. Space**

---

### 1. FREQUENCY DIVISION MULTIPLEXING (FDM)

**Principle:** Each flow transmitted using different frequency bands

**Requirements:**
- **Guard bands** needed (prevent interference)
- Filters needed to receive proper channel
- Receiver must know frequency band for reception

**Advantages:**
- Simple implementation
- Established technology
- Works well for analog signals

**Disadvantages:**
- Guard bands waste spectrum
- Inflexible (fixed allocation)

**Example:**
```
Frequency
  ↑
  |  [Flow 3]
  |  guard band
  |  [Flow 2]
  |  guard band
  |  [Flow 1]
  └────────────→ Time
```

#### OFDM (Orthogonal Frequency Division Multiplexing)

**Enhancement of FDM:**
- Partially overlapping frequency bands
- Uses orthogonal signals
- At peak value of one subcarrier, all others are zero

**Advantages:**
- High spectral efficiency
- No guard bands needed

**Disadvantages:**
- Strict synchronization requirements

**Usage:** Modern digital networks (optical, xDSL, 4G/5G)

---

### 2. TIME DIVISION MULTIPLEXING (TDM)

**Principle:** Each flow uses different time intervals (slots)

**Structure:**
- Define **frame** to repeat slot allocations
- Each frame typically lasts 125 μs
- Receiver must know proper time slots for reception

**Advantages:**
- Flexible allocation
- Works well for digital signals
- Easy to implement

**Disadvantages:**
- Requires synchronization
- Fixed allocation may waste capacity

**Example:**
```
Time
  →
|Slot1|Slot2|Slot3|...|Slot1|Slot2|Slot3|...
     Frame (125 μs)         Frame
```

**Usage:** SONET/SDH, GSM, traditional digital telephone networks

---

### 3. CODE DIVISION MULTIPLEXING (CDM/CDMA)

**Principle:** Each flow uses different code (waveform)

**Requirements:**
- Need orthogonal codes
- Higher frequency than transmission bit rate

**Key Point:** Code is NOT a new dimension
- Not a subset of time or frequency
- **Does NOT increase channel capacity**
- Can "increase" capacity with pseudo-orthogonal codes
- **BUT:** Degrades signal-to-noise ratio (increases bit error rate)

**Usage:** 3G cellular networks (UMTS)

---

### 4. SPACE MULTIPLEXING

**Principle:** Use physical separation to reuse resources

**Examples:**
- Multiple parallel wires
- Routing techniques exploiting space to increase capacity
- **Cells in wireless networks** (frequency reuse in different cells)

---

### Statistical Multiplexing

**Two Types of Multiplexing:**

#### Deterministic Multiplexing
- Fixed in time
- Based on requirements determined at connection setup
- Predictable allocation

#### Statistical Multiplexing
- Variable in time
- Adapts to instantaneous traffic requirements
- **Dynamic TDM scheme**

**Example:**
```
100 Mbps Ethernet

A ──┐
B ──┼──→ [Queue] ──→ 1.5 Mbps link ──→ D, E
C ──┘

Sequence of A & B packets does not have fixed pattern
Bandwidth shared on demand
```

**Advantages:**
- Efficient use of resources
- Adapts to traffic patterns
- Better for bursty traffic

**Disadvantages:**
- More complex
- Requires queuing/buffering
- Variable delays

### 📊 Exam Pattern

**Question:** "TDM, FDM, CDM, and space are ___ alternatives"  
**Answer:** Equivalent (can choose based on technological constraints)

**Question:** "Statistical multiplexing adapts to ___"  
**Answer:** Instantaneous traffic requirements

---

# PART 6: SWITCHING TECHNIQUES

## 🎯 SLIDES 116-154: Circuit Switching vs Packet Switching

### Core Concepts

**Switching:** Resource allocation process for the time needed to transfer information

**Two Main Techniques:**
1. **Circuit Switching:** For continuous, regular flows (voice)
2. **Packet Switching:** For bursty, unpredictable flows (data)

---

### CIRCUIT SWITCHING

#### Definition and Characteristics

**Definition:** Resources allocated on demand to create a circuit

**Circuit:**
- Physical link (or logical equivalent) directly connecting two user terminals
- Uniquely allocated to two users for whole call duration
- No other user can use circuit until call ends

**Three Phases:**
1. **Opening:** Circuit establishment via signalling
2. **Data Transfer:** Information exchange
3. **Closing:** Circuit release via signalling

**Example:** Telephone network

#### Advantages ✅

1. **Fixed guaranteed bit rate**
   - Predictable performance
   - Constant bandwidth

2. **Fixed transfer delay**
   - Predictable timing
   - No variability

3. **Circuit transparency**
   - Format, speed, protocol independent
   - Just change terminals to change application

4. **Negligible delays** in crossing nodes
   - Direct path established

#### Disadvantages ❌

1. **Resources allocated to single call**
   - Efficient only for non-bursty (regular) flows
   - Wastes capacity during silent periods

2. **Time needed to open circuit**
   - Setup delay before communication

3. **No format/speed/protocol conversion**
   - Network cannot perform error control
   - End-to-end responsibility

4. **Rate (price) time-based**
   - Pay for connection duration, not data volume

#### Node Architecture

**Components:**
- Input interface
- **Switching matrix** (interconnection network)
- Output interface
- Control system
- Signalling handling

**Operation:**
- Signalling sets up path through matrix
- Data flows directly through established path
- No packet processing in nodes

---

### PACKET SWITCHING

#### Definition and Characteristics

**Definition:** Data organized in packets with user data + control information

**Origin:** Leonard Kleinrock (1960s)

**Key Concept:**
- No exclusive resource allocation
- Whole network available for each user
- Well suited for bursty sources
- Similar to mailing system

#### Packet Structure

**PDU (Protocol Data Unit):**
```
┌─────────┬──────────┐
│   PCI   │   SDU    │
│ Header  │   Data   │
└─────────┴──────────┘
```

**Terms (All mean data unit):**
- PDU = Protocol Data Unit
- PCI = Protocol Control Information (header)
- SDU = Service Data Unit (user data)
- Other names: Packet, Cell, Datagram, Segment, Message, Frame

#### Store-and-Forward Behavior

**Each Node:**
1. **Stores** packet while receiving
2. **Processes** packet to determine output channel (routing)
3. **Stores** packet in queue for transmission
4. **Forwards** to next node

**Implies Delays:**
- Processing delay
- Transmission delay
- Reception delay
- **Queueing delay** (variable!)

**Why Store-and-Forward?**
- Need to read header for routing
- Routing requires processing time
- Header error protection needed
- Different links may have different speeds

#### Node Architecture

**Components:**
- Input interface
- **Memories** (buffering)
- Interconnection network / Switching matrix
- Output queues
- Output interface
- Control system (processing)

**Buffering Locations:**
- At outputs (most common)
- At inputs
- Mixed (shared)

#### Delays in Packet Switching

**Four Types of Delays:**

1. **Transmission Delay**
   - Function of packet size (bits) and link bit rate
   - TTX = P/VTX where P = packet size, VTX = link bit rate

2. **Propagation Delay**
   - Function of link length (meters)
   - Speed of light × link length

3. **Processing Delay**
   - Function of processing speed and complexity
   - Normally negligible vs transmission time

4. **Queueing Delay**
   - Depends on traffic from all users
   - **Highly variable** (unpredictable)

#### Packet Size Considerations

**Small Packets:**
- ✅ Increase transmission pipeline
- ✅ Enable parallel transmission (pipelining)
- ✅ Reduce node latency
- ✅ Reduce packetization delay (critical for voice)
- ✅ Lower error probability: (1-p)^n higher for small n
- ❌ Higher overhead (more headers)
- ❌ Need reassembly

**Large Packets:**
- ✅ Reduce percentage of control information: p/(s+p) smaller
- ✅ Less overhead
- ❌ Longer delays
- ❌ Higher error probability
- ❌ More data lost if error occurs

**Pipelining Example:**
```
Without pipelining (10 kB packet):
A → B → C → D: 1s + 1s + 1s = 3s

With pipelining (1 kB packets):
A → B → C → D: 0.1s×10 + 0.1s + 0.1s = 1.2s
```

#### Advantages ✅

1. **Efficient resource utilization** for bursty sources
2. **Error control possible** in network nodes
3. **Format/speed/protocol conversion** possible
4. **Accounting** based on data amount (fairer)

#### Disadvantages ❌

1. **Difficult to guarantee** bit rate and delay
2. **Each packet processed** at each node (overhead)
3. **Highly variable delays** (queueing)

---

### Two Packet Switching Services

#### 1. DATAGRAM SERVICE

**Characteristics:**
- **Connectionless** approach
- No end-to-end agreement needed
- Each packet contains source and destination addresses
- **Each packet routed independently**
- Packets may follow different paths
- No flow concept in network

**Addressing:**
- **Global identifiers** required
- Must uniquely identify any pair of users network-wide

**Advantages:**
- No setup delay
- Simple
- Flexible

**Disadvantages:**
- Packets may arrive out of order
- Each packet must carry full address

**Example:** IP (Internet Protocol)

#### 2. VIRTUAL CIRCUIT SERVICE

**Characteristics:**
- **Connection-oriented** approach
- Communication in three phases:
  1. **Connection opening** (signalling)
  2. **Data transfer**
  3. **Connection closing** (signalling)
  
- Users and network must agree before data transfer
- Packets follow **same path**
- Network aware of flow concept

**Addressing:**
- **Local identifiers (labels)** sufficient
- Labels can be reused on different paths
- Changed at each link

**Label Pairs:**
- VCI-VPI in ATM
- LCG-LCN in X.25/ISDN

**Advantages vs Datagram:**
- ✅ Sequence guaranteed
- ✅ Delays more controlled (reduced variability)
- ✅ Routing only at connection opening
- ✅ More efficient addressing (local labels)

**Two Types:**
- **SVC (Switched Virtual Circuit):** Created on demand via signalling
- **PVC (Permanent Virtual Circuit):** Created via management (semi-static)

**Important:** It is packet switching!
- No static resource allocation
- Resource sharing
- NOT equivalent to circuit switching

**Example:** ATM, Frame Relay, MPLS

---

### Circuit vs Packet Switching Comparison

| Feature | Circuit Switching | Packet Switching |
|---------|------------------|------------------|
| **Resource Allocation** | Dedicated | Shared |
| **Setup** | Required | Not required (datagram) |
| **Bit Rate** | Fixed, guaranteed | Variable, best effort |
| **Delay** | Fixed, low | Variable, queueing |
| **Best For** | Continuous, regular flows (voice) | Bursty, unpredictable flows (data) |
| **Processing** | Minimal in nodes | Every packet processed |
| **Error Control** | End-to-end only | Can be done in network |
| **Efficiency** | Low for bursty traffic | High for bursty traffic |
| **Pricing** | Time-based | Volume-based |

### 📊 Exam Patterns

**Question:** "Circuit switching is connection-oriented: T/F?"  
**Answer:** TRUE

**Question:** "Packet switching has better network response than message switching: T/F?"  
**Answer:** TRUE (smaller units = better response)

**Question:** "There is no store-and-forward for message exchange: T/F?"  
**Answer:** FALSE (message switching DOES have store-and-forward)

**Question:** "Suitable for bursty traffic: circuit or packet?"  
**Answer:** Packet switching

### ⚠️ Common Exam Traps

1. **"Message switching has no store-and-forward"**
   - WRONG! It DOES have store-and-forward

2. **"Virtual circuit = Circuit switching"**
   - WRONG! Virtual circuit is packet switching with connection setup

3. **"Packet switching guarantees delay"**
   - WRONG! Delays are variable (queueing)

---

# PART 7: SIGNALLING TECHNIQUES

## 🎯 SLIDES 155-162: Signalling Classification

### Signalling Definition (ITU-T)

**Signalling:** Exchange of control information associated with setup and release of a call on a telecommunications circuit

### Two Classifications

#### 1. By Location

**User Signalling:**
- Between user and network access node
- Examples: Dialing, lifting handset

**Network Signalling:**
- Among network nodes
- Examples: Path coordination, resource allocation

#### 2. By Association with Channel

**Three Types:**

### Type 1: Associated Signalling (In-Band)

**Characteristics:**
- Controlling and controlled channels are **the same**
- Channels used at different times for data and signalling
- One-to-one correspondence between signalling and data channel

**Diagram:**
```
signalling
    ↓
────┼──── Channel
    ↓
```

**Usage:** Early telephone networks

### Type 2: Associated Signalling (Out-of-Band)

**Characteristics:**
- **Separate** controlling and controlled channels
- Still one-to-one correspondence
- Signalling channel dedicated to specific data channel

**Diagram:**
```
Channel 1  ←→ user data
Channel 2  ←→ signalling (for Channel 1)
```

**Usage:** Some modern systems

### Type 3: Common Channel Signalling

**Characteristics:**
- **Single signalling channel** controls many user channels
- Signalling channel is **packet switched**
- Most flexible and efficient

**Diagram:**
```
Channels 1, 2, ..., k  ←→ user data
Channel (separate)     ←→ signalling (for all)
```

**Example:** ITU-T SS7 (Signalling System No. 7)

**Advantages:**
- Efficient use of signalling resources
- Flexibility
- Separation of signalling network

**Leads to:**
- Definition of signalling network
- Logically (and sometimes physically) separated from data network
- Contains addresses and addressing schemes

### 📊 Exam Pattern

**Question:** "Common channel signalling controls ___ user channels"  
**Answer:** Many (single signalling channel for multiple data channels)

---

# PART 8: MANAGEMENT TECHNIQUES

## 🎯 SLIDES 163-164: Network Management Functions

### Network Management Organization

**Five Functions (FCAPS Model):**

#### 1. **F**ault Management
- Detect faults
- Isolate faults
- Correct faults
- Track fault history

#### 2. **C**onfiguration Management
- Device configuration
- Inventory management
- Network topology
- Parameter settings

#### 3. **A**ccounting Management
- Track usage
- Billing
- Resource utilization
- Cost allocation

#### 4. **P**erformance Management
- Monitor metrics
- Analyze performance
- Optimize operations
- Capacity planning

#### 5. **S**ecurity Management
- Access control
- Authentication
- Encryption
- Security policies

### 📊 Exam Pattern

**Question:** "FCAPS stands for ___"  
**Answer:** Fault, Configuration, Accounting, Performance, Security

**Note:** Low exam weight - just be familiar with the five functions

---

# PART 9: QUALITY OF SERVICE (QoS)

## 🎯 SLIDES 165-170: QoS and Traffic Characterization

### Quality of Service Fundamentals

#### Network Analysis vs Design

**Network Analysis:**
- **Given:** Service requests + Available resources
- **Define:** Quality of service

**Network Design:**
- **Given:** Service requests + Quality of service
- **Define:** Needed network resources

### Traffic Characterization

#### Analog Sources
- Voice, video
- Defined through spectral characterization
- Bandwidth, correlation, etc.

#### Digital Sources
- Data, digitized voice, digitized video
- Defined through:
  - Average bit rate
  - Burstiness

### Traffic Types

#### Constant Bit Rate (CBR)
**Examples:**
- Voice (64 kb/s)
- Videoconference (n × 64 kb/s)
- Uncompressed video (180 Mb/s)

**Characteristics:**
- Predictable
- Regular
- Fixed rate

**Parameter:** Bit rate (bit/s)

#### Variable Bit Rate (VBR)
**Examples:**
- Compressed voice (tens of kb/s)
- MPEG video (Mb/s)
- File transfer (kb/s to Gb/s)

**Characteristics:**
- Unpredictable
- Bursty
- Variable rate

**Parameters:**
- Peak bit rate
- Average bit rate
- Burstiness factor

### Mathematical Models

**Purpose:**
- Characterize service requests
- Describe interaction among activities and resources
- Compute quality of service
- Design network resources

### 📊 Exam Pattern

**Question:** "CBR traffic has ___ bit rate"  
**Answer:** Constant / Fixed

**Question:** "VBR is characterized by ___"  
**Answer:** Average bit rate and burstiness

**Note:** Low exam weight - understand basic concepts

---

# SUMMARY: EXAM-CRITICAL POINTS FOR CHAPTER 1

## 🎯 MUST MEMORIZE

### Definitions
- **Telecommunication:** Transmission/reception via cables, radio, optical, EM media
- **Signalling:** Exchange of control information for call setup/release
- **Switching:** Interconnecting for time needed to transfer signals
- **Transmission:** Signal transfer from point to point(s)

### Four Main Functions
1. Signalling (implies routing)
2. Switching (implies routing)
3. Transmission
4. Management

### Bandwidth
- **Signal theory:** Spectral width (Hz)
- **Network jargon:** Bit rate (bit/s) ← **Most exams use this!**

### Throughput Constraints
```
Throughput ≤ Channel Capacity
Throughput ≤ Offered Traffic
```

### Topology Formulas
- **Fully Meshed:** C = N(N-1)/2
- **Tree:** C = N - 1
- **Active Star:** C = N
- **Passive Star:** C = 1
- **Ring (bidirectional):** C = N
- **Meshed:** N-1 < C < N(N-1)/2

### Device-Layer Mapping
- **Hub:** Layer 1 (Physical) - Passive star - Broadcast
- **Switch:** Layer 2 (Data Link) - Active star - Selective forwarding
- **Router:** Layer 3 (Network) - Different chapter

### Channel Types
- **Point-to-point:** 2 nodes, exclusive use
- **Multipoint:** Master + slaves, asymmetric
- **Broadcast:** All nodes, needs addressing

### Switching Types
- **Circuit:** Dedicated, guaranteed, continuous flows (voice)
- **Packet:** Shared, variable, bursty flows (data)
- **Datagram:** Connectionless, global addressing
- **Virtual Circuit:** Connection-oriented, local labels

### Signalling Types
- **User:** User ↔ Network
- **Network:** Node ↔ Node
- **In-band:** Same channel, different times
- **Out-of-band:** Separate channels, 1-to-1
- **Common channel:** One signalling for many data channels

## ⚠️ COMMON EXAM TRAPS

1. **Bandwidth meaning:** Network jargon = bit rate (NOT Hz)
2. **Hub vs Switch layers:** Hub = L1, Switch = L2 (NOT L3!)
3. **Message switching:** DOES have store-and-forward
4. **Virtual circuit:** IS packet switching (NOT circuit switching)
5. **Physical vs Logical topology:** Can be different!
6. **Meshed topology:** Most common in practice
7. **Throughput:** Limited by minimum of capacity and offered traffic

## 📊 EXAM WEIGHT DISTRIBUTION

**High Priority (Study thoroughly):**
- Topologies and formulas
- Hub vs Switch (layer identification)
- Circuit vs Packet switching
- Bandwidth definition
- Channel types

**Medium Priority (Understand well):**
- Four network functions
- Multiplexing techniques
- Virtual circuits vs Datagrams
- Delays in packet switching

**Low Priority (Brief review):**
- Management functions (FCAPS)
- QoS and traffic characterization
- Signalling techniques details
- Client-server vs P2P

---

**END OF CHAPTER 1: NETWORK FUNDAMENTALS**

**Status:** ✅ Complete - Ready for exam preparation  
**Next Chapter:** Protocol Architectures (Highest priority ⭐⭐⭐)

