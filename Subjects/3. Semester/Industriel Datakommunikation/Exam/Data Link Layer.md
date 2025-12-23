# Relevant Lectures
- [[L10 - The Link Layer]]
# Relevant Materials
- L10: page 479-549

# Relevant Themes
- Focuses on _node_ to _node_ delivery [[09 - The Link Layer.pdf#page=2|L10 page 2]]
- Packages datagrams from Network Layer to _frames_ in Link Layer [[09 - The Link Layer.pdf#page=2|L10 page 2]]
- _Node_ is a _host_ or _router_ or _switch_ that  runs Layer 2 (Link Layer) protocol [[09 - The Link Layer.pdf#page=3|L10 page 3]]
- _Links_ are communication channels, that connect neighbor nodes along communication path [[09 - The Link Layer.pdf#page=3|L10 page 3]]
	- Wired or Wireless Links
	- LANs
- Layer-2 packet is a _frame_
- **Data-Link Layer has responsibility of transferring datagrams from one node to _physically adjacent_ node over a link** [[09 - The Link Layer.pdf#page=3|L10 page 3]]

- Datagram may be transferred by _different link protocols_ over _different links_ [[09 - The Link Layer.pdf#page=4|L10 page 4]]
	- E.g. Ethernet on first link, frame realy on intermediate links, WiFi on last link
- Each link protocol provides different services
	- E.g. may or may not provide RDT (**R**eliablie **D**ata **T**ransfer) over link

- **Framing, link access:** Encapsulates datagram into frame, adding _header_ and _trailer_ [[09 - The Link Layer.pdf#page=5|L10 page 5]]
- Channel access if shared medium
- **MAC** (**M**edia **A**ccess **C**ontrol) adresses used in frame headers to identify source and destination _nodes_
	- **Different from IP address**
- **Reliable delivery between adjacent nodes** [[09 - The Link Layer.pdf#page=5|L10 page 5]]
	- Seldom used on low bit-error link (e.g. fiber or some twisted pair)
	- Wireles has _high_ error rates

**Link layer services** [[09 - The Link Layer.pdf#page=6|L10 page 6]]
- **Flow control**
	- Pacing between adjacent sending and receiving nodes
- **Error detection**
	- Errors caused by signal attenuation, noise
	- Receiver detects presence of errors and _signals sender for retransmission or drops frame_
- **Error correction**
	- Receiver identifies and correct bit error(s) without resorting to retransmission (2D parity bits (Hamming Codes))
- **Half-duplex and full-duplex**
	- With half-duplex nodes at both ends of link can transmit but not at same time. With full-duplex can do at same time

Link layer is implemented in each and every host and router.
Implemented in _adapter_ [[09 - The Link Layer.pdf#page=7|L10 page 7]]
- Network Interface Card (**NIC**) or on a chip
	- Ethernet card, 802.11 card; Ethernet chipset
	- Implements Link **AND** physical layer
- Attaches into host's system buses
- Combination of hardware, software, firmware.
- All upper layers are handled by CPU, which communicates with **NIC**, which transmits to network

- **Sending side NIC** [[09 - The Link Layer.pdf#page=8|L10 page 8]]
	- Encapsulates datagram in _frame_
	- Adds error checking bits, RDT, flow control etc
- **Receiving side NIC** [[09 - The Link Layer.pdf#page=8|L10 page 8]]
	- Looks for errors, RDT, flow control etc.
	- Extracts datagram, passes to upper layer at receiving side

## Error detection and correction
**EDC** (**E**rror **D**etection and **C**orrection bits) (redundancy)
**D** is **D**ata protected by error checking. May include _header fileds_

==Error detection is not 100% reliable== [[09 - The Link Layer.pdf#page=10|L10 page 10]]
- Larger EDC field yields better detection and correction

### Parity checking [[09 - The Link Layer.pdf#page=11|L10 page 11]]
**Single bit parity**
- Detects single bit errors
- One bit is appended, to set _even_ number of **1**'s

**Two-dimensional bit parity**
- Detects _and_ corrects single bit errors
- Detects even number of bit errors, but does not correct
- For 16 bit _frame_ 11 bits are **Data** and 5 bits are **EDC**

**Used for Serial links (UART, RS-232), as not so error prone** [[09 - The Link Layer.pdf#page=12|L10 page 12]]

### CRC [[09 - The Link Layer.pdf#page=12|L10 page 12]]
- Also see [[CRC]] page for self-written explanation of it
- Used for Ethernet and Wireless (Wifi, 4G/5G), as prone to _burst errors_
	- Wireless also uses **FEC** (**F**orward **E**rror **C**orrection)
	- The costiler the retransmission, the stronger FEC method is justified


## MAC and ARP
**MAC** (Multi Access Control)
**ARP** (Address Resolution Protocol)

- **Broadcast** (shared wire or medium (e.g. Wifi)) [[09 - The Link Layer.pdf#page=14|L10 page 14]]
- Core problem:
	- Single shared broadcast channel
	- Two or more simultaneous transmissions by nodes → **Inteference**
		- **Collision** if node receives two or more signals at the same time

IP address is used for forwarding and routing in _Network Layer_
**MAC** (or LAN or physical or Ethernet) address is: [[09 - The Link Layer.pdf#page=15|L10 page 15]]
- Used **locally** to get frame from one _interface_ to another **physically connected** interface (same network in IP-addressing sense)
- 48-bit MAC address burned in **NIC** ROM, also sometimes software settable
- Represented in base 16. E.g. 1A-2F-BB-76-0-AD

_Each_ adapter (NIC for example) on **LAN** (**L**ocal **A**rea **N**etwork) has _unique_ LAN address [[09 - The Link Layer.pdf#page=16|L10 page 16]]

MAC address allocation administered by IEEE (**I**nstitute of **E**lectrical and **E**lectonics **E**ngineers) [[09 - The Link Layer.pdf#page=17|L10 page 17]]
- Manufacturer buys portion of MAC address space (to ensure uniqueness)

_Both_ IP and MAC are needed, as they serve different purposes. IP is used to route through the network, while MAC is used to communicate between nodes
MAC is also **STATIC** so it is like Social Security Number, while IP is **DYNAMIC** like postal address (based on your current location) [[09 - The Link Layer.pdf#page=17|L10 page 17]]

### ARP
Each IP node on LAN has **ARP table** [[09 - The Link Layer.pdf#page=18|L10 page 18]]
- IP/MAC mapping for some LAN nodes
	- **<