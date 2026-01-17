# CHAPTER 7: STANDARD LAN - IEEE 802 STANDARDS (ETHERNET & WIFI)
## Exam-Oriented Study Guide

**Based on:** Professor's lecture slides (Modern LANs slides 1-74)  
**Exam Weight:** Very High (⭐⭐⭐+) - Approximately 20-25% of exam questions  
**Study Priority:** CRITICAL - Most important chapter for modern networks

---

## 📋 CHAPTER OVERVIEW

This chapter covers **IEEE 802 Standards** for Local Area Networks, with detailed focus on Ethernet (802.3) and the evolution from shared media to switched networks.

**Main Topics:**
1. IEEE 802 Architecture and Standards
2. MAC and LLC Addressing
3. Ethernet Frame Format and Evolution
4. Fast Ethernet, Gigabit Ethernet, 10/100 Gigabit
5. Hubs vs Switches
6. Bridge/Switch Forwarding and Learning

---

# PART 1: IEEE 802 ARCHITECTURE

## 🎯 SLIDES 2-7: IEEE 802 Standard Structure

### IEEE 802 Layer Architecture

**Layer 2 Divided into Two Sublayers:**

```
┌──────────────────────┐
│   Network Layer (3)  │
├──────────────────────┤
│   LLC (802.2)        │  ← Logical Link Control
├──────────────────────┤
│   MAC                │  ← Media Access Control
│ (802.3, 802.11, etc) │
├──────────────────────┤
│   Physical Layer (1) │
└──────────────────────┘
```

**Two Sublayers:**

#### 1. LLC - Logical Link Control (Upper)
- **Standard:** 802.2
- **Function:** Interface to network layer
- **Services:** Optional error control, flow control
- **Multiplexing:** Higher layer protocols

#### 2. MAC - Media Access Control (Lower)
- **Standards:** 802.3 (Ethernet), 802.11 (WiFi), etc.
- **Function:** Media access, addressing, framing
- **Technology-specific:** Different for each LAN type

---

### IEEE 802 Standards (Historical)

**Original Standards (1980s):**

| Standard | Name | Technology | Status |
|----------|------|------------|--------|
| **802.1** | Internetworking | Bridging, VLANs | ✅ Active |
| **802.2** | LLC | Logical Link Control | ✅ Active |
| **802.3** | Ethernet | CSMA/CD | ✅ **Active** (Most Important!) |
| 802.4 | Token Bus | Token passing on bus | ❌ Obsolete |
| 802.5 | Token Ring | Token passing on ring | ❌ Obsolete |
| 802.6 | DQDB | Metropolitan area network | ❌ Obsolete |

**More Recent Standards:**

| Standard | Name | Status |
|----------|------|--------|
| 802.7 | Broadband Technical Advisory | Advisory |
| 802.8 | Fiber-Optic Technical Advisory | Advisory |
| 802.9 | Integrated Data and Voice | Obsolete |
| 802.10 | Network Security | Advisory |
| **802.11** | **WiFi** | ✅ **Active** (Very Important!) |
| 802.12 | 100BaseVG | Obsolete |
| **802.15** | **Bluetooth/Sensors** | ✅ Active |
| 802.17 | Resilient Packet Ring | Limited use |

**Key Takeaway:** Only 802.1, 802.2, **802.3 (Ethernet)**, and **802.11 (WiFi)** are widely used today.

---

### Layer 2 Functions Distribution

**LLC Functions:**
- Error correction (optional - window protocols)
- Flow control (toward higher layer)
- Higher layer protocol multiplexing (LSAP addresses)

**MAC Functions:**
- Frame delineation (silence, SFD)
- Error detection (CRC)
- Addressing (MAC addresses for NIC identification)
- Multiplexing (in Ethernet, can also multiplex protocols)

---

### 📊 Exam Pattern

**Question:** "IEEE 802.3 standard defines ___"  
**Answer:** **Ethernet** (CSMA/CD)

**Question:** "IEEE 802.11 standard defines ___"  
**Answer:** **WiFi** (wireless LAN)

**Question:** "Two sublayers of Layer 2 in IEEE 802?"  
**Answer:** **LLC (upper) and MAC (lower)**

**Question:** "Token Ring is IEEE 802.___"  
**Answer:** **802.5** (obsolete)

---

# PART 2: MAC ADDRESSING

## 🎯 SLIDES 8-13: MAC Address Structure and Types

### MAC Address Basics

**Size:** **6 bytes (48 bits)**

**Format:** XX-XX-XX-XX-XX-XX (hexadecimal)

**Uniqueness:** Originally globally unique (now can be configured)

**Location:** Stored in Network Interface Card (NIC)
- Originally: ROM (Read-Only Memory)
- Now: Can be selected/configured

---

### MAC Address Structure

**Two Parts:**

#### 1. OUI - Organizationally Unique Identifier (3 bytes)
- **First 3 bytes (24 bits)**
- Assigned to NIC manufacturer
- Identifies vendor

#### 2. NIC Number (3 bytes)
- **Last 3 bytes (24 bits)**
- Unique number assigned by manufacturer
- Device-specific

**Example:**
```
02-60-8C-07-9A-4D
└─┬──┘ └───┬────┘
 OUI    NIC Number
(3Com)  (Device ID)

EC-22-80-07-9A-4D
└─┬──┘
 OUI
(D-Link)
```

---

### Special Bits in MAC Address

**First Byte Contains Two Special Bits:**

#### Bit 7 (7th bit of first byte):
- **0 = Globally unique** (worldwide unique, assigned by IEEE)
- **1 = Locally administered** (chosen locally, not globally unique)

#### Bit 8 (8th bit / LSB of first byte):
- **0 = Unicast** (single destination)
- **1 = Multicast** (group of destinations)

---

### MAC Address Types

#### 1. UNICAST Address
- **Purpose:** Single specific node
- **Format:** Normal MAC address with bit 8 = 0
- **Use:** Most common - point-to-point communication

#### 2. MULTICAST Address
- **Purpose:** Group of nodes
- **Format:** Bit 8 = 1
- **Use:** Send to multiple nodes simultaneously
- **Configuration:** Group membership configured via software

#### 3. BROADCAST Address
- **Purpose:** ALL nodes on LAN
- **Value:** **FF-FF-FF-FF-FF-FF** (all bits = 1)
- **Use:** Network-wide announcements

---

### NIC Packet Reception Rules

**NIC Accepts Packet If:**
1. **Unicast** address = NIC's MAC address
2. **Broadcast** address (FF-FF-FF-FF-FF-FF)
3. **Multicast** address enabled on NIC

**NIC Rejects:** All other addresses

**Exception: Promiscuous Mode**
- Captures ALL packets regardless of destination
- Used for network monitoring/analysis
- Configured via software

---

### 📊 Exam Pattern

**Question:** "MAC address size is ___"  
**Answer:** **6 bytes or 48 bits**

**Question:** "First 3 bytes of MAC address identify ___"  
**Answer:** **Manufacturer** (OUI - Organizationally Unique ID)

**Question:** "Broadcast MAC address is ___"  
**Answer:** **FF-FF-FF-FF-FF-FF**

**Question:** "Promiscuous mode means ___"  
**Answer:** **Capture all packets regardless of destination address**

**Question:** "Bit 8 of first byte: 0 = ___, 1 = ___"  
**Answer:** **0 = Unicast, 1 = Multicast**

---

# PART 3: ETHERNET FRAME FORMAT

## 🎯 SLIDES 14-21: Ethernet vs IEEE 802.3

### History

**Ethernet:**
- Designed by **Bob Metcalfe** in 1970s
- Developed by **DIX** (Digital, Intel, Xerox)
- **Ethernet 2.0** published 1982

**IEEE 802.3:**
- Defined by IEEE in 1985
- Based on Ethernet
- Minor differences in frame format

**Key Point:** Ethernet and 802.3 are very similar, differ mainly in one header field

---

### Ethernet Frame Format (DIX Ethernet 2.0)

```
┌──────────┬─────┬──────────┬──────────┬────────┬──────────┬─────┬─────┐
│Preamble  │ SFD │ Dest MAC │  Src MAC │Protocol│   DATA   │ FCS │ IPG │
│(7 bytes) │(1 B)│ (6 bytes)│ (6 bytes)│ (2 B)  │(46-1500 B)│(4 B)│(12 B)│
└──────────┴─────┴──────────┴──────────┴────────┴──────────┴─────┴─────┘
```

**Fields:**

1. **Preamble: 7 bytes**
   - Pattern: 10101010... (alternating)
   - Purpose: Synchronization, clock recovery

2. **SFD (Start Frame Delimiter): 1 byte**
   - Pattern: 10101011
   - Purpose: Indicates frame start

3. **Destination MAC: 6 bytes**
   - Destination address

4. **Source MAC: 6 bytes**
   - Source address

5. **Protocol Type: 2 bytes** ← **Key Difference**
   - Values **> 1500**
   - Indicates higher layer protocol
   - Examples: 0x0800 = IPv4, 0x0806 = ARP, 0x86DD = IPv6

6. **DATA: 46-1500 bytes**
   - Payload
   - Minimum 46 bytes (padding if needed)

7. **FCS (Frame Check Sequence): 4 bytes**
   - CRC-32 for error detection

8. **IPG (Inter-Packet Gap): 12 bytes equivalent**
   - Silence between frames

---

### IEEE 802.3 Frame Format

```
┌──────────┬─────┬──────────┬──────────┬────────┬──────────┬───────┬─────┬─────┐
│Preamble  │ SFD │ Dest MAC │  Src MAC │ Length │   DATA   │Padding│ FCS │ IPG │
│(7 bytes) │(1 B)│ (6 bytes)│ (6 bytes)│ (2 B)  │(0-1500 B)│(0-46B)│(4 B)│(12 B)│
└──────────┴─────┴──────────┴──────────┴────────┴──────────┴───────┴─────┴─────┘
```

**Key Difference:**

**Length Field: 2 bytes** ← **Instead of Protocol Type**
- Values **≤ 1500**
- Indicates data field length
- Protocol type indicated by LLC header (in DATA)

**Padding:**
- Added if data < 46 bytes
- Ensures minimum frame size

---

### How to Distinguish Ethernet vs 802.3?

**Rule:** Look at the 2-byte field after source MAC

- **Value > 1500** → Ethernet (Protocol Type)
- **Value ≤ 1500** → IEEE 802.3 (Length)

**Practical:** Modern networks use both
- Pure Ethernet common for IP
- 802.3 with LLC for some protocols

---

### Design Parameters (CRITICAL!)

**Classic 10 Mbps Ethernet:**

**Joint Definition (All Related):**

1. **Minimum Packet Size:** **64 bytes**
   - Including IPG (12 bytes)
   - Actual frame content: 64 - 12 = 52 bytes minimum
   - Or: 18 bytes header/trailer + 46 bytes data minimum

2. **Transmission Speed:** **10 Mbps**

3. **Maximum Network Size:** **2800 meters**

**Why Related?**

**Formula:**
```
Minimum Frame Time ≥ 2 × Maximum Propagation Delay

For collision detection:
Frame Transmission Time ≥ RTT (Round Trip Time)
```

**Calculation:**
```
64 bytes × 8 bits/byte = 512 bits
512 bits / 10 Mbps = 51.2 μs (minimum frame time)

Must be ≥ 2 × propagation delay
Therefore: Maximum propagation delay = 25.6 μs

Distance = propagation delay × signal speed
2800m ≈ 25.6 μs × signal speed in copper
```

**Key Point:** If you increase speed, must either:
- Increase minimum frame size, OR
- Decrease maximum network size

---

### 📊 Exam Pattern

**Question:** "Ethernet designed by ___"  
**Answer:** **Bob Metcalfe**

**Question:** "Ethernet 2.0 vs 802.3 main difference?"  
**Answer:** **Protocol Type field (>1500) vs Length field (≤1500)**

**Question:** "Minimum Ethernet frame size?"  
**Answer:** **64 bytes** (including IPG)

**Question:** "Classic Ethernet speed and max distance?"  
**Answer:** **10 Mbps, 2800 meters**

**Question:** "SFD pattern is ___"  
**Answer:** **10101011**

**Question:** "IPG means ___"  
**Answer:** **Inter-Packet Gap** (silence between frames)

---

# PART 4: ETHERNET PHYSICAL LAYER

## 🎯 SLIDES 22-24: Physical Layer Specifications

### Classic Ethernet (10 Mbps)

**Bit Rate:** 10 Mbps
- Bit time = 0.1 μs (100 nanoseconds)

**Encoding:** **Manchester**
- Requires 20 MHz clock (2× bit rate)
- Purpose: Clock recovery in asynchronous environment
- Preamble helps recover transmitter clock

**Maximum Stations:** 1024

**Transmission Media:**

| Name | Medium | Cable Type | Notes |
|------|--------|------------|-------|
| **10BASE5** | Coax | Thick coax (RG213) | Original, obsolete |
| **10BASE2** | Coax | Thin coax (RG58) | Cheaper, obsolete |
| **10BASE-T** | UTP | 100Ω unshielded twisted pair | **Most common** |
| 10BASE-FL/FB/FP | Fiber | Multimode fiber (850nm) | First window |

**Naming Convention:** `<Speed>BASE<Medium>`
- Speed in Mbps
- BASE = Baseband (vs broadband)
- T = Twisted pair, 2/5 = coax segment length (×100m), F = Fiber

---

### 📊 Exam Pattern

**Question:** "Ethernet encoding method?"  
**Answer:** **Manchester** (at 10 Mbps)

**Question:** "10BASE-T uses which medium?"  
**Answer:** **UTP (Unshielded Twisted Pair)**

**Question:** "10BASE5 uses which medium?"  
**Answer:** **Thick coaxial cable**

---

# PART 5: ETHERNET EVOLUTION

## 🎯 SLIDES 25-30: Fast, Gigabit, and High-Speed Ethernet

### Evolution Challenge

**Problem:** How to increase speed beyond 10 Mbps?

**Constraint:** Minimum packet size (64 bytes) and maximum distance (2800m) are related

**Solutions:**

#### At 100 Mbps (Fast Ethernet):
- **Reduce maximum distance to 100m**
- Keep 64-byte minimum frame

#### At 1 Gbps (Gigabit Ethernet):
- **Increase minimum frame size by 10×** (to 640 bytes in half-duplex)
- OR use **full-duplex** (no collision domain → no minimum)

#### At 10+ Gbps:
- **Full-duplex only** (point-to-point)
- No CSMA/CD needed
- No collision domain concept

---

### Fast Ethernet (100 Mbps) - IEEE 802.3u

**Speed:** 100 Mbps

**Maximum Distance:** **100 meters**

**Key Technology:** **100BASE-TX**
- Line coding: **4B5B** (not Manchester)
- Medium: UTP Cat5 cables
- Auto-negotiation support

**Advantages:**
- 10× speed improvement
- Still uses CSMA/CD
- Backward compatible

**Limitation:** Short distance (100m)

---

### Gigabit Ethernet (1 Gbps) - IEEE 802.3ab/z

**Speed:** 1 Gbps (1000 Mbps)

**Frame Format:** Same as 802.3

**MAC Protocol:** CSMA/CD (but usually switched)

**Operation Modes:**
- **Half-duplex:** Collision possible (rare)
- **Full-duplex:** Point-to-point, no collisions (common)

**Key Changes:**

**1. Minimum Frame Size (Half-Duplex):**
- Increased by **factor of 10**
- Reason: Keep ratio of frame transmission time to propagation time constant

**2. Jumbo Frames:**
- Up to **9216 bytes**
- Reduces overhead
- Not standard, but widely supported

**3. Encoding:** **8B10B**
- Easier synchronization
- Better clock recovery

**Backward Compatibility:** Yes, with traditional Ethernet

---

### 10 Gigabit Ethernet - IEEE 802.3ae (2002)

**Speed:** 10 Gbps

**Key Change:** **Full-duplex ONLY**
- Point-to-point links
- **No multiple access**
- **CSMA/CD not necessary** anymore

**Media Support:**

**Copper:**
- 10GBASE-CX4 (InfiniBand cables)
- 10GBASE-T (Cat 7 twisted pair)

**Fiber:**
| Type | Medium | Distance |
|------|--------|----------|
| 10GBASE-SR | MMF (Multi-Mode) | 65m / 300m |
| 10GBASE-LR | SMF (Single-Mode) | 2 km |
| 10GBASE-ER | SMF | 10 km |
| 10GBASE-ZR | SMF | 40 km |

**On SDH:** Can go > 40 km

---

### 2.5 and 5 Gigabit Ethernet - IEEE 802.3bz

**Motivation:**
- WiFi 6/6e reaches 1.2 Gbps per channel
- Gigabit Ethernet no longer sufficient
- 10 Gigabit requires fiber

**Solution:** Intermediate speeds
- **2.5GBASE-T**
- **5GBASE-T**

**Medium:** UTP Cat 5e (existing infrastructure)

**Purpose:** Bridge gap between Gigabit and 10 Gigabit

---

### 100 Gigabit Ethernet - IEEE 802.3ba (2010)

**Speeds:** 40 Gbps and 100 Gbps

**Technology:** Parallel transmission
- Example: 20 wires × 5.15625 Gbps each
- Round-robin transmission
- **64B/66B encoding**

**Challenge:** Synchronization among multiple wires

**Status:** Data center, high-performance computing

---

### Ethernet Evolution Summary

| Standard | Speed | Year | Max Distance | Key Feature |
|----------|-------|------|--------------|-------------|
| Ethernet | 10 Mbps | 1980s | 2800m | CSMA/CD, Manchester |
| Fast Ethernet | 100 Mbps | 1995 | 100m | 4B5B coding |
| Gigabit | 1 Gbps | 1998 | Varies | 8B10B, jumbo frames |
| 2.5G/5G | 2.5/5 Gbps | 2016 | 100m | Cat 5e support |
| 10 Gigabit | 10 Gbps | 2002 | Up to 40km | **Full-duplex only** |
| 40/100 Gigabit | 40/100 Gbps | 2010 | Varies | Parallel transmission |

---

### 📊 Exam Pattern

**Question:** "Fast Ethernet speed and max distance?"  
**Answer:** **100 Mbps, 100 meters**

**Question:** "Gigabit Ethernet encoding?"  
**Answer:** **8B10B**

**Question:** "10 Gigabit Ethernet uses CSMA/CD?"  
**Answer:** **No** - full-duplex only, point-to-point

**Question:** "Jumbo frames size?"  
**Answer:** **Up to 9216 bytes**

**Question:** "4B5B encoding used in ___"  
**Answer:** **Fast Ethernet (100BASE-TX)**

---

# PART 6: LAN INTERCONNECTION DEVICES

## 🎯 SLIDES 31-40: Hubs vs Switches

### Modern LAN Topology Evolution

**1990s Changes:**
- Need for higher bit rates (>10 Mbps)
- **Structured cabling** - hierarchical star topology
- Star center devices: Hub or Switch

### Hub (Repeater) - Layer 1 Device

**Function:** Multi-port repeater

**Operation:**
- Operates at **bit level** (Physical Layer - Layer 1)
- Regenerates bit strings
- Forwards on **ALL ports**
- **3R:** Re-generation, Re-shaping, Re-timing

**Characteristics:**
- **Shared bit rate** on all ports
- **Single collision domain** (all ports)
- No intelligence
- Does not recognize packets
- Passive star

**Topology:**
- Star-based (twisted pair or fiber)
- Structured cabling

**Advantages:**
- ✅ Simple
- ✅ Cheap
- ✅ Extends cable length

**Disadvantages:**
- ❌ No capacity increase
- ❌ All ports share bandwidth
- ❌ Single collision domain
- ❌ Performance degrades with load

**Status:** ❌ **Obsolete** - not used in modern networks

---

### Switch (Bridge) - Layer 2 Device

**Function:** Intelligent forwarding based on MAC addresses

**Operation:**
- Operates at **frame level** (Data Link Layer - Layer 2)
- **Store and forward**
- Selective forwarding based on destination MAC
- Creates **separate collision domains per port**

**Characteristics:**
- **Dedicated bit rate per port**
- Can have **single user per port**
- **Intelligent routing** (MAC address table)
- **Transparent to users**
- Active star

**Key Features:**

**1. Store and Forward:**
- Receives entire frame
- Checks for errors
- Forwards only correct frames
- Buffer overflow possible → packet loss

**2. Selective Forwarding:**
- Only sends to destination port
- Not broadcast to all ports (unlike hub)

**3. Backward Learning:**
- Dynamically learns MAC addresses
- Builds forwarding table automatically

**Advantages:**
- ✅ Increases network capacity
- ✅ Dedicated bandwidth per port
- ✅ Separate collision domains
- ✅ Performance improvement
- ✅ Can connect different speeds

**Disadvantages:**
- ❌ More expensive than hub
- ❌ More complex
- ❌ Can drop packets (buffer overflow)

**Status:** ✅ **Current standard** - all modern LANs use switches

---

### Collision Domains: Hub vs Switch

#### With Hub:
```
┌─────────────────────────────────┐
│   Single Collision Domain       │
│  ┌───┐                           │
│  │Hub│───PC1                     │
│  └───┘───PC2                     │
│    └─────PC3                     │
└─────────────────────────────────┘
All PCs compete for same bandwidth
```

#### With Switch:
```
┌────────────┐  ┌────────────┐  ┌────────────┐
│ Collision  │  │ Collision  │  │ Collision  │
│  Domain 1  │  │  Domain 2  │  │  Domain 3  │
│    PC1     │  │    PC2     │  │    PC3     │
└─────┬──────┘  └─────┬──────┘  └─────┬──────┘
      │               │               │
    ┌─┴───────────────┴───────────────┴─┐
    │           Switch                   │
    └────────────────────────────────────┘
Each PC has dedicated collision domain
```

**Key Insight:** With switches, **CSMA/CD becomes unnecessary**
- Each port is point-to-point
- Full-duplex possible (separate TX/RX)
- No collisions
- Ethernet becomes just a framing protocol

---

### Bridge vs Switch

#### Bridge (Old):
- Interconnects **buses** (coaxial)
- Tree-based topology
- Can connect **different MAC** types
- Runs spanning tree protocol

#### Switch (Modern):
- Interconnects via **star** (twisted pair/fiber)
- Active star topology
- Same MAC type (usually Ethernet)
- Runs spanning tree protocol
- Supports **VLANs**

**Key Point:** Switches are essentially modern bridges with more ports and better performance

---

### 📊 Exam Pattern

**Question:** "Hub operates at which layer?"  
**Answer:** **Layer 1** (Physical)

**Question:** "Switch operates at which layer?"  
**Answer:** **Layer 2** (Data Link)

**Question:** "Hub creates ___ collision domain(s)"  
**Answer:** **One** (single, shared)

**Question:** "Switch creates ___ collision domain per ___"  
**Answer:** **One collision domain per port**

**Question:** "Hub forwards to ___"  
**Answer:** **All ports** (broadcast)

**Question:** "Switch forwards based on ___"  
**Answer:** **MAC address** (destination MAC in forwarding table)

**Question:** "With switches, is CSMA/CD needed?"  
**Answer:** **No** - point-to-point, full-duplex, no collisions

---

# PART 7: SWITCH FORWARDING

## 🎯 SLIDES 41-43: Learning and Forwarding

### Three Fundamental Switch Functions

#### 1. Address Learning (Backward Learning Algorithm)
- Dynamically builds forwarding table
- **No manual configuration needed**

#### 2. Frame Forwarding
- Selective forwarding based on table lookup
- Forwards only to destination port

#### 3. Spanning Tree Algorithm
- Ensures loop-free topology
- Creates tree structure from meshed network

---

### Backward Learning Algorithm

**Purpose:** Automatically learn which MAC addresses are reachable through which ports

**Process:**

**For Each Received Frame:**

1. **Read Source MAC Address (MAC_S)**
   - Frame received on port PORT_X
   - Associate MAC_S with PORT_X

2. **Update Forwarding Table Entry:**
   - Add/update: (MAC_S, PORT_X)
   - Reset timer for this entry

3. **Use Later:**
   - When forwarding TO MAC_S
   - Send to PORT_X

**Timer Purpose:**
- Automatically adapt to topology changes
- Remove stale entries
- Keep table size manageable
- Typical: 5-10 minutes

**Why "Backward"?**
- Learns from **source** addresses (where frame came FROM)
- Uses for **destination** forwarding (where frame goes TO)

**Example:**
```
Frame arrives: SRC=AA:BB:CC, DST=DD:EE:FF, Port=1
Action: Learn (AA:BB:CC, Port 1)
Later: Frame with DST=AA:BB:CC → Send to Port 1
```

---

### Frame Forwarding Algorithm

**When Correct Frame Received on PORT_X:**

**Step 1: Read Destination MAC (MAC_D)**

**Step 2: Look Up MAC_D in Table**

**Case A: NOT Found (Unknown Destination)**
- **Action: FLOOD**
- Forward to **ALL ports** except PORT_X
- Like hub behavior (temporarily)

**Case B: Found, Associated with PORT_X (Same Port)**
- **Action: DROP**
- Frame already on correct LAN segment
- No forwarding needed

**Case C: Found, Associated with PORT_Y (Different Port)**
- **Action: FORWARD**
- Send ONLY to PORT_Y
- Selective forwarding

**Special Cases:**

**Broadcast Frame (DST = FF-FF-FF-FF-FF-FF):**
- **Always flood** to all ports except source

**Multicast Frame:**
- Forward to ports with multicast group members
- Or flood if unknown

**Error Frame:**
- **Drop immediately**
- Do not forward corrupted frames

---

### Forwarding Table Example

**Scenario:**

```
Extended LAN:

  LAN 1          LAN 2          LAN 3
    │              │              │
    A              │              C
    │              │              │
  ┌─┴──────────────┴──────────────┴─┐
  │          Switch B               │
  └─────────────────────────────────┘
 Port 1        Port 2        Port 3
```

**Learning Process:**

1. **A sends to C:**
   - Switch receives on Port 1
   - Learns: (MAC_A, Port 1)
   - MAC_C unknown → Flood to Ports 2, 3

2. **C replies to A:**
   - Switch receives on Port 3
   - Learns: (MAC_C, Port 3)
   - MAC_A known on Port 1 → Forward to Port 1 only

3. **Later, A sends to C again:**
   - MAC_A known (Port 1) - already learned
   - MAC_C known (Port 3) - forward to Port 3 only
   - **No flooding needed!**

**Final Table:**
```
| MAC Address | Port | Timer |
|-------------|------|-------|
| MAC_A       | 1    | 300s  |
| MAC_C       | 3    | 180s  |
```

---

### 📊 Exam Pattern

**Question:** "Switch forwarding table built how?"  
**Answer:** **Automatically** (backward learning algorithm)

**Question:** "Switch learns from ___ addresses"  
**Answer:** **Source** MAC addresses

**Question:** "If destination unknown, switch ___"  
**Answer:** **Floods** (forwards to all ports except source)

**Question:** "If destination on same port as source, switch ___"  
**Answer:** **Drops** the frame

**Question:** "Backward learning algorithm uses ___ for learning"  
**Answer:** **Source MAC address** (from received frames)

**Question:** "Forwarding table timer purpose?"  
**Answer:** **Remove stale entries** / adapt to topology changes

---

# SUMMARY: EXAM-CRITICAL POINTS FOR CHAPTER 7

## 🎯 MUST MEMORIZE

### IEEE 802 Standards

| Standard | Technology | Status |
|----------|------------|--------|
| **802.1** | Internetworking | ✅ Active |
| **802.2** | LLC | ✅ Active |
| **802.3** | **Ethernet** | ✅ **Active** (Most Important) |
| 802.4 | Token Bus | ❌ Obsolete |
| 802.5 | Token Ring | ❌ Obsolete |
| **802.11** | **WiFi** | ✅ **Active** (Very Important) |

### MAC Address

- **Size:** 6 bytes (48 bits)
- **Format:** XX-XX-XX-XX-XX-XX (hex)
- **OUI:** First 3 bytes (manufacturer)
- **NIC:** Last 3 bytes (device)
- **Broadcast:** FF-FF-FF-FF-FF-FF

### Ethernet Frame Differences

| Field | Ethernet 2.0 | IEEE 802.3 |
|-------|--------------|------------|
| After Source MAC | **Protocol Type** (>1500) | **Length** (≤1500) |
| Usage | Indicates protocol (IP, ARP, etc.) | Indicates data length |

### Classic Ethernet Parameters

- **Speed:** 10 Mbps
- **Min Frame:** 64 bytes (including IPG)
- **Max Distance:** 2800 meters
- **Encoding:** Manchester

### Ethernet Evolution

| Type | Speed | Distance | Encoding | Duplex |
|------|-------|----------|----------|--------|
| Ethernet | 10 Mbps | 2800m | Manchester | Half/Full |
| Fast | 100 Mbps | 100m | 4B5B | Half/Full |
| Gigabit | 1 Gbps | Varies | 8B10B | Half/Full |
| 10 Gigabit | 10 Gbps | Varies | 64B/66B | **Full only** |

### Hub vs Switch

| Feature | Hub | Switch |
|---------|-----|--------|
| **Layer** | **1 (Physical)** | **2 (Data Link)** |
| **Collision Domains** | **1 (shared)** | **1 per port** |
| **Bandwidth** | **Shared** | **Dedicated** |
| **Forwarding** | **All ports** | **Selective** (MAC-based) |
| **Intelligence** | **None** | **MAC learning** |
| **Status** | **Obsolete** | **Current** |

### Switch Forwarding

**Unknown destination:** Flood (all ports except source)  
**Known on same port:** Drop  
**Known on different port:** Forward to that port only

---

## ⚠️ COMMON EXAM TRAPS

### Trap 1: IEEE Standards
**WRONG:** "802.5 is Ethernet"  
**RIGHT:** "802.3 is Ethernet, 802.5 is Token Ring (obsolete)" ✓

### Trap 2: MAC Address Size
**WRONG:** "MAC address is 4 bytes"  
**RIGHT:** "MAC address is 6 bytes (48 bits)" ✓

### Trap 3: Ethernet Frame Field
**WRONG:** "Ethernet 2.0 has Length field"  
**RIGHT:** "Ethernet 2.0 has Protocol Type; 802.3 has Length" ✓

### Trap 4: Hub Layer
**WRONG:** "Hub operates at Layer 2"  
**RIGHT:** "Hub at Layer 1, Switch at Layer 2" ✓

### Trap 5: Collision Domains
**WRONG:** "Switch creates one collision domain"  
**RIGHT:** "Switch creates one collision domain PER PORT" ✓

### Trap 6: 10 Gigabit Ethernet
**WRONG:** "10GbE uses CSMA/CD"  
**RIGHT:** "10GbE is full-duplex only, no CSMA/CD" ✓

### Trap 7: Switch Forwarding
**WRONG:** "Switch forwards to all ports"  
**RIGHT:** "Switch forwards selectively based on MAC table" ✓

### Trap 8: Learning Algorithm
**WRONG:** "Switch learns from destination MAC"  
**RIGHT:** "Switch learns from SOURCE MAC (backward learning)" ✓

---

## 📊 EXAM WEIGHT DISTRIBUTION

### CRITICAL (Study exhaustively - 70%):
- ✅ IEEE 802.3 (Ethernet) and 802.11 (WiFi)
- ✅ MAC address structure (6 bytes, OUI + NIC)
- ✅ Broadcast address (FF-FF-FF-FF-FF-FF)
- ✅ Ethernet vs 802.3 frame difference
- ✅ Hub (Layer 1, shared) vs Switch (Layer 2, dedicated)
- ✅ Collision domains: Hub=1, Switch=1 per port
- ✅ Backward learning algorithm
- ✅ Switch forwarding rules

### HIGH (Study thoroughly - 20%):
- Ethernet evolution (10/100/1000/10000 Mbps)
- Manchester encoding (10 Mbps)
- 4B5B (Fast Ethernet), 8B10B (Gigabit)
- Minimum frame size (64 bytes) and why
- Full-duplex eliminates CSMA/CD need
- Promiscuous mode
- Unicast vs Multicast vs Broadcast

### MEDIUM (Understand well - 10%):
- Bob Metcalfe (Ethernet inventor)
- DIX (Digital, Intel, Xerox)
- Token Ring (802.5) - obsolete
- 10BASE-T, 10BASE5, 10BASE2 naming
- Jumbo frames (9216 bytes)
- Spanning tree (brief mention)

---

## 🎓 STUDY STRATEGY

### Day 1: IEEE 802 and MAC Addressing
- IEEE 802 standards (focus on 802.3, 802.11)
- LLC vs MAC sublayers
- MAC address structure (6 bytes, OUI)
- Address types (unicast, multicast, broadcast)

### Day 2: Ethernet Frame Formats
- Ethernet 2.0 frame format
- IEEE 802.3 frame format
- Key difference (Protocol Type vs Length)
- Minimum frame size (64 bytes) and why

### Day 3: Ethernet Evolution
- Classic Ethernet (10 Mbps, Manchester)
- Fast Ethernet (100 Mbps, 4B5B)
- Gigabit Ethernet (1 Gbps, 8B10B)
- 10 Gigabit (full-duplex only)

### Day 4: Hub vs Switch
- Hub characteristics (Layer 1, shared, one collision domain)
- Switch characteristics (Layer 2, dedicated, per-port collision)
- Why switches eliminate need for CSMA/CD

### Day 5: Switch Forwarding
- Backward learning algorithm
- Forwarding table building
- Three forwarding cases (unknown, same port, different port)
- Practice scenarios

---

## 📝 QUICK REFERENCE FLASHCARDS

**Q:** 802.3 standard?  
**A:** Ethernet

**Q:** 802.11 standard?  
**A:** WiFi

**Q:** MAC address size?  
**A:** 6 bytes (48 bits)

**Q:** Broadcast MAC?  
**A:** FF-FF-FF-FF-FF-FF

**Q:** Ethernet vs 802.3 difference?  
**A:** Protocol Type (>1500) vs Length (≤1500)

**Q:** Min Ethernet frame?  
**A:** 64 bytes

**Q:** Classic Ethernet speed?  
**A:** 10 Mbps

**Q:** Fast Ethernet speed?  
**A:** 100 Mbps

**Q:** Gigabit Ethernet encoding?  
**A:** 8B10B

**Q:** Hub layer?  
**A:** Layer 1 (Physical)

**Q:** Switch layer?  
**A:** Layer 2 (Data Link)

**Q:** Hub collision domains?  
**A:** 1 (shared)

**Q:** Switch collision domains?  
**A:** 1 per port

**Q:** Hub forwards to?  
**A:** All ports

**Q:** Switch learns from?  
**A:** Source MAC addresses

**Q:** Unknown destination action?  
**A:** Flood (forward to all except source)

**Q:** 10GbE uses CSMA/CD?  
**A:** No (full-duplex only)

---

**END OF CHAPTER 7: STANDARD LAN (IEEE 802)**

**Status:** ✅ Complete - Ready for exam preparation  
**Importance:** ⭐⭐⭐+ CRITICAL - 20-25% of exam  
**Next Chapter:** Routing (Network Layer)

