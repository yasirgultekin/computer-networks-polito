# CHAPTER 5: DATA LINK LAYER (LAYER 2)
## Exam-Oriented Study Guide

**Based on:** Professor's lecture slides (Data link layer protocols slides 1-54)  
**Exam Weight:** Medium-High (⭐⭐½) - Approximately 10-15% of exam questions  
**Study Priority:** MEDIUM-HIGH - Important protocols and functions

---

## 📋 CHAPTER OVERVIEW

This chapter covers the **Data Link Layer** (Layer 2) of the OSI model, focusing on protocol functions, HDLC family protocols, and framing techniques.

**Main Topics:**
1. Data Link Layer Functions
2. HDLC Protocol Family (SDLC, LAP-B, LAP-D, PPP, LLC)
3. Frame Structure and Format
4. Data Transparency (Bit Stuffing and Byte Stuffing)
5. Public vs Private Networks

---

# PART 1: DATA LINK LAYER FUNCTIONS

## 🎯 SLIDE 3: Core Functions

### Six Main Functions

#### 1. FRAME DELINEATION (Framing)

**Purpose:** Identify beginning and end of frames

**Four Techniques:**

**A. Explicit Delimiters (Flags)**
- Special bit pattern before and after frame
- Most common method
- Example: Flag 01111110 in HDLC

**B. Length Indicator**
- Header contains frame length field
- Receiver knows where frame ends

**C. Fixed Length**
- All frames have same predetermined size
- Simple but inflexible

**D. Silence Between Packets**
- Gap (no signal) between frames
- Used in some physical layer implementations

**Most Common:** Explicit delimiters (flags)

---

#### 2. MULTIPLEXING

**Purpose:** Support multiple higher layer protocols

**Examples:**
- IPv4, IPv6, ARP all use same Ethernet frame
- Frame header contains protocol type field
- Demultiplexes at receiver based on type

**Benefit:** Single data link can carry multiple protocol types

---

#### 3. ADDRESSING (Local)

**Purpose:** Identify source and destination on local network

**Scope:** Link-level addressing (not end-to-end)

**Examples:**
- **MAC addresses** in Ethernet (48 bits)
- **DLCI** in Frame Relay
- Local scope only (within same network segment)

**Note:** Different from network layer addressing (IP)

---

#### 4. ERROR DETECTION

**Purpose:** Detect transmission errors

**Method:** Error detection codes in frame
- **CRC (Cyclic Redundancy Check)** - most common
- Detects but does NOT correct errors
- High error detection capability

**Action on Error:**
- Discard frame
- May request retransmission (if connection-oriented)

---

#### 5. WINDOW PROTOCOL

**Purpose:** Reliable data transfer

**Two Functions:**

**A. Flow Control**
- Prevent sender from overwhelming receiver
- Receiver controls transmission rate
- Window size mechanism

**B. Sequence and Error Control**
- Through retransmission (ARQ techniques)
- Ensures ordered, reliable delivery
- Uses sequence numbers

**Protocols:** Stop-and-Wait, Go-Back-N, Selective Repeat

---

#### 6. MULTIPLE ACCESS PROTOCOLS

**Purpose:** Control access to shared media

**Needed when:** Multiple nodes share same transmission medium

**Examples:**
- CSMA/CD (Ethernet)
- Token passing (Token Ring)
- CSMA/CA (WiFi)

**Scope:** Only for shared media (not point-to-point)

---

### 📊 Exam Pattern

**Question:** "Data link layer is responsible for ___"  
**Answer:** Frame delineation, error detection, flow control, addressing (local)

**Question:** "Which layer provides error detection using CRC?"  
**Answer:** **Data Link Layer (Layer 2)**

**Question:** "MAC addressing is done at which layer?"  
**Answer:** **Data Link Layer (Layer 2)**

---

# PART 2: DATA LINK LAYER PROTOCOLS

## 🎯 SLIDES 4-7: Protocol Families and History

### HDLC Protocol Family Tree

**Origin:** SDLC (Synchronous Data Link Control) - IBM

**Standardization Path:**
```
SDLC (IBM)
    ↓
    ├→ ADCCP (ANSI standard)
    ├→ HDLC (ISO standard)
    └→ LAP (CCITT/ITU-T)
         ├→ LAP-B (Balanced)
         ├→ LAP-D (D-Channel)
         ├→ LAP-F (Frame Mode)
         └→ LAP-Dm (Mobile)
```

### HDLC Family Protocols

**1. SDLC (Synchronous Data Link Control)**
- Defined by IBM
- Original protocol
- Basis for all others

**2. HDLC (High-level Data Link Control)**
- ISO standardization of SDLC
- International standard
- Basis for many protocols

**3. LAP-B (Link Access Procedure Balanced)**
- **Used in:** X.25, ISDN
- **Status:** Obsolete (X.25 and ISDN obsolete)
- Balanced configuration (peer-to-peer)

**4. LAP-D (Link Access Procedure D-Channel)**
- **Used in:** ISDN D-channel
- **Purpose:** Signalling channel
- **Status:** Obsolete with ISDN

**5. LAP-F (Link Access Procedure Frame Mode)**
- **Used in:** Frame Relay
- **Purpose:** Frame mode bearer service
- **Status:** Still used in some legacy networks

**6. PPP (Point-to-Point Protocol)**
- **Used in:** ADSL, dial-up, serial links
- **Purpose:** Point-to-point connections
- **Status:** **Still widely used** ✓
- Modern, flexible protocol

**7. LLC 802.2 (Logical Link Control)**
- **Used in:** LANs (Ethernet, Token Ring)
- **Purpose:** Upper sublayer of Layer 2 in LANs
- **Status:** **Still in use** ✓
- Part of IEEE 802 standard

**8. LAP-Dm (LAP for Mobile D-channel)**
- **Used in:** GSM mobile networks
- **Purpose:** Mobile signalling
- **Status:** Used in 2G networks

### Active vs Obsolete Protocols

**Still in Use:**
- ✅ PPP (ADSL, serial links)
- ✅ LLC 802.2 (LANs)
- ✅ LAP-F (some Frame Relay networks)

**Obsolete:**
- ❌ LAP-B (X.25, ISDN dead)
- ❌ LAP-D (ISDN dead)

---

### ISDN (Quick Reference)

**ISDN = Integrated Services Digital Network**

**Purpose:** Digital extension of telephone network to user premises

**Channels:**
- **B-channel:** 64 kbps (Bearer - for data)
- **D-channel:** 16 or 64 kbps (Delta - for signalling)

**Multiplexing:** Time division

**Status:** Obsolete technology (replaced by DSL, fiber, mobile)

---

## 🎯 SLIDES 7-9: Public vs Private Networks

### Network Types and Layer 2 Usage

#### 1. Public Networks (Access Segment)

**Definition:** Point-to-point links from home/SOHO to network provider

**Protocols Used:**
- Derived from SDLC/HDLC
- PPP (most common for ADSL)
- LAP-B (obsolete X.25)

**Topology:** Point-to-point

**Examples:**
- Home → ISP connection (ADSL uses PPP)
- X.25 connections (obsolete)

#### 2. Private (Local) Networks

**Definition:** Interconnect devices in limited distance range

**Examples:**
- Labs, offices, home networks
- Data centers
- Campus networks

**Topology:** Mostly broadcast channel (shared medium)

**Two Sublayers of Layer 2:**

**A. LLC (Logical Link Control)**
- Upper sublayer
- Derived from SDLC
- Provides services to network layer

**B. MAC (Media Access Control)**
- Lower sublayer
- Solves multiple access problem
- Specific to LAN technology

#### 3. Public Transport Networks

**Protocols:**
- ATM (Asynchronous Transfer Mode)
- Frame Relay

**Purpose:** Backbone, high-speed transport

---

### Network Components

**DTE (Data Terminal Equipment)**
- User devices
- Computers, terminals, routers

**DCE (Data Circuit-terminating Equipment)**
- Network devices
- Modems, switches, multiplexers

**Connection:**
```
DTE ←→ DCE ←→ [NETWORK] ←→ DCE ←→ DTE
```

---

# PART 3: HDLC FRAME FORMAT

## 🎯 SLIDE 10: Frame Structure

### Standard HDLC Frame Format

```
┌──────────┬─────────┬─────────┬──────┬──────┬──────────┐
│  Flag    │ Address │ Control │ Data │ CRC  │   Flag   │
│01111110  │         │         │      │      │ 01111110 │
└──────────┴─────────┴─────────┴──────┴──────┴──────────┘
   8 bits     8 bits   8/16 bits ≥0 bits 16 bits  8 bits
```

### Field Descriptions

#### 1. FLAG (8 bits)
**Value:** 01111110 (0x7E in hex)

**Purpose:**
- Marks beginning of frame
- Marks end of frame

**Position:**
- Opening flag before frame
- Closing flag after frame

**Key Property:** Must NOT appear elsewhere in frame (data transparency issue)

#### 2. ADDRESS Field (8 bits)

**Purpose:** Identify station in multipoint configuration

**Usage:**
- Master/slave configurations
- Multipoint links
- Identify which station should respond

**Note:** Not used in point-to-point links (only 2 stations)

#### 3. CONTROL Field (8 or 16 bits)

**Purpose:** Differentiate PDU types

**Three Frame Types:**

**A. Information Frames (I-frames)**
- Carry user data
- Sequence numbers included
- Used for data transfer

**B. Supervisory Frames (S-frames)**
- Flow and error control
- ACK/NAK functions
- No user data

**C. Unnumbered Frames (U-frames)**
- Control functions
- Link setup/disconnect
- Mode setting

#### 4. DATA Field (Variable length, ≥ 0 bits)

**Content:** User data (SDU from network layer)

**Length:** Variable (can be empty for control frames)

**Multiple of:** 8 bits (byte-oriented)

#### 5. CRC Field (16 bits)

**Purpose:** Error detection

**Coverage:** Address + Control + Data fields

**Method:** CRC-16 or CRC-CCITT

**Properties:**
- Detects single and burst errors
- Very high detection probability
- Does NOT correct errors

---

### Frame Characteristics

**Protocol Type:**
- Bit/byte oriented
- Packet length must be integer multiple of 8 bits

**Data Transparency:**
- Flag 01111110 must not appear in other fields
- Ensured by bit stuffing or byte stuffing

---

### 📊 Exam Pattern

**Question:** "HDLC flag value is ___"  
**Answer:** **01111110** (0x7E)

**Question:** "HDLC uses ___ for error detection"  
**Answer:** **CRC** (16 bits)

**Question:** "Address field is used in ___ configuration"  
**Answer:** **Multipoint** (master/slave)

**Question:** "HDLC frame format: Flag, ___, ___, Data, CRC, Flag"  
**Answer:** **Address, Control**

---

# PART 4: DATA TRANSPARENCY

## 🎯 SLIDES 11-13: Bit Stuffing and Byte Stuffing

### The Problem

**Issue:** Flag pattern 01111110 must NOT appear in:
- Data field (user data)
- Other PCI fields (address, control, CRC)

**Why?** Receiver would mistake it for frame boundary

**Solution:** Stuffing techniques

---

### BIT STUFFING (Bit-Oriented Protocols)

#### How It Works

**At Transmitter:**
1. Monitor outgoing bit stream (except in flag field)
2. When detecting sequence **01111** (5 consecutive 1s)
3. Insert (stuff) a **0 bit** after it
4. Regardless of what the next bit is

**At Receiver:**
1. Monitor incoming bit stream
2. When detecting sequence **011111** (5 consecutive 1s followed by 0)
3. Remove (de-stuff) the 0 bit
4. Continue processing

#### Example

**Original Data:**
```
0111111
```

**After Bit Stuffing:**
```
01111101  (0 stuffed after 5 ones)
```

**Another Example:**
```
Original:  011111110  
Stuffed:   0111110110  (0 stuffed after each sequence of 5 ones)
```

#### When Used

**Transmission Type:** Synchronous transmission

**Protocol Type:** Bit-oriented protocols

**Examples:** HDLC, SDLC, LAP-B

#### Key Points

✅ Works at bit level  
✅ Transparent to upper layers  
✅ Automatic (hardware/firmware)  
✅ Small overhead (only when needed)  
❌ Cannot be used with byte-oriented transmission

---

### BYTE STUFFING (Byte-Oriented Protocols)

#### How It Works

**Escape Byte:** 01111101 (0x7D)

**At Transmitter:**
1. Scan frame byte by byte (except in flag field)
2. When finding **01111110** (flag) → Insert 01111101 before it
3. When finding **01111101** (escape) → Insert 01111101 before it

**At Receiver:**
1. Scan incoming bytes
2. When finding 01111101 (escape)
3. Always discard the first 01111101
4. Keep the next byte as data

#### Example

**Original Data Contains Flag:**
```
Data: ... 01111110 ...
```

**After Byte Stuffing:**
```
Stuffed: ... 01111101 01111110 ...
         (escape inserted before flag)
```

**Original Data Contains Escape:**
```
Data: ... 01111101 ...
```

**After Byte Stuffing:**
```
Stuffed: ... 01111101 01111101 ...
         (escape inserted before escape)
```

#### When Used

**Transmission Type:** Asynchronous transmission

**Protocol Type:** Byte-oriented protocols

**Examples:** PPP, some legacy protocols

#### Key Points

✅ Works at byte level  
✅ Simpler logic than bit stuffing  
✅ Good for byte-oriented systems  
❌ More overhead than bit stuffing (whole byte)  
❌ Only for asynchronous transmission

---

### Bit Stuffing vs Byte Stuffing Comparison

| Feature | Bit Stuffing | Byte Stuffing |
|---------|--------------|---------------|
| **Works On** | Individual bits | Whole bytes |
| **Escape** | Insert 0 after 5 ones | Insert 01111101 byte |
| **Overhead** | 1 bit when needed | 8 bits (1 byte) |
| **Transmission** | Synchronous | Asynchronous |
| **Protocol Type** | Bit-oriented | Byte-oriented |
| **Examples** | HDLC, LAP-B | PPP |
| **Complexity** | Higher | Lower |
| **Efficiency** | Better | Lower (more overhead) |

---

### 📊 Exam Pattern

**Question:** "Bit stuffing inserts ___ after detecting 5 consecutive 1s"  
**Answer:** **0 (zero bit)**

**Question:** "Byte stuffing inserts ___ before flag or escape bytes"  
**Answer:** **01111101 (escape byte)**

**Question:** "Bit stuffing is used for ___ transmission"  
**Answer:** **Synchronous transmission**

**Question:** "Byte stuffing is used for ___ transmission"  
**Answer:** **Asynchronous transmission**

**Question:** "Purpose of stuffing techniques?"  
**Answer:** **Ensure data transparency** / **Prevent flag appearing in data**

---

# SUMMARY: EXAM-CRITICAL POINTS FOR CHAPTER 5

## 🎯 MUST MEMORIZE

### Data Link Layer Functions (All 6)

1. **Frame Delineation** - Identify frame boundaries
2. **Multiplexing** - Support multiple protocols
3. **Addressing (local)** - Link-level addressing (MAC)
4. **Error Detection** - CRC for error checking
5. **Window Protocol** - Flow + error control via retransmission
6. **Multiple Access** - Control shared media access

**Mnemonic:** "FMAEWM" or "Frames Must Always Ensure Window Management"

---

### HDLC Protocol Family

**Origin:** SDLC (IBM) → HDLC (ISO)

**Key Protocols:**

| Protocol | Full Name | Used In | Status |
|----------|-----------|---------|--------|
| **PPP** | Point-to-Point Protocol | **ADSL, Serial** | ✅ **Active** |
| **LLC 802.2** | Logical Link Control | **LANs** | ✅ **Active** |
| LAP-B | LAP Balanced | X.25, ISDN | ❌ Obsolete |
| LAP-D | LAP D-Channel | ISDN signalling | ❌ Obsolete |
| LAP-F | LAP Frame Mode | Frame Relay | △ Legacy |

---

### HDLC Frame Format (Must Know!)

```
Flag (01111110) - Address (8) - Control (8/16) - Data (≥0) - CRC (16) - Flag (01111110)
```

**Key Values:**
- **Flag:** 01111110 (0x7E)
- **CRC Size:** 16 bits
- **Address:** 8 bits (multipoint)
- **Control:** 8 or 16 bits (frame type)

---

### Stuffing Techniques

| Aspect | Bit Stuffing | Byte Stuffing |
|--------|--------------|---------------|
| **Insert** | 0 after 5 ones | 01111101 before flag/escape |
| **Remove** | 0 after 5 ones | First 01111101 |
| **Used For** | Synchronous | Asynchronous |
| **Protocol** | HDLC, LAP-B | PPP |
| **Overhead** | 1 bit | 8 bits (1 byte) |

**Critical:** Bit stuffing inserts **0** after **5 consecutive 1s** (01111 → 011110)

---

### Network Types and Protocols

**Public Access Networks:**
- Point-to-point
- Uses: PPP, LAP-B
- Example: ADSL connection

**Private/Local Networks:**
- Broadcast/shared medium
- Uses: LLC + MAC sublayers
- Example: Ethernet LAN

**Transport Networks:**
- Backbone
- Uses: ATM, Frame Relay

---

## ⚠️ COMMON EXAM TRAPS

### Trap 1: Layer Confusion
**WRONG:** "Error correction done at data link layer"  
**RIGHT:** "Error **detection** at data link; correction at transport or application" ✓

### Trap 2: Flag Value
**WRONG:** "HDLC flag is 10000001"  
**RIGHT:** "HDLC flag is 01111110" ✓

### Trap 3: Bit Stuffing Insert
**WRONG:** "Bit stuffing inserts 1 after 5 ones"  
**RIGHT:** "Bit stuffing inserts **0** after 5 ones" ✓

### Trap 4: Stuffing Type
**WRONG:** "Bit stuffing for asynchronous transmission"  
**RIGHT:** "Bit stuffing for **synchronous**; byte stuffing for asynchronous" ✓

### Trap 5: PPP Status
**WRONG:** "PPP is obsolete like LAP-B"  
**RIGHT:** "PPP still widely used (ADSL, serial links)" ✓

### Trap 6: MAC vs LLC
**WRONG:** "MAC is upper sublayer of Layer 2"  
**RIGHT:** "**LLC is upper**, MAC is lower sublayer" ✓

### Trap 7: Address Field Purpose
**WRONG:** "Address field for end-to-end addressing"  
**RIGHT:** "Address field for **multipoint/local** addressing only" ✓

---

## 📊 EXAM WEIGHT DISTRIBUTION

### CRITICAL (Study exhaustively - 60%):
- ✅ Six data link layer functions
- ✅ HDLC flag value (01111110)
- ✅ Bit stuffing (insert 0 after 5 ones)
- ✅ Byte stuffing (escape byte 01111101)
- ✅ Frame format (Flag-Address-Control-Data-CRC-Flag)
- ✅ PPP vs LAP-B (active vs obsolete)

### HIGH (Study thoroughly - 30%):
- HDLC protocol family tree
- Bit stuffing vs byte stuffing comparison
- Public vs private networks
- LLC vs MAC sublayers
- CRC for error detection
- Multipoint configuration

### MEDIUM (Understand well - 10%):
- ISDN overview (obsolete)
- X.25 reference (obsolete)
- Frame types (I, S, U)
- DTE vs DCE
- Transport network protocols

---

## 🎓 STUDY STRATEGY

### Day 1: Functions and Protocols
- Learn all 6 data link layer functions
- HDLC protocol family tree
- Active vs obsolete protocols
- PPP usage (ADSL)

### Day 2: Frame Format
- HDLC frame structure
- Flag value (01111110)
- Field purposes and sizes
- CRC error detection

### Day 3: Data Transparency
- Bit stuffing mechanism
- Byte stuffing mechanism
- When each is used
- Practice examples

### Day 4: Network Types
- Public vs private networks
- LLC and MAC sublayers
- Point-to-point vs broadcast
- Protocol usage by network type

### Day 5: Review and Practice
- All common traps
- Flashcard drill
- Frame format drawing
- Stuffing examples

---

## 📝 QUICK REFERENCE FLASHCARDS

**Q:** Data link layer functions? (name 3)  
**A:** Frame delineation, error detection, flow control, addressing, multiplexing, multiple access

**Q:** HDLC flag value?  
**A:** 01111110

**Q:** Bit stuffing inserts what after 5 ones?  
**A:** 0 (zero bit)

**Q:** Escape byte in byte stuffing?  
**A:** 01111101

**Q:** Bit stuffing for which transmission?  
**A:** Synchronous

**Q:** Byte stuffing for which transmission?  
**A:** Asynchronous

**Q:** PPP used for?  
**A:** ADSL, point-to-point serial links

**Q:** LAP-B status?  
**A:** Obsolete (X.25 dead)

**Q:** HDLC frame: Flag, ___, ___, Data, ___, Flag  
**A:** Address, Control, CRC

**Q:** CRC size in HDLC?  
**A:** 16 bits

**Q:** Error detection method?  
**A:** CRC (Cyclic Redundancy Check)

**Q:** MAC sublayer: upper or lower?  
**A:** Lower (LLC is upper)

**Q:** Address field used in which config?  
**A:** Multipoint (master/slave)

**Q:** Two sublayers of Layer 2 in LANs?  
**A:** LLC (upper) and MAC (lower)

**Q:** Protocol family origin?  
**A:** SDLC (IBM)

---

**END OF CHAPTER 5: DATA LINK LAYER**

**Status:** ✅ Complete - Ready for exam preparation  
**Importance:** ⭐⭐½ MEDIUM-HIGH PRIORITY - 10-15% of exam  
**Next Chapter:** LAN and LAN Version 2

