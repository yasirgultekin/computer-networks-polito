# CHAPTER 8: ROUTING
## Exam-Oriented Study Guide

**Based on:** Professor's lecture slides (Routing slides 1-33)  
**Exam Weight:** High (⭐⭐⭐) - Approximately 15-20% of exam questions  
**Study Priority:** HIGH - Critical for understanding network layer

---

## 📋 CHAPTER OVERVIEW

This chapter covers **Routing** at the Network Layer, focusing on how routers find paths through networks using different algorithms and protocols.

**Main Topics:**
1. Network Layer Functions (Routing vs Forwarding)
2. Routing Algorithm Classification
3. Link State Routing (Dijkstra's Algorithm)
4. Distance Vector Routing (Bellman-Ford)
5. Algorithm Comparison

---

# PART 1: NETWORK LAYER FUNCTIONS

## 🎯 SLIDES 2-5: Routing Fundamentals

### Network Layer Functions

**Three Main Functions:**

#### 1. **ROUTING** (Control Plane)
- **Definition:** Path determination / route selection
- **Executed:** Looking at routing table
- **When:** 
  - For every PDU in **datagram services**
  - For every connection/call in **virtual circuit services**

#### 2. **Addressing**
- Unique addresses for each node
- Address resolution (mapping)

#### 3. **Congestion Control**
- Buffer reservation
- **Packet drops** (most widely used method)
- Explicit congestion signaling

---

### Routing Table

**Contains:** Destination → **Next Hop** mapping

**Example:**
```
Destination    Next Hop
10.0.1.0/24   →  Router B
20.0.5.0/24   →  Router C
```

**Critical Point:** Table stores **next hop** (next router), NOT complete path

---

### Three Key Concepts to Distinguish

#### 1. **Routing Protocols**
- **Purpose:** Define how to exchange network status among nodes
- **Function:** Build the routing table
- **Examples:** RIP, OSPF, BGP

#### 2. **Routing Algorithms**
- **Purpose:** Select the path toward destination
- **Input:** Network status information
- **Output:** Builds routing table
- **Examples:** Dijkstra, Bellman-Ford

#### 3. **Forwarding Procedures**
- **Purpose:** Forward each packet to proper output port
- **Function:** Exploits the routing table
- **When:** For every packet (data plane operation)

**Distinction:**
```
Routing Protocol → Exchanges Info
       ↓
Routing Algorithm → Computes Paths → Builds Table
       ↓
Forwarding → Uses Table → Sends Packets
```

---

### 📊 Exam Pattern

**Question:** "Routing is executed ___"  
**Answer:** **Looking at routing table**

**Question:** "Routing table contains ___"  
**Answer:** **Next hop for every destination**

**Question:** "Difference between routing and forwarding?"  
**Answer:** **Routing = path computation (control plane), Forwarding = packet switching (data plane)**

**Question:** "Most common congestion control method?"  
**Answer:** **Packet drops**

---

# PART 2: ROUTING ALGORITHMS - FUNDAMENTALS

## 🎯 SLIDES 6-10: Algorithm Classification and Basics

### Routing Algorithm Goal

**Objective:** Define a "good" path from source to destination

**Network as Graph:**
- **Nodes** = Vertices (routers)
- **Links** = Edges (connections)
- **Costs** assigned to edges

**"Good" path** = **Minimum cost path**

---

### Link Cost

**Cost can be:**
- **Fixed:** Static value (e.g., 1 for every link)
- **Distance:** Physical distance
- **Delay:** Propagation + transmission time
- **Monetary:** Euro cost
- **Congestion level:** Current load

**Static vs Dynamic:**
- **Static:** Cost doesn't change
- **Dynamic:** Cost depends on network status (e.g., current load)

**Warning:** Dynamic costs can cause **oscillations**
- If cost = link load, traffic may oscillate between paths
- As load increases on one path, cost increases
- Traffic moves to alternative path
- Then first path becomes cheaper again
- Cycle repeats

---

### Simple Routing Algorithms (No Coordination)

These avoid coordination but are inefficient:

#### 1. **Random**
- Randomly select output port
- Very inefficient

#### 2. **Flooding**
- Forward on **ALL output ports** (except input port)
- Guarantees delivery but wastes bandwidth
- **Very high overhead**

#### 3. **Deflection / Hot Potato**
- Used on regular topologies
- If correct port available → use it
- If correct port busy → use any available port
- Suboptimal but avoids buffering

**Practical Use:** Modern networks use coordinated algorithms (Link State or Distance Vector)

---

### Algorithm Taxonomy: Centralized vs Distributed

#### **CENTRALIZED**
**How it works:**
- One node collects info from all other nodes
- Computes paths centrally
- Distributes routing tables to all nodes

**Pros:**
- ✅ Can use complex algorithms and costs
- ✅ Coherent routing plan for all nodes
- ✅ No conflicts

**Cons:**
- ❌ Single point of failure
- ❌ Large control info load to/from central node
- ❌ Scalability issues

**Status:** Rarely used in modern networks

---

#### **DISTRIBUTED**
**How it works:**
- All nodes exchange info via routing protocols
- All nodes compute paths independently or based on neighbor info

**Pros:**
- ✅ Robust to failures (no single point of failure)
- ✅ Uniform control load distribution
- ✅ Scalable

**Cons:**
- ❌ Intelligence needed in all nodes
- ❌ Errors in exchanged info may create non-coherent routing
- ❌ Can lead to loops

**Status:** Standard in modern networks (Internet uses distributed)

---

### Distributed Algorithm Types

#### **GLOBAL (Link State)**
- **Knowledge:** All nodes know complete network topology + all link costs
- **Exchange:** All nodes exchange info with ALL other nodes
- **Algorithm:** **Link State** (e.g., OSPF)
- **Method:** Dijkstra's algorithm

#### **PARTIAL (Distance Vector)**
- **Knowledge:** Nodes only know adjacent nodes + their link costs
- **Exchange:** Only adjacent nodes exchange info
- **Algorithm:** **Distance Vector** (e.g., RIP)
- **Method:** Bellman-Ford algorithm

---

### 📊 Exam Pattern

**Question:** "In centralized routing, who computes paths?"  
**Answer:** **One central node**

**Question:** "Main advantage of distributed routing?"  
**Answer:** **Robust to failures** (no single point of failure)

**Question:** "Link State uses which type of information?"  
**Answer:** **Global** (complete topology)

**Question:** "Distance Vector uses which type of information?"  
**Answer:** **Partial** (only adjacent nodes)

**Question:** "Flooding forwards to ___"  
**Answer:** **All output ports** (except input port)

---

# PART 3: LINK STATE ROUTING

## 🎯 SLIDES 11-16: Dijkstra's Algorithm

### Link State Algorithm Overview

**Principle:** Every node knows complete network topology

**Process:**

1. **Discovery:** Every node sends **link cost info** to ALL other nodes
   - Method: **(Multi)broadcast** or flooding

2. **Topology Building:** Every node builds complete network topology
   - Knows all nodes
   - Knows all link costs

3. **Path Computation:** Every node computes minimum cost paths to all destinations
   - Uses **Dijkstra's algorithm**
   - Stores results in routing table

**Key Point:** All nodes have **same topology information**, but each computes paths from its own perspective

---

### Dijkstra's Algorithm

**Type:** Iterative algorithm

**Property:** After k iterations, minimum cost paths to k destinations are known

**Requirement:** **Works only for POSITIVE costs**

---

### Dijkstra Algorithm Notation

**Variables:**

- **c(i,j)** = cost of link from node i to node j
  - = ∞ if nodes not directly connected

- **D(n)** = current cost of best path from source to destination n

- **p(n)** = preceding node (parent) in path toward destination n

- **N** = set of nodes for which optimal path is known

---

### Dijkstra Algorithm Steps

```
1. Initialization (assume source = A):
2.   N = {A}
3.   For all nodes n ∉ N:
4.     if n adjacent to A:
5.       D(n) = c(A,n), p(n) = A
6.     else:
7.       D(n) = ∞

8. repeat:
9.   Find node w ∉ N such that D(w) is minimum
10.  Add w to N
11.  Update D(n) for all n adjacent to w, n ∉ N:
12.    if (D(n) > D(w) + c(w,n)):
13.      D(n) = D(w) + c(w,n), p(n) = w
14.    /* New cost to n is either:
15.       - Old cost to n, OR
16.       - Cost to w + cost from w to n */
17. until all nodes in N
```

**Key Logic (Line 12-13):** 
- Compare current path to n: D(n)
- With alternative through w: D(w) + c(w,n)
- Keep the minimum

---

### Dijkstra Example

**Network:**
```
    5         2
A ——————— B
|         |
|1       2|
|         |
D         |
|         |
|3       1|
|         |
C ——————— E
    3         
        1
      E ——— F
        2
```

**Execution Table:**

| Step | Start N | D(B),p(B) | D(C),p(C) | D(D),p(D) | D(E),p(E) | D(F),p(F) | Selected |
|------|---------|-----------|-----------|-----------|-----------|-----------|----------|
| 0    | A       | 2,A       | 5,A       | 1,A       | ∞         | ∞         | -        |
| 1    | AD      | 2,A       | 4,D       | -         | 2,D       | ∞         | D (cost 1) |
| 2    | ADE     | 2,A       | 3,E       | -         | -         | 4,E       | E (cost 2) |
| 3    | ADEB    | -         | 3,E       | -         | -         | 4,E       | B (cost 2) |
| 4    | ADEBC   | -         | -         | -         | -         | 4,E       | C (cost 3) |
| 5    | ADEBCF  | -         | -         | -         | -         | -         | F (cost 4) |

**Final Routing Table at A:**
```
Destination  Next Hop  Cost
B            B         2
C            D         3
D            D         1
E            D         2
F            D         4
```

**Note:** Next hop from A to C, E, F is all D (shortest path goes through D)

---

### Dijkstra Complexity

**Number of nodes:** M

**Complexity:**
- **Every iteration:**
  - Check all nodes w ∉ N
  - Add w at minimum distance
  
- **Total comparisons:** M × (M+1) / 2

- **Complexity:** **O(M²)**

**Better implementations:** O(M log M) using priority queues

---

### 📊 Exam Pattern

**Question:** "Dijkstra's algorithm works only for ___"  
**Answer:** **Positive costs**

**Question:** "After k iterations, Dijkstra has found paths to ___"  
**Answer:** **k destinations**

**Question:** "Dijkstra complexity?"  
**Answer:** **O(M²)** or O(M log M) with better implementation

**Question:** "Link State: each node knows ___"  
**Answer:** **Complete network topology** (all nodes and link costs)

**Question:** "In Dijkstra, D(n) represents ___"  
**Answer:** **Current cost of best path from source to n**

---

# PART 4: DISTANCE VECTOR ROUTING

## 🎯 SLIDES 17-30: Bellman-Ford Algorithm

### Distance Vector Algorithm Overview

**Principle:** Nodes exchange distance vectors with neighbors

**Properties:**

- **Iterative:** Runs until no more info needs to be exchanged
- **Asynchronous:** No synchronized iterations
- **Autonomous termination:** No explicit signal when done
- **Distributed:** Every node exchanges info only with **adjacent nodes**

---

### How Distance Vector Works

**Each Node:**

1. **Periodically** exchanges vector with adjacent nodes containing:
   - Reachable destinations
   - Current distance to each destination
   - Example: Number of hops

2. **Compares** received vector with current Routing Table

3. **Modifies** routing table if needed:
   - Add new destinations
   - Update if new paths are shorter
   - Modify costs

**Also known as:** "Routing by rumor" - nodes trust what neighbors tell them

---

### Distance Vector Pros and Cons

**Pros:**
- ✅ **Easy to implement**
- ✅ Simple logic
- ✅ Low computational complexity

**Cons:**
- ❌ **Slow convergence**
- ❌ **Routing errors propagate** (bad info spreads)
- ❌ **Not highly scalable**
  - Message size increases with network size
  - Contains info about ALL destinations

---

### Distance Table Structure

**Data Structure:** Distance table in every node

**Format:**
- **One row** for each possible destination
- **One column** for each adjacent node

**Formula:** At node X, for destination Y through adjacent node Z:

```
DX(Y,Z) = c(X,Z) + min{DZ(Y,w)}
                    w

Where:
- c(X,Z) = cost from X to adjacent node Z
- min{DZ(Y,w)} = minimum cost from Z to Y (through Z's neighbors w)
```

**Meaning:** Cost to reach Y via Z = cost to reach Z + Z's minimum cost to Y

---

### Distance Table Example

**Network:**
```
    7
A ——— B
    1     8
E ——— D
    2
```

**Distance Table at E:**

|     | A  | B  | D |
|-----|----|----|---|
| A   | 1  | 14 | 5 |
| B   | 7  | 8  | 5 |
| C   | 6  | 9  | 4 |
| D   | 4  | 11 | 2 |

**Reading the table:**
- To reach A via A: cost = 1 (direct)
- To reach A via B: cost = 14 (via B)
- To reach A via D: cost = 5 (via D)
- To reach C via D: cost = 4 (best path)

**Calculation example:**
```
DE(C,D) = c(E,D) + min{DD(C,w)}
         = 2 + 2 = 4
```

---

### From Distance Table to Routing Table

**Distance Table** (at E):
|     | A  | B  | D |
|-----|----|----|---|
| A   | 1  | 14 | 5 |
| B   | 7  | 8  | 5 |
| C   | 6  | 9  | 4 |
| D   | 4  | 11 | 2 |

**⬇ Select minimum cost for each destination**

**Routing Table** (at E):
| Destination | Next Hop | Cost |
|-------------|----------|------|
| A           | A        | 1    |
| B           | D        | 5    |
| C           | D        | 4    |
| D           | D        | 2    |

**Process:** For each destination, select column with minimum cost

---

### Distance Vector Algorithm Pseudocode

**Initialization (at node X):**
```
For every adjacent node v:
  DX(*,v) = ∞           // * means all destinations
  DX(v,v) = c(X,v)      // Direct link cost

For every destination y:
  Send min{DX(y,w)} to every adjacent node w
         w
```

---

**Main Loop (at node X):**
```
loop:
  wait (until link cost change to neighbor V
        OR receive update from neighbor V)
  
  if (c(X,V) changes by d):
    // Link cost changed
    For all destinations y:
      DX(y,V) = DX(y,V) + d
  
  else if (update received from V for destination Y):
    // Neighbor sent new distance
    DX(Y,V) = c(X,V) + newval
  
  if we have a new min{DX(Y,w)} for any destination Y:
                    w
    send new value to all neighbors
  
forever
```

---

### Distance Vector Example

**Network:**
```
    2
X ——— Y
|     |
|7   1|
|     |
Z ————
```

**Calculation at X:**

**To reach Y via Z:**
```
DX(Y,Z) = c(X,Z) + min{DZ(Y,w)}
                    w
        = 7 + 1 = 8
```

**To reach Z via Y:**
```
DX(Z,Y) = c(X,Y) + min{DY(Z,w)}
                    w
        = 2 + 1 = 3
```

**Result:** Best path from X to Z is via Y (cost 3, not via direct link cost 7)

---

### Link Cost Changes

#### **Good News Travels Fast**

**Scenario:** Link cost decreases

**Network before:**
```
    1
X ——— Y
    50    1
    Z ————
```

**Change:** X-Y link cost changes from 50 to 1

**Result:**
- X detects change immediately
- Updates distance table
- Sends update to neighbors
- **Fast convergence** - algorithm terminates quickly

---

#### **Bad News Travels Slow - Count-to-Infinity Problem**

**Scenario:** Link cost increases

**Network before:**
```
    4
X ——— Y
    50    1
    Z ————
```

**Change:** X-Y link cost changes from 4 to 60

**Problem:**
- Y thinks it can reach X via Z (with total cost 51)
- But Z's path to X actually goes through Y!
- Y tells Z: "I can reach X with cost 51 via Z"
- Z updates: "I can reach X with cost 52 via Y"
- Y updates: "I can reach X with cost 53 via Z"
- ... (continues incrementing)
- **Slow convergence** - counts to infinity (or max hop count)

**This is the COUNT-TO-INFINITY problem**

---

### Poisoned Reverse Solution

**Technique:** If Z routes to X via Y, Z tells Y that Z's distance to X is ∞

**Logic:**
- Z prevents Y from trying to route to X via Z
- Breaks the loop

**Network:**
```
    60
X ——— Y
    50    1
    Z ————
```

**With Poisoned Reverse:**
- Z routes to X via Y
- Z tells Y: "My distance to X is ∞"
- Y won't try to route to X via Z
- Faster convergence

**Limitation:** Does NOT fully solve the problem for loops involving 3+ nodes

---

### 📊 Exam Pattern

**Question:** "Distance Vector is also known as ___"  
**Answer:** **Routing by rumor**

**Question:** "Distance Vector exchanges info with ___"  
**Answer:** **Adjacent nodes only** (neighbors)

**Question:** "Main problem with Distance Vector?"  
**Answer:** **Slow convergence** / **Count-to-infinity problem**

**Question:** "Poisoned Reverse prevents ___"  
**Answer:** **Routing loops** (partially)

**Question:** "Good news travels ___, bad news travels ___"  
**Answer:** **Fast, slow**

**Question:** "Distance Vector message size depends on ___"  
**Answer:** **Number of destinations** (scalability issue)

---

# PART 5: LINK STATE VS DISTANCE VECTOR

## 🎯 SLIDES 31-33: Algorithm Comparison

### Message Complexity

**With M nodes and E edges (neighbors) per node:**

#### **Link State:**
- Every node sends to ALL other nodes
- Messages: **O(M)** messages
- Size: **O(E)** per message (link costs)
- **Total:** O(M × E)

#### **Distance Vector:**
- Every message contains ALL destinations: **O(M)**
- Sent to **O(E)** neighbors
- **Total:** O(E × M)

**Comparison:** Similar complexity O(ME), but:
- LS: Send to all, small messages
- DV: Send to neighbors, large messages

---

### Speed of Convergence

#### **Link State:**
- **Immediate** after new state is propagated
- All nodes get complete info quickly
- Dijkstra runs once
- **Fast convergence**

#### **Distance Vector:**
- **Variable time**
- Each node depends on adjacent nodes
- Several message exchange phases needed
- **Slow convergence**
- Worse with count-to-infinity problem

**Winner:** **Link State** (much faster)

---

### Reliability (Node Misbehavior)

**What if a node lies or makes mistakes?**

#### **Link State:**
- Nodes may announce **wrong link costs**
- All nodes make mistake
- **But NO LOOPS created**
- Errors reset at next info exchange
- **Localized impact**

#### **Distance Vector:**
- Nodes may announce **wrong path costs**
- All nodes use this wrong info **(indirectly)**
- **Errors propagate through network**
- **Routing errors may create LOOPS**
- **Widespread impact**

**Winner:** **Link State** (more robust)

---

### Complete Comparison Table

| Feature | Link State | Distance Vector |
|---------|------------|-----------------|
| **Information** | Global (complete topology) | Partial (neighbors only) |
| **Exchange** | All nodes | Adjacent nodes only |
| **Algorithm** | Dijkstra | Bellman-Ford |
| **Message Size** | O(E) | O(M) |
| **Message Recipients** | All nodes | Neighbors |
| **Convergence** | **Fast** | **Slow** |
| **Count-to-Infinity** | **No** | **Yes** |
| **Loop Risk** | **Low** | **High** |
| **Error Impact** | Localized | Propagates |
| **Complexity** | O(M²) or O(M log M) | O(M) per iteration |
| **Scalability** | Good | Poor (message size) |
| **Examples** | **OSPF, IS-IS** | **RIP** |
| **Internet Use** | **Common** (OSPF) | Limited (RIP) |

---

### Real-World Usage

#### **Link State** (OSPF - Open Shortest Path First)
- Used in **large enterprise networks**
- Used in **ISP backbones**
- Fast convergence critical
- Hierarchical design (areas)

#### **Distance Vector** (RIP - Routing Information Protocol)
- Used in **small networks** only
- **Limited** to 15 hops (infinity = 16)
- **Legacy** protocol
- Being replaced by OSPF

**Modern Trend:** Link State (OSPF) dominating

---

### 📊 Exam Pattern

**Question:** "Which converges faster: LS or DV?"  
**Answer:** **Link State (LS)**

**Question:** "Which has count-to-infinity problem?"  
**Answer:** **Distance Vector (DV)**

**Question:** "Which knows complete topology?"  
**Answer:** **Link State (LS)**

**Question:** "Which exchanges info with all nodes?"  
**Answer:** **Link State (LS)**

**Question:** "Which is more robust to errors?"  
**Answer:** **Link State (LS)**

**Question:** "OSPF uses which algorithm?"  
**Answer:** **Link State** (Dijkstra)

**Question:** "RIP uses which algorithm?"  
**Answer:** **Distance Vector** (Bellman-Ford)

**Question:** "Which has better scalability?"  
**Answer:** **Link State (LS)** - smaller messages

---

# SUMMARY: EXAM-CRITICAL POINTS FOR CHAPTER 8

## 🎯 MUST MEMORIZE

### Routing vs Forwarding

| Aspect | Routing | Forwarding |
|--------|---------|------------|
| **Plane** | Control plane | Data plane |
| **Function** | Path computation | Packet switching |
| **When** | Occasional | Every packet |
| **Output** | Routing table | Packet forwarded |

### Algorithm Classification

| Type | Knowledge | Exchange | Algorithm | Example |
|------|-----------|----------|-----------|---------|
| **Link State** | **Global** (complete topology) | **All nodes** | **Dijkstra** | **OSPF** |
| **Distance Vector** | **Partial** (neighbors only) | **Adjacent nodes** | **Bellman-Ford** | **RIP** |

### Dijkstra's Algorithm

- **Type:** Link State
- **Requirement:** Positive costs only
- **Complexity:** O(M²) or O(M log M)
- **After k iterations:** k destinations known
- **Convergence:** Fast

### Distance Vector Algorithm

- **Also called:** Routing by rumor
- **Exchange:** Adjacent nodes only
- **Problem:** Count-to-infinity (slow convergence)
- **Solution:** Poisoned reverse (partial)
- **Good news:** Travels fast
- **Bad news:** Travels slow

### Link State vs Distance Vector

**Link State WINS on:**
- ✅ Convergence speed (FAST)
- ✅ No count-to-infinity
- ✅ Error localization
- ✅ Scalability

**Distance Vector:**
- ✅ Easier to implement
- ❌ Slow convergence
- ❌ Count-to-infinity problem
- ❌ Poor scalability

---

## ⚠️ COMMON EXAM TRAPS

### Trap 1: Routing vs Forwarding
**WRONG:** "Routing forwards packets"  
**RIGHT:** "Routing computes paths, Forwarding sends packets" ✓

### Trap 2: Dijkstra Requirements
**WRONG:** "Dijkstra works with any costs"  
**RIGHT:** "Dijkstra requires POSITIVE costs only" ✓

### Trap 3: Link State Knowledge
**WRONG:** "Link State nodes know only neighbors"  
**RIGHT:** "Link State nodes know COMPLETE topology" ✓

### Trap 4: Distance Vector Exchange
**WRONG:** "Distance Vector exchanges with all nodes"  
**RIGHT:** "Distance Vector exchanges with ADJACENT nodes only" ✓

### Trap 5: Convergence Speed
**WRONG:** "Distance Vector converges faster"  
**RIGHT:** "Link State converges FASTER" ✓

### Trap 6: Count-to-Infinity
**WRONG:** "Link State has count-to-infinity problem"  
**RIGHT:** "DISTANCE VECTOR has count-to-infinity problem" ✓

### Trap 7: OSPF Algorithm
**WRONG:** "OSPF uses Distance Vector"  
**RIGHT:** "OSPF uses Link State (Dijkstra)" ✓

### Trap 8: RIP Algorithm
**WRONG:** "RIP uses Link State"  
**RIGHT:** "RIP uses Distance Vector" ✓

---

## 📊 EXAM WEIGHT DISTRIBUTION

### CRITICAL (Study exhaustively - 60%):
- ✅ Routing vs Forwarding distinction
- ✅ Link State = Global knowledge, all nodes exchange
- ✅ Distance Vector = Partial knowledge, neighbors only
- ✅ Dijkstra = Link State, positive costs, O(M²)
- ✅ Distance Vector = Bellman-Ford, count-to-infinity
- ✅ Link State converges FAST, Distance Vector SLOW
- ✅ OSPF = Link State, RIP = Distance Vector

### HIGH (Study thoroughly - 30%):
- Dijkstra algorithm steps and example
- Distance table structure and calculations
- Good news travels fast, bad news travels slow
- Poisoned reverse technique
- Centralized vs Distributed routing
- Message complexity comparison

### MEDIUM (Understand well - 10%):
- Simple algorithms (flooding, random, hot potato)
- Dynamic costs and oscillations
- Error propagation differences
- Scalability issues

---

## 🎓 STUDY STRATEGY

### Day 1: Fundamentals
- Routing vs Forwarding
- Routing table concept (next hop)
- Routing protocols vs algorithms vs forwarding
- Centralized vs Distributed
- Global vs Partial knowledge

### Day 2: Link State (Dijkstra)
- Algorithm principle
- Dijkstra notation and steps
- Work through example step-by-step
- Practice calculating D(n) values
- Complexity O(M²)

### Day 3: Distance Vector
- Algorithm principle
- Distance table structure
- Bellman-Ford formula: DX(Y,Z) = c(X,Z) + min{DZ(Y,w)}
- Good news vs bad news
- Count-to-infinity problem

### Day 4: Algorithm Comparison
- Link State vs Distance Vector table
- Convergence speed
- Error handling
- Message complexity
- OSPF vs RIP

### Day 5: Practice & Review
- Work through Dijkstra examples
- Calculate distance tables
- Identify count-to-infinity scenarios
- Practice algorithm classification questions
- Review all traps

---

## 📝 QUICK REFERENCE FLASHCARDS

**Q:** Routing vs Forwarding?  
**A:** Routing = path computation (control), Forwarding = packet switching (data)

**Q:** Routing table contains?  
**A:** Next hop for each destination

**Q:** Link State knowledge?  
**A:** Global (complete topology)

**Q:** Distance Vector knowledge?  
**A:** Partial (adjacent nodes only)

**Q:** Link State exchanges with?  
**A:** All nodes

**Q:** Distance Vector exchanges with?  
**A:** Adjacent nodes only

**Q:** Link State algorithm?  
**A:** Dijkstra

**Q:** Distance Vector algorithm?  
**A:** Bellman-Ford

**Q:** Dijkstra requirement?  
**A:** Positive costs only

**Q:** Dijkstra complexity?  
**A:** O(M²) or O(M log M)

**Q:** Which converges faster?  
**A:** Link State

**Q:** Count-to-infinity problem in?  
**A:** Distance Vector

**Q:** OSPF uses which algorithm?  
**A:** Link State (Dijkstra)

**Q:** RIP uses which algorithm?  
**A:** Distance Vector

**Q:** Poisoned reverse prevents?  
**A:** Routing loops (partially)

**Q:** Good news travels?  
**A:** Fast

**Q:** Bad news travels?  
**A:** Slow

**Q:** Flooding forwards to?  
**A:** All output ports (except input)

---

**END OF CHAPTER 8: ROUTING**

**Status:** ✅ Complete - Ready for exam preparation  
**Importance:** ⭐⭐⭐ HIGH - 15-20% of exam  
**Next Steps:** Review all 8 chapters, focus on critical sections

**Note:** This chapter does NOT cover IP addressing and subnetting, which are typically part of the Network Layer but may be in a separate section of your course materials.

