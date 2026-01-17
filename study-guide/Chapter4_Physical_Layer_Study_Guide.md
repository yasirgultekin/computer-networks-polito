# CHAPTER 4: PHYSICAL LAYER - TRANSMISSION MEDIA & ACCESS NETWORKS
## Exam-Oriented Study Guide

**Based on:** Professor's lecture slides (Physical layer slides 1-77)  
**Exam Weight:** Medium (⭐⭐) - Approximately 10-12% of exam questions  
**Study Priority:** MEDIUM - Important foundation, but less tested than protocols

---

## 📋 CHAPTER OVERVIEW

This chapter covers the **Physical Layer** (Layer 1) of the OSI model, including transmission media types, encoding techniques, and access network technologies.

**Main Topics:**
1. Transmission Media (Electrical, Optical, Radio)
2. Line Coding and Digital Modulation
3. Access Networks (DSL, PON, Cellular)
4. Transport Networks
5. Cellular Network Evolution (1G to 4G)

---

# PART 1: TRANSMISSION MEDIA

## 🎯 SLIDES 3-21: Types of Transmission Media

### Three Main Categories

#### 1. ELECTRICAL MEDIA

##### A. Twisted Pair (TP)

**Description:**
- Two copper conductors twisted together
- Twisting reduces electromagnetic interference
- Uses differential transmission techniques

**Types:**
- **UTP (Unshielded Twisted Pair):** No shielding
- **FTP (Foiled Twisted Pair):** Foil shielding
- **STP (Shielded Twisted Pair):** Full shielding

**Categories and Speeds:**

| Category | Speed | Application |
|----------|-------|-------------|
| Cat 1 | Analog | Analog telephony |
| Cat 2 | - | ISDN |
| Cat 3 | 10 Mbps | LAN (10BASE-T) |
| Cat 4 | 16 Mbps | Token Ring |
| Cat 5 | 100 Mbps | Fast Ethernet |
| **Cat 5e** | **1 Gbps** | **Gigabit Ethernet** |
| **Cat 6** | **1 Gbps** | **Better quality than 5e** |
| **Cat 6a** | **10 Gbps** | **10 Gigabit Ethernet** |
| Cat 7 | 10 Gbps | Distance > 100m |
| Cat 8 | 40 Gbps | High-speed data centers |

**Connector:** RJ45 (8 pins for Ethernet)

**Advantages:**
- ✅ Low cost
- ✅ Easy to install and cable
- ✅ Flexible
- ✅ Widely deployed

**Disadvantages:**
- ❌ Electromagnetic interference susceptible
- ❌ Limited distance
- ❌ Lower speed than fiber

**Use Cases:**
- Telephone networks
- Ethernet LANs
- Building cabling

##### B. Coaxial Cable

**Description:**
- One central conductor
- One or more shields/covers
- Faraday cage effect reduces interference

**Advantages:**
- ✅ Better shielding than twisted pair
- ✅ Higher frequency capacity
- ✅ Reduced electromagnetic interference

**Disadvantages:**
- ❌ Higher cost than twisted pair
- ❌ Complex cabling and installation
- ❌ Less flexible

**Speed:** ~Hundreds of Mbps

**Use Cases:**
- Old generation LANs (10BASE2, 10BASE5)
- Antenna connections
- Cable TV networks

---

#### 2. OPTICAL MEDIA

##### Optical Fiber

**Structure:**
- **Core:** Inner glass (where light travels)
- **Cladding:** Outer glass (different refraction index)
- **Protection:** Outer protective layers

**How it works:** 
- Based on Snell's law
- Light reflects inside core
- Signal carried by LED or laser

**Advantages:**
- ✅ **Immune to electromagnetic interference**
- ✅ **Very high bit rate** (tens of Terabits/s)
- ✅ **Low attenuation** (~0.1 dB/km)
- ✅ Relatively low cost
- ✅ Small size
- ✅ Secure (difficult to tap)

**Disadvantages:**
- ❌ Only point-to-point connections
- ❌ Difficult to connect
- ❌ Difficult to align transceivers
- ❌ Not easy to lay (limited bend radius)
- ❌ Suffers from vibration

**Attenuation Windows:**

| Window | Wavelength | Attenuation | Use |
|--------|------------|-------------|-----|
| **First** | **850 nm** | **1.2 dB/km** | Short distance |
| **Second** | **1300 nm** | **0.4 dB/km** | Medium distance |
| **Third** | **1550 nm** | **0.2 dB/km** | Long distance (best) |

**Key Point:** Lower attenuation at higher wavelengths (infrared range)

**Submarine Cables:**
- Cables at ocean bottom
- Amplifiers every 30-50 km
- Each amplifier backed up
- Power supply over cable
- Costly maintenance

**Use Cases:**
- Long-distance communications
- Internet backbone
- Data centers
- High-speed LANs

---

#### 3. RADIO MEDIA (Wireless)

##### Radio/Ether Transmission

**Characteristics:**
- Signals sent via antennas
- Transmitter to one or several receivers
- **Radiomobile:** If TX or RX is mobile

**Signal Propagation:**

**Friis Equation (Free Space):**
```
PR/PT = GT × GR × (λ²/(4πD)²)

Where:
PR = Received power
PT = Transmitted power
GT = Transmitter antenna gain
GR = Receiver antenna gain
λ = Wavelength
D = Distance
```

**Key Point:** Received power ∝ 1/D² (inverse square of distance)

**Factors Affecting Quality:**
1. **Distance:** Longer distance → weaker signal
2. **Frequency:** Higher frequency → higher attenuation
3. **Transmitted power:** Higher power → better reception
4. **Environment:**
   - Natural obstacles (buildings, mountains)
   - Co-channel interference
   - Atmospheric phenomena (fog, rain, clouds)

**Radio-Specific Problems:**

##### 1. Multipath Propagation
- Signal reflects off obstacles
- Creates multiple copies arriving at different times
- Causes interference

##### 2. Fading
- Quick signal amplitude variation
- Due to in-phase or out-of-phase combination of signal copies
- Rapid changes
- **Effect:** SNR varies quickly

##### 3. Shadowing
- Slow signal amplitude variation
- Due to obstacles blocking signal
- Gradual changes
- **Effect:** Long-term signal level reduction

**Visualization:**
```
Signal Amplitude
     ^
     |     Fading (fast)
     |  /\/\/\/\/\
     | /          \___    Shadowing (slow)
     |/               \___
     +-------------------> Distance
```

**Use Cases:**
- Wi-Fi networks
- Cellular networks
- Satellite communications
- Point-to-point radio links

---

### Media Parameters (CRITICAL!)

**For Electrical Media:**

1. **Impedance:** Function of frequency
2. **Propagation Speed:** 
   - Cables: 0.5c to 0.7c (where c = speed of light)
   - Fiber: ~0.6c
3. **Attenuation:**
   - Increases linearly with distance
   - Increases with √frequency
   - Measured in dB
4. **Cross-Talk:**
   - Noise from adjacent wires
   - Increases with distance then saturates

### 📊 Exam Pattern

**Question:** "Which has highest bit rate: twisted pair, coax, or fiber?"  
**Answer:** **Fiber optic** (tens of Tbps)

**Question:** "Fiber optic attenuation at 1550nm is ___"  
**Answer:** **~0.2 dB/km** (third window, lowest attenuation)

**Question:** "Cat 5e twisted pair supports up to ___"  
**Answer:** **1 Gbps** (Gigabit Ethernet)

**Question:** "Fading is ___ amplitude variation"  
**Answer:** **Quick/Fast** (shadowing is slow)

**Question:** "Received power is proportional to ___"  
**Answer:** **1/D²** (inverse square of distance)

---

# PART 2: TRANSMISSION TECHNIQUES

## 🎯 SLIDES 22-31: Line Coding and Digital Modulation

### Two Main Techniques

#### 1. Line Coding
**For:** Electrical and optical media  
**Maps:** Bits/symbols → Digital signals  
**Media:** Well-suited to pulsed signals

#### 2. Digital Modulation
**For:** Radio, optical, electrical media  
**Maps:** Bits/symbols → Analog signals  
**Carrier:** Sinusoidal signal modulated

---

### LINE CODING

**Purpose:** Represent digital information via digital signals

**Classification by Voltage Level:**
1. Unipolar
2. Polar
3. Bipolar

---

#### 1. Unipolar Coding

**How it works:**
- 0 → Zero voltage
- 1 → Positive voltage

**Advantages:**
- ✅ Simple implementation

**Disadvantages:**
- ❌ Loss of synchronization (long sequences of 0s or 1s)
- ❌ Non-null DC component (needs filtering)
- ❌ In optical: long 1s overload LED

**Use Case:** Simple, low-speed systems

---

#### 2. Polar Coding

**Principle:** Two voltage levels with different polarities

**Reduces DC component** compared to unipolar

##### Three Variations:

**A. NRZ (Non-Return-to-Zero)**
- No transition to zero between consecutive bits
- Simple
- Synchronization issues with long sequences

**B. RZ (Return-to-Zero)**
- Transition to zero between consecutive bits
- Better synchronization
- Requires higher bit rate

**C. Biphase (Manchester)**
- Every bit represented by TWO voltage levels with inverse polarity
- **Excellent synchronization recovery**
- Transition in middle of bit period
- No DC component
- **Requires 2x bit rate** (drawback)

**Used in:** Classic Ethernet (10BASE-T)

---

#### 3. Bipolar Coding (AMI)

**How it works:**
- 0 → Zero voltage
- 1 → Alternates between positive and negative voltage

**Also called:** AMI (Alternate Mark Inversion)

**Advantages:**
- ✅ Enables ternary symbols (-1, 0, +1)
- ✅ No DC component
- ✅ Better error detection

**Example:** 8B6T coding
- 8 bits coded as 6 ternary symbols
- Reduces number of signal changes

---

#### 4. nBmB Coding

**Principle:** n bits represented as m bits, where n < m

**Examples:**
- **4B5B:** 4 bits → 5 bits
- **8B10B:** 8 bits → 10 bits (Gigabit Ethernet)
- **64B66B:** 64 bits → 66 bits (10 Gigabit Ethernet)

**Advantages:**
- ✅ Avoid code words with too many 0s or 1s
- ✅ Easier synchronization
- ✅ Reduced DC component
- ✅ Reserved codes for control functions (framing, idle, padding)

**Disadvantage:**
- ❌ Reduced effective bit rate (overhead)

**Calculation:**
- Efficiency = n/m
- Example: 8B10B → 80% efficiency

---

### DIGITAL MODULATION

**Purpose:** Represent digital information via analog signals

**Method:** Vary carrier signal parameters

**Carrier Signal Parameters:**
1. **Amplitude** → ASK (Amplitude Shift Keying)
2. **Frequency** → FSK (Frequency Shift Keying)
3. **Phase** → PSK (Phase Shift Keying)
4. **Combination** → QAM (Quadrature Amplitude Modulation)

**Notation:**
- Number indicates symbols in modulating signal
- **8-PSK:** 8 symbols (3 bits per symbol)
- **64-QAM:** 64 symbols (6 bits per symbol)
- **256-QAM:** 256 symbols (8 bits per symbol)

**Key Principle:**
- Higher order modulation → Higher bit rate
- BUT requires higher quality channel
- Trade-off between speed and reliability

**Use Cases:**
- Wi-Fi: QAM modulations
- LTE: Up to 256-QAM
- DSL: QAM modulations

### 📊 Exam Pattern

**Question:** "Manchester encoding requires ___ bit rate"  
**Answer:** **2x** (or double/twice the data rate)

**Question:** "Which line coding has no DC component: unipolar, NRZ, or biphase?"  
**Answer:** **Biphase (Manchester)** ✓

**Question:** "8B10B coding efficiency is ___"  
**Answer:** **80%** (8/10 = 0.8)

**Question:** "64-QAM encodes ___ bits per symbol"  
**Answer:** **6 bits** (2^6 = 64)

**Question:** "Higher order modulation requires ___"  
**Answer:** **Higher quality channel** / **Better SNR**

---

# PART 3: ACCESS AND TRANSPORT NETWORKS

## 🎯 SLIDES 32-34: Network Segmentation

### Two Types of Network Segments

#### 1. Access Network (Last Mile / Local Loop)

**Definition:** Connects user to service provider's access node (e.g., urban central office)

**Types:**
- **Residential:** Home connections
- **Mobile:** Cellular access
- **Institutional:** Campus/enterprise

**Also called:** Last mile, local loop

#### 2. Transport Network (Backbone)

**Definition:** Devices and media of providers enabling data transfer among access nodes

**Types:**
- **Metropolitan:** City-level
- **National:** Country-level
- **International:** Global

**Structure:**
```
User → [Access Network] → Access Node → [Transport Network] → Access Node → [Access Network] → User
```

---

# PART 4: ACCESS NETWORK TECHNOLOGIES

## 🎯 SLIDES 35-48: DSL and PON Technologies

### Main Access Technologies

1. **DSL (Digital Subscriber Line)** - Most common
2. **PON (Passive Optical Networks)** - Modern, high-speed
3. **Mobile Broadband** - Cellular (covered later)

### Minor/Older Technologies:
- POTS (Plain Old Telephone Service)
- HFC (Hybrid Fiber Coaxial)
- ISDN (Integrated Services Digital Network)
- Satellite
- WiMAX

---

### DSL ACCESS (xDSL Family)

#### ADSL (Asymmetric DSL)

**Characteristics:**
- **Asymmetric:** Higher downstream, lower upstream
- Designed for client-server applications (web browsing)
- Uses existing telephone twisted pair
- Dedicated bit rate from user to first access node only

**Speed depends on distance** from user to access node

**Versions:**

| Version | Downstream | Upstream |
|---------|------------|----------|
| **ADSL** | 6 Mbps | 1.5 Mbps |
| **ADSL2** | 8 Mbps | 3.5 Mbps |
| **ADSL2+** | 24 Mbps | 3.5 Mbps |

**Components:**

##### At User Premises:
1. **Splitter Filter**
   - Separates voice signal from data
   - Voice: 0-4 kHz
   - Data: 25 kHz - 1.1 MHz

2. **ADSL Modem**
   - **MODEM = MOdulator/DEModulator**
   - Transmission: Digital → Analog (for twisted pair)
   - Reception: Analog → Digital
   - Makes digital signal suitable for voice band

##### In the Network:
1. **Filter/Modem POTS**
   - Separates voice and data flows

2. **DSLAM (DSL Access Multiplexer)**
   - Receives data flows from multiple users
   - Multiplexes them onto single high-speed channel
   - Aggregates traffic

#### VDSL (Very High-Rate DSL)

**Purpose:** Further increase bit rate for short distances

**Speeds:**
- **VDSL:** Up to 50 Mbps
- **VDSL2:** Over 100 Mbps

**Requirements:**
- Short distance (urban environment)
- Better transmission standards
- Higher frequency bands than ADSL2+

**Key Principle:** Speed ↓ as distance ↑ (due to attenuation and noise)

**Trade-off:** VDSL = high speed but short distance

---

### PASSIVE OPTICAL NETWORKS (PON)

#### Overview

**Purpose:** Fiber-based passive optical access in last mile

**"Passive":** Unpowered devices (no electricity in distribution network)

**From:** Central office  
**To:** As close as reasonable to residential users

#### PON Components

**Four Main Components:**

1. **OLT (Optical Line Terminator)**
   - Location: Central office
   - Function: Network side termination

2. **ONU (Optical Network Units)**
   - Location: Street cabinet
   - Function: Neighborhood distribution

3. **ONT (Optical Network Terminals)**
   - Location: User premises
   - Function: Customer side termination

4. **ODN (Optical Distribution Network)**
   - Passive optical splitters
   - Fiber distribution

#### PON Deployment Scenarios

**Two Main Types:**

1. **FTTH (Fiber-To-The-Home)**
   - Fiber all the way to user premises
   - Highest speed
   - Highest cost (fiber replacement)

2. **FTTCab (Fiber-To-The-Cabinet)**
   - Fiber to street cabinet
   - VDSL for last segment (copper)
   - Shorter copper = less attenuation
   - Lower cost (reuses existing copper)

#### PON Technologies

**Two Main Standards (very similar):**

##### 1. GPON (Gigabit PON)

**Specifications:**
- **Downstream:** 2.5 Gbps
- **Upstream:** 1 Gbps (asymmetric)
- **Split ratio:** Up to 64 ONUs per OLT (typically 32 in Italy)
- **Supports:** Multiple frame/encapsulation formats

**Next Generation:**
- **XG-PON:** 10 Gbps / 2.5 Gbps
- **XGS-PON:** 10 Gbps / 10 Gbps (symmetric)
- **NG-PON2:** 4×10 Gbps / 10 Gbps
- **Split ratio:** Up to 256 ONUs per OLT

##### 2. EPON (Ethernet PON)

**Specifications:**
- **Speed:** 1 Gbps symmetric
- **Frames:** Ethernet frames (native compatibility)
- **Split ratio:** Up to 64 ONUs per OLT

**Advantage:** Direct Ethernet compatibility

#### PON Technical Aspects

**Multiplexing:**

1. **WDM (Wavelength Division Multiplexing)**
   - Downstream: ~1500 nm
   - Upstream: ~1300 nm
   - Bidirectional on single fiber

2. **TDM/TDMA**
   - Downstream: Time Division Multiplexing
   - Upstream: Time Division Multiple Access
   - **DBA (Dynamic Bandwidth Allocation)**
   - Statistical multiplexing/multiple access

---

### 📊 Exam Pattern

**Question:** "ADSL stands for ___"  
**Answer:** **Asymmetric Digital Subscriber Line**

**Question:** "DSLAM stands for ___"  
**Answer:** **DSL Access Multiplexer**

**Question:** "In PON, OLT is located at ___"  
**Answer:** **Central office**

**Question:** "FTTH means ___"  
**Answer:** **Fiber To The Home**

**Question:** "GPON downstream/upstream speeds are ___"  
**Answer:** **2.5 Gbps / 1 Gbps**

**Question:** "MODEM stands for ___"  
**Answer:** **MOdulator/DEModulator**

---

# PART 5: CELLULAR NETWORK EVOLUTION

## 🎯 SLIDES 52-59: Mobile Access Networks

### Radio Access Networks

**Two Categories:**

#### 1. Wireless Network
- Access via wireless link to access point
- **No mobility support**
- Examples: Wi-Fi, WiMAX, HiperLAN, Satellite

#### 2. Cellular Network
- Large area covered by adjacent cells
- Small areas controlled by antenna
- **Mobility support** (roaming and handover)
- Examples: GSM, UMTS, LTE, 5G

---

### Cellular Network Characteristics

**Key Concepts:**

1. **Cell**
   - Small area under control of one antenna
   - Shorter coverage → Higher bit rate
   - Resources shared among fewer users
   - But higher operational cost

2. **Roaming**
   - Ability to find a user
   - User can move between networks

3. **Handover (Handoff)**
   - Continuous coverage while moving
   - Seamless transfer from one cell to another
   - No communication interruption

---

### FOUR GENERATIONS OF CELLULAR NETWORKS

#### 1G - First Generation (1970s-1980s)

**Technology:** Analog

**Access:** FDMA (Frequency Division Multiple Access)

**Service:** Voice calls only

**Characteristics:**
- Large coverage cells
- Limited quality
- Inefficient frequency reuse
- Limited capacity

**Examples:**
- TACS (Italy: 1990-2005)
- AMPS (USA)

**Status:** Obsolete

---

#### 2G - Second Generation (1990s-2000s)

**Standard:** GSM (Europe, Japan), D-AMPS, IS-95 (USA)

**Technology:** Digital

**Access:** FDMA/TDMA

**Frequency Bands:** 850, 900, 1800, 1900 MHz

**Cell Size:** Max radius 40 km

**Features:**
- ✅ Digital service
- ✅ Privacy and security (encrypted transmission)
- ✅ Better capacity than 1G
- ✅ SMS support

**Data Services:**

**GPRS (General Packet Radio Service)**
- Dynamic TDM slot allocation
- Speed: Up to 170 kbps
- Charging: Based on traffic volume (not time)

**EDGE (Enhanced Data rates for GSM Evolution)**
- Same as GPRS but higher bit rate
- Speed: Up to 384 kbps
- Better modulation

**Status:** Still deployed in some areas

---

#### 3G - Third Generation (2000s-2010s)

**Standard:** UMTS (Universal Mobile Telecommunications System)

**Purpose:** Integrated data and voice (multimedia)

**Technology:**
- **Access:** FDMA/CDMA (Code Division Multiple Access)
- **Layered coverage:**
  - Micro-cells (high capacity)
  - Umbrella cells (uniform coverage)

**Speed:** Up to 2 Mbps initially

**Evolution: HSPA (High Speed Packet Access)**
- Speed: Up to 56 Mbps
- Same infrastructure
- Higher bit rate modulation
- Smaller latency
- **HSPA+:** Further improvements

**Advantages over 2G:**
- ✅ Higher data rates
- ✅ Better spectrum efficiency
- ✅ True multimedia support

**Status:** Still widely deployed

---

#### 4G - Fourth Generation (2010s-present)

**Name:** LTE (Long Term Evolution)

**Technology:**
- **Access:** OFDMA (Orthogonal FDMA)
- Frequency micro-channels assigned dynamically
- Based on traffic requests

**Key Features:**

1. **OFDMA Benefits:**
   - Micro-channels more fading resistant
   - Higher bit rate modulation possible
   - Adaptive to channel conditions

2. **MIMO (Multiple Input Multiple Output)**
   - Multiple antennas at device
   - Spatial multiplexing
   - Increased capacity

3. **All-IP Architecture:**
   - Internet architecture up to user terminal
   - Packet-switched only (no circuit-switched)

**Speed:** Up to 250 Mbps (theoretical)

**Modulation:** Up to 256-QAM (in LTE-Advanced)

**Service:** Worldwide coverage

**Advantages over 3G:**
- ✅ Much higher data rates
- ✅ Lower latency
- ✅ All-IP network (simpler)
- ✅ Better spectral efficiency

**Status:** Current mainstream technology

---

### Cellular Evolution Timeline

```
1970s: 1G (Analog, Voice only)
  ↓
1990s: 2G (Digital, GSM)
  ↓
2000s: 2.5G (GPRS, EDGE - Data services)
  ↓
2000s: 3G (UMTS - Multimedia, 2 Mbps)
  ↓
2000s: 3.5G (HSPA - Up to 56 Mbps)
  ↓
2010s: 4G (LTE - Up to 250 Mbps, All-IP)
  ↓
2020s: 5G (Current deployment)
```

---

### 📊 Exam Pattern

**Question:** "First generation cellular used ___ technology"  
**Answer:** **Analog** (1G = analog)

**Question:** "GSM belongs to ___ generation"  
**Answer:** **2G** (Second generation)

**Question:** "UMTS uses ___ access method"  
**Answer:** **CDMA** (FDMA/CDMA)

**Question:** "LTE stands for ___"  
**Answer:** **Long Term Evolution**

**Question:** "LTE uses ___ access technique"  
**Answer:** **OFDMA** (Orthogonal FDMA)

**Question:** "Handover means ___"  
**Answer:** **Transfer from one cell to another while maintaining connection**

**Question:** "Roaming means ___"  
**Answer:** **Ability to find/locate a user**

---

# SUMMARY: EXAM-CRITICAL POINTS FOR CHAPTER 4

## 🎯 MUST MEMORIZE

### Transmission Media Comparison

| Medium | Speed | Attenuation | Interference | Cost | Use |
|--------|-------|-------------|--------------|------|-----|
| **Twisted Pair** | Up to 40 Gbps | High | Susceptible | Low | LANs, Phone |
| **Coaxial** | ~100s Mbps | Medium | Low | Medium | Old LANs, Antennas |
| **Fiber Optic** | Tens of Tbps | Very Low (0.1 dB/km) | Immune | Medium | Long distance, Backbone |
| **Radio** | Varies | Distance² | High | Medium | Wireless, Mobile |

### Twisted Pair Categories (Most Tested)

| Category | Speed | Use |
|----------|-------|-----|
| **Cat 5e** | **1 Gbps** | **Gigabit Ethernet** ← Most common |
| **Cat 6** | **1 Gbps** | **Better than 5e** |
| **Cat 6a** | **10 Gbps** | **10 Gigabit Ethernet** |

### Fiber Optic Windows

| Window | Wavelength | Attenuation |
|--------|------------|-------------|
| First | 850 nm | 1.2 dB/km |
| Second | 1300 nm | 0.4 dB/km |
| **Third** | **1550 nm** | **0.2 dB/km** ← Best |

### Line Coding Summary

| Type | DC Component | Sync | Bit Rate | Use |
|------|--------------|------|----------|-----|
| Unipolar | Yes | Poor | 1x | Simple systems |
| NRZ | Reduced | Poor | 1x | Common |
| Manchester | No | Excellent | **2x** | Classic Ethernet |
| 8B10B | No | Good | 0.8x | Gigabit Ethernet |

### DSL Speeds

| Version | Downstream | Upstream |
|---------|------------|----------|
| ADSL | 6 Mbps | 1.5 Mbps |
| ADSL2+ | 24 Mbps | 3.5 Mbps |
| VDSL2 | >100 Mbps | ~50 Mbps |

### PON Technologies

| Technology | Down/Up | Notes |
|------------|---------|-------|
| **GPON** | **2.5/1 Gbps** | **Most common** |
| EPON | 1/1 Gbps | Ethernet native |
| XGS-PON | 10/10 Gbps | Next-gen |

### Cellular Generations

| Gen | Technology | Access | Speed | Key Feature |
|-----|------------|--------|-------|-------------|
| **1G** | Analog | FDMA | Voice | Analog voice only |
| **2G** | Digital | TDMA | ~384 kbps | GSM, GPRS, EDGE |
| **3G** | Digital | CDMA | 2-56 Mbps | UMTS, HSPA |
| **4G** | Digital | OFDMA | ~250 Mbps | LTE, All-IP |

---

## ⚠️ COMMON EXAM TRAPS

### Trap 1: Fiber vs Twisted Pair
**WRONG:** "Twisted pair has higher bit rate than fiber"  
**RIGHT:** "Fiber has much higher bit rate (Tbps vs Gbps)" ✓

### Trap 2: Manchester Bit Rate
**WRONG:** "Manchester encoding same bit rate as data"  
**RIGHT:** "Manchester requires 2× bit rate" ✓

### Trap 3: ADSL Symmetry
**WRONG:** "ADSL has symmetric speeds"  
**RIGHT:** "ADSL is asymmetric (higher downstream)" ✓

### Trap 4: PON Active/Passive
**WRONG:** "PON has powered devices in distribution network"  
**RIGHT:** "PON is passive (unpowered devices)" ✓

### Trap 5: Cellular Access Methods
**WRONG:** "All cellular uses TDMA"  
**RIGHT:** "1G=FDMA, 2G=TDMA, 3G=CDMA, 4G=OFDMA" ✓

### Trap 6: Fading vs Shadowing
**WRONG:** "Fading is slow variation"  
**RIGHT:** "Fading is fast, shadowing is slow" ✓

### Trap 7: OLT Location
**WRONG:** "OLT at user premises"  
**RIGHT:** "OLT at central office; ONT at premises" ✓

---

## 📊 EXAM WEIGHT DISTRIBUTION

### HIGH PRIORITY (Study thoroughly - 50%):
- ✅ Twisted pair categories and speeds
- ✅ Fiber optic advantages and attenuation
- ✅ Manchester encoding (2× bit rate)
- ✅ DSL types and speeds
- ✅ Cellular generations (1G-4G)
- ✅ Access methods (FDMA, TDMA, CDMA, OFDMA)

### MEDIUM PRIORITY (Understand well - 30%):
- Line coding types (unipolar, polar, bipolar)
- Digital modulation (QAM, PSK, FSK)
- PON components (OLT, ONU, ONT)
- GPON vs EPON specs
- Radio propagation (fading, shadowing)
- ADSL vs VDSL

### LOW PRIORITY (Brief review - 20%):
- Coaxial cable details
- Submarine cables
- nBmB coding efficiency
- DSLAM function
- FTTH vs FTTCab
- MIMO in LTE

---

## 🎓 STUDY STRATEGY

### Day 1: Transmission Media
- Three types: Electrical, Optical, Radio
- Twisted pair categories (focus on 5e, 6, 6a)
- Fiber advantages and windows
- Radio propagation basics

### Day 2: Encoding Techniques
- Line coding types
- Manchester = 2× bit rate
- Digital modulation basics
- nBmB coding

### Day 3: Access Technologies
- DSL family (ADSL, VDSL)
- MODEM and DSLAM
- PON technologies (GPON, EPON)
- FTTH vs FTTCab

### Day 4: Cellular Networks
- Four generations (1G to 4G)
- Access methods for each
- Key features and speeds
- Evolution timeline

### Day 5: Practice & Review
- Compare all media types
- Review common traps
- Flashcard drill
- Practice calculations

---

## 📝 QUICK REFERENCE FLASHCARDS

**Q:** Cat 5e supports?  
**A:** 1 Gbps

**Q:** Cat 6a supports?  
**A:** 10 Gbps

**Q:** Best fiber window?  
**A:** Third (1550 nm, 0.2 dB/km)

**Q:** Manchester bit rate?  
**A:** 2× data rate

**Q:** ADSL downstream?  
**A:** 6-24 Mbps (version dependent)

**Q:** GPON speeds?  
**A:** 2.5 Gbps down / 1 Gbps up

**Q:** OLT location?  
**A:** Central office

**Q:** ONT location?  
**A:** User premises

**Q:** 1G access method?  
**A:** FDMA

**Q:** 2G standard?  
**A:** GSM (with TDMA)

**Q:** 3G access method?  
**A:** CDMA

**Q:** 4G access method?  
**A:** OFDMA

**Q:** LTE stands for?  
**A:** Long Term Evolution

**Q:** Fading: fast or slow?  
**A:** Fast (shadowing is slow)

**Q:** MODEM stands for?  
**A:** MOdulator/DEModulator

---

**END OF CHAPTER 4: PHYSICAL LAYER**

**Status:** ✅ Complete - Ready for exam preparation  
**Importance:** ⭐⭐ MEDIUM PRIORITY - 10-12% of exam  
**Next Chapter:** Data Link Layer

