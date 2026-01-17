# CHAPTER 3: WINDOW PROTOCOLS (ARQ TECHNIQUES)
## Exam-Oriented Study Guide

**Based on:** Professor's lecture slides (Window protocols slides 1-70)  
**Exam Weight:** High (⭐⭐⭐) - Approximately 10-15% of exam questions  
**Study Priority:** HIGH - Important for understanding reliable data transfer

---

## 📋 CHAPTER OVERVIEW

This chapter covers **Automatic Repeat reQuest (ARQ)** techniques used for reliable data transmission. These protocols ensure data is delivered correctly even when errors occur.

**Main Topics:**
1. Error Control Techniques (FEC vs ARQ)
2. Block Codes and Error Detection
3. Stop-and-Wait ARQ (Alternating Bit Protocol)
4. Go-Back-N ARQ
5. Selective Repeat ARQ
6. Window Protocols and Throughput

---

# PART 1: ERROR CONTROL FUNDAMENTALS

## 🎯 SLIDES 3-11: Error Protection Techniques

### Two Main Approaches

#### 1. FEC (Forward Error Correction)
**Method:** Try to **correct** errors at the receiver

**Characteristics:**
- Receiver corrects errors without retransmission
- Requires **more redundant bits** (correction harder than detection)
- Used when retransmission is expensive or impossible

**Examples:**
- Satellite communications
- Real-time streaming
- Deep space communications

#### 2. ARQ (Automatic Retransmission reQuest)
**Method:** **Detect** errors at receiver, request retransmission

**Characteristics:**
- Receiver detects errors and asks transmitter to retransmit
- Requires **fewer redundant bits** (detection easier than correction)
- Most common in data networks

**Process:**
1. Receiver detects error in PDU
2. Receiver requests retransmission
3. Transmitter sends PDU again

**Examples:**
- TCP protocol
- Data link layer protocols
- Most reliable protocols

### Key Comparisons

| Feature | FEC | ARQ |
|---------|-----|-----|
| **Action** | Correct errors | Detect and retransmit |
| **Redundancy** | High (more bits needed) | Lower (fewer bits) |
| **Complexity** | Higher at receiver | Higher at transmitter |
| **Delay** | No retransmission delay | Retransmission adds delay |
| **Use Case** | One-way, real-time | Two-way, reliable transfer |

**Both techniques:**
- Need additional bits in packet header
- Have limited capability (too many errors → failure)

### 📊 Exam Pattern

**Question:** "ARQ tries to ___ errors at the receiver"  
**Answer:** **Detect** (NOT correct!)

**Question:** "Which requires more bits: FEC or ARQ?"  
**Answer:** **FEC** (correction requires more info than detection)

---

## 🎯 SLIDES 4-11: Block Codes for Error Control

### Block Code Structure

**n-bit codeword:**
- **k bits:** User data
- **(n-k) bits:** Parity/redundancy bits

**Total possible combinations:** 2^n  
**Valid codewords:** 2^k (only subset are valid)

### Common Error Detection Codes

#### 1. Parity Bit
**How it works:**
- Add 1 bit to make number of 1s even (or odd)
- **Detects:** Odd number of bit errors
- **Limitation:** Cannot detect even number of errors

**Example:**
```
Data: 01101010
Even parity: 01101010 0 (already even number of 1s)
Data: 01001010  
Even parity: 01001010 1 (adds 1 to make even)
```

#### 2. Repetition Code
**How it works:**
- Send each bit multiple times (e.g., 3 times)
- Use **majority decision** at receiver
- **Error correction possible**

**Example:**
```
Data bit: 1
Transmitted: 1 1 1
Received: 1 0 1 (one error)
Decision: Majority says 1 ✓
```

**Drawback:** Requires much more overhead

#### 3. Row and Column Parity
**How it works:**
- Arrange bits in matrix
- Add parity for each row AND each column
- **Can correct single bit errors**
- Can detect (not always correct) multiple bit errors

**Overhead:** More than single parity, less than repetition

#### 4. CRC (Cyclic Redundancy Check)
**How it works:**
- Polynomial division mathematics
- **Classical example** of parity bits in networking
- Very good error detection capability

**Usage:** Most common in data link layer (Ethernet, WiFi, etc.)

**Location:** Parity bits in PDU header (PCI)

### 📊 Exam Pattern

**Question:** "Parity bit detects errors in ___ number"  
**Answer:** **Odd number** (cannot detect even number of errors)

**Question:** "Classical example of parity bit in networks?"  
**Answer:** **CRC (Cyclic Redundancy Check)**

---

# PART 2: ARQ FUNDAMENTALS

## 🎯 SLIDES 12-15: ARQ Basics

### What ARQ Controls

**ARQ provides joint control over:**
1. **Error** (losses) - Detect lost or corrupted PDUs
2. **Sequence** - Maintain order of PDUs
3. **Flow** - Prevent overwhelming receiver

### Basic ARQ Concept

**Core Idea:** 
1. Send a packet
2. Wait for confirmation (ACK - Acknowledgement)
3. If no ACK received within timeout → retransmit

### PDU Structure for ARQ

**Data Packet Header (PCI):**
- **Parity bits:** Error control over data AND header
- **N(T):** Transmitted packet number (sequence number)
- **Addresses:** Source and destination

**ACK Packet Header:**
- **Parity bits:** Error control over header only
- **N(R):** Next expected packet number
- **Addresses:** Source and destination

### Variables Used

**At Transmitter:**
- **V(T):** Value of next PDU to transmit (send sequence number)

**At Receiver:**
- **V(R):** Value of next PDU expected to receive (receive sequence number)

### Three ARQ Flavors

1. **Stop-and-Wait** (Alternating Bit)
2. **Go-Back-N**
3. **Selective Repeat**

**Focus:** Primarily on unidirectional communication (one-way data flow)

---

# PART 3: STOP-AND-WAIT ARQ

## 🎯 SLIDES 16-48: Stop-and-Wait Protocol

### How Stop-and-Wait Works

#### Transmitter Behavior

**Step 1:** Transmission
1. Make copy of PDU (for possible retransmission)
2. Store in TX buffer
3. Send the PDU with N(T) = V(T)
4. Start timer (timeout)
5. Wait for ACK

**Step 2:** On Timeout (before ACK)
1. Timeout expires
2. Retransmit the PDU
3. Restart timer

**Step 3:** On ACK Reception
1. Check ACK correctness (parity)
2. Check sequence number: N(R) = V(T) + 1?
3. If correct:
   - Stop timer
   - Erase PDU copy from buffer
   - Increment V(T)
   - Ready for next PDU
4. If incorrect:
   - Ignore ACK
   - Wait for timeout

#### Receiver Behavior

**On PDU Reception:**
1. Check PDU correctness (parity)
2. If correct (regardless of sequence): Send ACK
3. Check sequence number: N(T) = V(R)?
4. If expected:
   - Move PDU to higher layer
   - Increment V(R)
5. Send ACK with N(R) = V(R)

### Initialization

**At Connection Setup:**
- **V(T) = 0** at transmitter
- **V(R) = 0** at receiver
- TX and RX agree on protocol parameters

### Normal Operation Example

```
TX Side          RX Side
V(T)=0           V(R)=0
  |                |
  |--N(T)=0 SDU--->|  Send PDU 0
  |                |  Receive, check, V(R)=0? Yes
  |                |  V(R) becomes 1
  |<---N(R)=1------|  Send ACK expecting 1
  |                |
V(T)=1           V(R)=1  Ready for next
  |                |
  |--N(T)=1 SDU--->|  Send PDU 1
  |                |
```

### Alternating Bit Protocol

**Special Case:** Use only **1 bit** for numbering

**Sequence:** 0, 1, 0, 1, 0, 1, ...

**Name:** "Alternating Bit" because bit alternates between 0 and 1

**Advantage:** Minimal overhead (just 1 bit)

**Example:**
```
V(T): 0 → 0 → 1 → 1 → 0 → 0 → 1 → 1 ...
N(T): 0       1       0       1
N(R):     1       0       1       0
V(R): 0 → 1 → 1 → 0 → 0 → 1 → 1 → 0
```

### Error Scenarios

#### Scenario 1: PDU Loss (Transmission Error)

```
TX              RX
V(T)=0          V(R)=0
  |               |
  |--N(T)=0-X     |  PDU lost/corrupted
  |               |  No ACK sent
  |  (timeout)    |
  |--N(T)=0------>|  Retransmit
  |               |  Received correctly
  |<--N(R)=1------|  ACK sent
V(T)=1          V(R)=1
```

**Key Point:** Timeout value setting is **critical**

#### Scenario 2: ACK Loss

```
TX              RX
V(T)=0          V(R)=0
  |               |
  |--N(T)=0------>|  PDU received
  |               |  V(R)=1
  |      X--N(R)=1|  ACK lost
  |  (timeout)    |
  |--N(T)=0------>|  Retransmit (duplicate)
  |               |  Already have it, but ACK again
  |<--N(R)=1------|  Send ACK
V(T)=1          V(R)=1
```

**Key Point:** Need sequence numbers to detect duplicates!

### Non-Sequential Channel Problem

**Problem:** If channel can reorder packets, alternating bit (1-bit numbering) may fail

**Example of Failure:**
- Old PDU 0 delayed in network
- New PDU 0 sent and ACKed
- Old PDU 0 arrives later
- Receiver cannot distinguish old from new (both numbered 0)

**Solution:** Use more bits for numbering

**Modulo-4 Numbering Example:**
- Use 2 bits: 0, 1, 2, 3, 0, 1, 2, 3, ...
- Better distinguishes old vs new packets
- But still can have problems with very delayed packets

**General Rule:** 
- More bits → Better handling of delays
- Add maximum lifetime for PDUs
- Prevents very old packets from causing confusion

### 📊 Exam Pattern

**Question:** "Stop-and-Wait sends ___ PDU per cycle"  
**Answer:** **One** (that's why it's called "stop and wait")

**Question:** "Alternating bit protocol uses ___ bit(s) for numbering"  
**Answer:** **1 bit** (alternates 0, 1, 0, 1...)

**Question:** "Why is PDU numbering needed?"  
**Answer:** **To detect duplicates** (otherwise duplicate PDUs not detected)

**Question:** "What is RTT?"  
**Answer:** **Round Trip Time** (cycle duration for one PDU)

### ⚠️ Common Exam Traps

**TRAP:** "Stop-and-wait can send multiple PDUs before waiting"  
**WRONG!** It sends ONE PDU then waits (that's the definition)

**TRAP:** "Alternating bit uses 2 bits"  
**WRONG!** Alternating bit uses 1 bit (values: 0, 1)

**TRAP:** "Non-sequential channel is always OK with alternating bit"  
**WRONG!** Alternating bit can fail on non-sequential channels

---

# PART 4: GO-BACK-N ARQ

## 🎯 SLIDES 49-60: Go-Back-N Protocol

### Motivation

**Problem with Stop-and-Wait:**
- Sends only 1 packet per RTT
- If RTT is large → throughput limited
- Channel underutilized

**Solution: Go-Back-N**
- Transmitter can send up to **N PDUs** before waiting for ACK
- Increases throughput
- Better channel utilization

### Transmission Window (WT)

**Definition:** Maximum number of PDUs that can be transmitted in sequence without receiving any ACK

**Determined by:**
- Buffer space at transmitter
- Network capacity
- Protocol design

**Also represents:** Maximum number of PDUs/ACKs in flight (propagating in network) at any time

**Visualization:**
```
┌──────────────┬───────────┬────────────┬──────────────┐
│  Correctly   │   PDUs    │    PDUs    │    PDUs      │
│   ACKed      │  waiting  │  that can  │  that cannot │
│   PDUs       │  for ACK  │    be TX   │   be TX      │
└──────────────┴───────────┴────────────┴──────────────┘
                    WT = N
              ^
              n (current position)
```

### Receiver Window (WR)

**Definition:** Sequence of PDUs that receiver is willing to store

**In Go-Back-N:** WR = **1** (receiver window size is ONE)

**Meaning:** Receiver only accepts the NEXT expected PDU (in sequence)

**Visualization:**
```
┌──────────────┬──────────┬─────────────────────┐
│  Correctly   │ Expected │  Out-of-sequence    │
│   ACKed      │   PDU    │  PDUs (cannot       │
│   PDUs       │  (only)  │   be accepted)      │
└──────────────┴──────────┴─────────────────────┘
              ^
              n
         WR = 1
```

**Key Point:** Out-of-sequence PDUs are **rejected** (not buffered)

### Go-Back-N Transmitter Behavior

**Operation:**
1. Send up to N = WT PDUs in sequence
2. Store copy of each in TX memory
3. Start timer (usually one timer per window)
   - Timer reset at any PDU transmission
4. Wait for ACK reception
5. For each received in-sequence ACK:
   - Move TX window forward by number of acknowledged packets
6. **If timeout before ACK:**
   - Retransmit **ALL PDUs** that haven't been ACKed
   - **"Go back"** by N positions (hence the name!)

### Go-Back-N Receiver Behavior

**On PDU Reception:**
1. Check PDU correctness (parity)
2. If correct: Send ACK
3. Check sequence number
4. **If sequence number is expected (first PDU not yet received):**
   - Move PDU to higher layer
   - Process it
5. **If sequence number is NOT expected:**
   - Discard PDU (no buffering!)
   - Send ACK for last correctly received PDU (duplicate ACK)

**Key Point:** Receiver does NOT buffer out-of-sequence PDUs

### ACK Semantics (IMPORTANT!)

#### 1. Selective ACK
**Meaning:** ACK(n) = "PDU n received"  
**Acknowledges:** Single specific PDU

#### 2. Cumulative ACK (Used in Go-Back-N)
**Meaning:** ACK(n) = "All PDUs up to n received"  
**Acknowledges:** PDU n and ALL previous PDUs  
**Generates:** Duplicate ACKs if packet lost

**Example:**
```
Received PDUs: 5, 6, 8 (7 missing)
With Cumulative ACK:
- After PDU 5: Send ACK 6 (expect 6 next)
- After PDU 6: Send ACK 7 (expect 7 next)
- After PDU 8: Send ACK 7 again (still expect 7, haven't gotten it)
```

#### 3. Negative ACK (NAK)
**Meaning:** NAK(n) = "Retransmit PDU n"  
**Explicitly requests:** Specific lost packet

**Comparison Table:**

| ACK Type | Example | Meaning |
|----------|---------|---------|
| Cumulative | ACK 7 | All PDUs up to 6 received, expect 7 |
| Selective | ACK 5 | PDU 5 received |
| Negative | NAK 7 | PDU 7 missing, please resend |

**Important:** TX and RX must **agree** on ACK semantic

### Piggybacking

**Definition:** Include ACK number on PDU header traveling in opposite direction

**Used for:** Bidirectional flows

**Advantage:** Reduces number of ACK packets
- ACKs are packets with no data (only control)
- Piggybacking adds ACK to data packet

**Example:**
```
A → B: PDU(data) + ACK(for B's previous data)
B → A: PDU(data) + ACK(for A's previous data)
```

### PDU Numbering in Go-Back-N

**Numbering is cyclic:** Modulo 2^k (where k = number of bits)

**Example with k=3 bits:**
- Sequence: 0, 1, 2, 3, 4, 5, 6, 7, 0, 1, 2, 3, ...
- Modulo 8 numbering

**Constraint:** WT < 2^k

**Why?** To avoid ambiguity when numbers wrap around

**Example:**
```
k = 3 bits → modulo 8 numbering
If WT = 3, WR = 1:

  7    0
   \  /
6 -  - 1
   /  \
  5    2
     3  4

Numbers wrap around after 7 → 0
```

### Go-Back-N Complexity

**Transmitter:**
- **More complex** than Stop-and-Wait
- More memory needed (buffer N PDUs)
- Timer management more complex
- PDU numbering more difficult

**Receiver:**
- **Same as Stop-and-Wait** (WR = 1)
- Simple: accept only next expected PDU

**Benefit:**
- Can group ACKs (cumulative meaning)
- One ACK for several PDUs
- May need receiver timer to send delayed ACK

### 📊 Exam Pattern

**Question:** "Go-Back-N can send up to ___ PDUs before stopping"  
**Answer:** **N** (or WT - window size)

**Question:** "In Go-Back-N, receiver window size is ___"  
**Answer:** **1** (only accepts next expected PDU)

**Question:** "On timeout, Go-Back-N retransmits ___"  
**Answer:** **All unacknowledged PDUs** (goes back N)

**Question:** "Cumulative ACK(n) means ___"  
**Answer:** **All PDUs up to n received** (not just PDU n)

**Question:** "Go-Back-N uses ___ ACK semantic"  
**Answer:** **Cumulative** ACK

### ⚠️ Common Exam Traps

**TRAP:** "Go-Back-N receiver buffers out-of-sequence PDUs"  
**WRONG!** Receiver discards out-of-sequence PDUs (WR=1)

**TRAP:** "On timeout, only retransmit lost PDU"  
**WRONG!** Retransmit ALL unacknowledged PDUs (go back N)

**TRAP:** "Go-Back-N receiver is more complex than Stop-and-Wait"  
**WRONG!** Receiver is the same (WR=1 in both)

**TRAP:** "Selective ACK means all PDUs up to n"  
**WRONG!** That's cumulative ACK. Selective means only PDU n.

---

# PART 5: SELECTIVE REPEAT ARQ

## 🎯 SLIDES 61-68: Selective Repeat Protocol

### Motivation

**Problem with Go-Back-N:**
- Retransmits ALL unacknowledged PDUs on timeout
- Wastes bandwidth retransmitting PDUs that were correctly received
- Inefficient when errors are rare

**Solution: Selective Repeat**
- **Only retransmit** the specific PDUs that were lost/corrupted
- Receiver buffers out-of-sequence PDUs
- More efficient use of bandwidth

### Key Difference: Receiver Window > 1

**Definition:** Selective Repeat has receiver window **WR > 1**

**Meaning:** Receiver can accept and buffer out-of-sequence PDUs

**Receiver Window Visualization:**
```
┌─────────────┬────────────┬────────────────────┐
│  Correctly  │  Received  │  Out-of-sequence   │
│  ACKed and  │  PDUs      │  PDUs that CAN     │
│  moved to   │  waiting   │  be accepted       │
│  higher     │  for gaps  │  (buffered)        │
│  layer      │  to fill   │                    │
└─────────────┴────────────┴────────────────────┘
         ^           WR = N
         n
```

### Selective Repeat Transmitter Behavior

**Operation:**
1. Send up to N = WT PDUs
2. Store copy in TX memory
3. Start timer (reset at any PDU transmission)
4. Wait for ACK reception
5. **On timeout:**
   - Retransmit **ONLY** PDUs that have not been correctly ACKed
   - (NOT all PDUs like Go-Back-N)

**Key Difference from Go-Back-N:** Selective retransmission only

### Selective Repeat Receiver Behavior

**On PDU Reception:**
1. Check PDU correctness
2. If correct: Send ACK (often selective ACK)
3. Check sequence number
4. **If in receiver window range:**
   - Buffer the PDU (even if out of sequence)
   - Wait for missing PDUs to fill gaps
5. **When gap is filled:**
   - Deliver all consecutive PDUs to higher layer
   - Advance window

**Key Difference from Go-Back-N:** Buffers out-of-sequence PDUs

### Advantages vs Go-Back-N

**Selective Repeat Advantages:**
- ✅ More efficient (only retransmit lost PDUs)
- ✅ Better throughput (especially with high error rates)
- ✅ Less wasted bandwidth

**Selective Repeat Disadvantages:**
- ❌ More complex receiver (needs buffering)
- ❌ More memory required at receiver
- ❌ More complex ACK management

### Window Size Constraints

**For Selective Repeat:**
- **Constraint:** WT + WR ≤ 2^k
- Where k = number of bits for sequence numbers

**Why?** To prevent ambiguity when windows wrap around

**Common Configuration:**
- WT = WR = 2^(k-1)
- Example: k=3 bits → WT = WR = 4

### Error Scenario Example

**Comparison of Go-Back-N vs Selective Repeat:**

**Scenario:** PDUs 0,1,2,3,4 sent; PDU 2 lost

**Go-Back-N:**
```
TX: Send 0,1,2,3,4
RX: Receive 0,1,X,3,4 (2 lost, discard 3,4)
    ACK: 0, 1, 1, 1, 1 (duplicate ACKs)
TX: Timeout → Resend 2,3,4 (even though 3,4 were OK)
```

**Selective Repeat:**
```
TX: Send 0,1,2,3,4
RX: Receive 0,1,X,3,4 (2 lost, buffer 3,4)
    ACK: 0, 1, NAK 2, 3, 4
TX: Resend only 2 (selective retransmission)
RX: Receive 2, now have 0,1,2,3,4 complete
```

**Result:** Selective Repeat retransmits less data

### 📊 Exam Pattern

**Question:** "Selective Repeat receiver window size is ___"  
**Answer:** **Greater than 1** (WR > 1)

**Question:** "On timeout, Selective Repeat retransmits ___"  
**Answer:** **Only lost/unacknowledged PDUs** (NOT all)

**Question:** "Selective Repeat receiver ___ out-of-sequence PDUs"  
**Answer:** **Buffers** (unlike Go-Back-N which discards)

**Question:** "Which is more efficient: Go-Back-N or Selective Repeat?"  
**Answer:** **Selective Repeat** (retransmits less)

### ⚠️ Common Exam Traps

**TRAP:** "Selective Repeat retransmits all unacknowledged PDUs"  
**WRONG!** Only retransmits specifically lost PDUs (selective!)

**TRAP:** "Selective Repeat receiver window = 1"  
**WRONG!** WR > 1 (that's the defining characteristic)

**TRAP:** "Go-Back-N is more efficient than Selective Repeat"  
**WRONG!** Selective Repeat is more efficient (but more complex)

---

# PART 6: WINDOW PROTOCOL THROUGHPUT

## 🎯 SLIDES 69-70: Performance Analysis

### Throughput Formula

**In absence of errors:**

```
Throughput = min( transmission_window/RTT , link_speed )
```

**Key Insights:**

1. **Optimal Window Size:**
   - For given RTT, there is optimal window size that maximizes throughput
   - Window_optimal ≈ RTT × link_speed

2. **Window Too Small:**
   - Throughput limited by: window/RTT
   - Channel underutilized

3. **Window Too Large:**
   - No throughput benefit beyond optimal
   - Acts like fictitious RTT increase
   - More buffer memory needed

4. **Short Connections:**
   - Get higher throughput for same window size
   - Less overhead per data transferred

### Throughput Control Methods

**To control TX throughput, can act on:**

1. **RTT (delay ACK transmission)**
   - Longer wait before sending ACK
   - Effective but may induce unnecessary retransmissions
   - Must be careful with timeout values

2. **Window Size**
   - Reduce window → reduce throughput
   - Most common method
   - Example: TCP flow control

### 📊 Exam Pattern

**Question:** "Window protocol throughput depends on ___"  
**Answer:** **Window size and RTT** (and link speed)

**Question:** "Larger windows beyond optimal ___"  
**Answer:** **Don't increase throughput** (wasteful)

---

# SUMMARY: EXAM-CRITICAL POINTS FOR CHAPTER 3

## 🎯 MUST MEMORIZE

### Error Control Techniques

| Technique | Action | Bits Needed | Use Case |
|-----------|--------|-------------|----------|
| **FEC** | Correct errors | More | One-way, real-time |
| **ARQ** | Detect + retransmit | Fewer | Two-way, reliable |

### Three ARQ Protocols Comparison

| Feature | Stop-and-Wait | Go-Back-N | Selective Repeat |
|---------|---------------|-----------|------------------|
| **PDUs per cycle** | 1 | Up to N | Up to N |
| **TX window (WT)** | 1 | N | N |
| **RX window (WR)** | 1 | 1 | > 1 |
| **On timeout** | Resend 1 PDU | Resend all N | Resend only lost |
| **RX buffers out-of-seq?** | No | No | Yes |
| **Efficiency** | Low | Medium | High |
| **Complexity** | Low | Medium | High |
| **ACK type** | Simple | Cumulative | Selective/Cumulative |

### Key Numbers to Remember

**Alternating Bit:**
- Uses **1 bit** for numbering
- Sequence: 0, 1, 0, 1, ...
- Simplest form of Stop-and-Wait

**Modulo Numbering:**
- k bits → modulo 2^k
- Example: 3 bits → modulo 8 (0-7)

**Window Constraints:**
- **Go-Back-N:** WT < 2^k
- **Selective Repeat:** WT + WR ≤ 2^k

### ACK Semantics

**Cumulative:** ACK(n) = "All PDUs up to n received"  
**Selective:** ACK(n) = "PDU n received"  
**Negative:** NAK(n) = "Retransmit PDU n"

### Variables

**V(T):** Next PDU to transmit (at sender)  
**V(R):** Next PDU expected (at receiver)  
**N(T):** Transmitted PDU number (in packet)  
**N(R):** Next expected PDU number (in ACK)

---

## ⚠️ COMMON EXAM TRAPS

### Trap 1: FEC vs ARQ
**WRONG:** "ARQ corrects errors at receiver"  
**RIGHT:** "ARQ detects errors; FEC corrects errors" ✓

### Trap 2: Stop-and-Wait Window
**WRONG:** "Stop-and-Wait can send N PDUs"  
**RIGHT:** "Stop-and-Wait sends 1 PDU per cycle" ✓

### Trap 3: Go-Back-N Retransmission
**WRONG:** "Go-Back-N retransmits only lost PDU"  
**RIGHT:** "Go-Back-N retransmits all unacknowledged PDUs" ✓

### Trap 4: Receiver Window
**WRONG:** "Go-Back-N receiver window > 1"  
**RIGHT:** "Go-Back-N receiver window = 1; Selective Repeat > 1" ✓

### Trap 5: ACK Semantics
**WRONG:** "Cumulative ACK acknowledges only one PDU"  
**RIGHT:** "Cumulative ACK acknowledges all PDUs up to n" ✓

### Trap 6: Selective Repeat Efficiency
**WRONG:** "Go-Back-N more efficient than Selective Repeat"  
**RIGHT:** "Selective Repeat more efficient (fewer retransmissions)" ✓

### Trap 7: Numbering Bits
**WRONG:** "Alternating bit uses 2 bits"  
**RIGHT:** "Alternating bit uses 1 bit" ✓

### Trap 8: Out-of-Sequence Handling
**WRONG:** "Go-Back-N buffers out-of-sequence PDUs"  
**RIGHT:** "Go-Back-N discards; Selective Repeat buffers" ✓

---

## 📊 EXAM WEIGHT DISTRIBUTION

### CRITICAL (Study exhaustively - 60%):
- ✅ Three ARQ types and differences
- ✅ Stop-and-Wait operation
- ✅ Go-Back-N operation and WR=1
- ✅ Selective Repeat operation and WR>1
- ✅ On timeout: what each protocol does
- ✅ Cumulative vs Selective ACK

### HIGH (Study thoroughly - 30%):
- FEC vs ARQ differences
- Alternating bit protocol (1 bit)
- Why PDU numbering needed (detect duplicates)
- Window size constraints
- ACK semantics (cumulative, selective, negative)

### MEDIUM (Understand well - 10%):
- Error detection codes (parity, CRC)
- Piggybacking concept
- Throughput formula
- Non-sequential channel problems

---

## 🎓 STUDY STRATEGY

### Day 1: Error Control Basics
- FEC vs ARQ
- Error detection codes
- ARQ fundamentals

### Day 2: Stop-and-Wait
- Protocol operation
- Alternating bit
- Error scenarios
- Why numbering needed

### Day 3: Go-Back-N
- How it differs from Stop-and-Wait
- Transmission and receiver windows
- Cumulative ACK
- Retransmission on timeout

### Day 4: Selective Repeat
- How it differs from Go-Back-N
- Receiver buffering (WR > 1)
- Selective retransmission
- Efficiency comparison

### Day 5: Practice & Review
- Compare all three protocols
- Practice error scenarios
- Review common traps
- Quick reference flashcards

---

## 📝 QUICK REFERENCE FLASHCARDS

**Q:** ARQ does what with errors?  
**A:** Detects (FEC corrects)

**Q:** Stop-and-Wait sends how many PDUs?  
**A:** 1 per cycle

**Q:** Alternating bit uses how many bits?  
**A:** 1 bit (0, 1, 0, 1...)

**Q:** Go-Back-N receiver window size?  
**A:** WR = 1

**Q:** Go-Back-N on timeout retransmits?  
**A:** All unacknowledged PDUs

**Q:** Selective Repeat receiver window?  
**A:** WR > 1

**Q:** Selective Repeat on timeout retransmits?  
**A:** Only lost/unacknowledged PDUs

**Q:** Cumulative ACK(n) means?  
**A:** All PDUs up to n received

**Q:** Which buffers out-of-sequence PDUs?  
**A:** Selective Repeat only

**Q:** Most efficient ARQ protocol?  
**A:** Selective Repeat

**Q:** Why PDU numbering needed?  
**A:** Detect duplicates

**Q:** What is RTT?  
**A:** Round Trip Time

---

**END OF CHAPTER 3: WINDOW PROTOCOLS (ARQ TECHNIQUES)**

**Status:** ✅ Complete - Ready for exam preparation  
**Importance:** ⭐⭐⭐ HIGH PRIORITY - 10-15% of exam  
**Next Chapter:** Physical Layer, Access & Transport Networks

