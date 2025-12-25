# Relevant Lectures
- [[L8 - The Network Layer 1]]
- [[L9 - The Network Layer 2]]

# Relevant Materials
- L8: page 333-389
- L9: page 407-467

# Relevant Themes
- Protocol/Role at **host** [[07 - NetworkLayerDataPlane.pdf#page=7|L8 page 7]]
	- Retrieves and delivers _segments_ from/to Transport Layer
	- Comply with network layer protocols
		- Data plane: IP (IPv4, IPv6)
		- Control plane: e.g. ICMP (error reporting, router "signaling")
	- Sends and receives _datagrams_ to/from other layer 3 (Network Layer) devices through the Link Layer
- Protocol/Role at **router** [[07 - NetworkLayerDataPlane.pdf#page=8|L8 page 8]]
	- Comply with network layer protocols
		- Data plane: IP (IPv4, IPv6)
		- Control  plane: e.g. ICMP
	- Sends and receives _datagrams_ to/from other layer 3 (Network Layer) devices through the Link Layer
	- Forward datagrams from one interface (physical port) to another
	- Route datagrams to the "right" interface

**Overall Role of Network Layer** [[07 - NetworkLayerDataPlane.pdf#page=9|L8 page 9]]
- Transport _segments_ from sending to receiving host
- On **sending** side, encapsulates segments into _datagrams_
- On **receiving** side, delivers segments to Transport Layer
- Network Layer protocols in _every_ host and router
- Router examines **header fields** in _all_ IP datagrams passing through it

- **Forwarding** is moving packets from router's input to appropriate router output [[07 - NetworkLayerDataPlane.pdf#page=10|L8 page 10]]
- **Routing** determines route taken by packets from source to destination [[07 - NetworkLayerDataPlane.pdf#page=10|L8 page 10]]
- Like taking a trip. _Forwarding_ is the current intersection, _Routing_ is the planning of the trip

**Data plane** [[07 - NetworkLayerDataPlane.pdf#page=11|L8 page 11]]
- Local, per-router function
- Determines how datagram arriving on router input port is forwarded to router output port
- _Forwarding_ function

**Control plane** [[07 - NetworkLayerDataPlane.pdf#page=11|L8 page 11]]
- Network-wide logic
- Determines how datagram is routed among routers along E2E path from source host to destination host
- Two approaches:
	- _Traditional routing algorithms:_ Implemented in routers
		- Individual routing algorithm components in _each and every router_ interact in the control plane [[07 - NetworkLayerDataPlane.pdf#page=12|L8 page 12]]
	- _Software-defined networking (SDN):_ Implemented in (remote) servers
		- A distincrt (typically remote) controller interacts with local controls agents (CAs) [[07 - NetworkLayerDataPlane.pdf#page=13|L8 page 13]]

- Could be great with lots of guarantees (delivery, bounded delay etc.), but is **Best-effort service** [[07 - NetworkLayerDataPlane.pdf#page=14|L8 page 14]]

## The router
- Has a _forwarding data plane_ (hardware) which operates in nanosecond timeframe [[07 - NetworkLayerDataPlane.pdf#page=17|L8 page 17]]
	- Router _input_ ports
	- High-speed _switching fabric_
	- Router _output_ ports
- Has a _routing, management control plane_  (software) which operates in millisecond timeframe [[07 - NetworkLayerDataPlane.pdf#page=17|L8 page 17]]
	- _Routing processor_. Communicates with switching fabric

### Input port
- _Line termination_ [[07 - NetworkLayerDataPlane.pdf#page=18|L8 page 18]]
	- Physical layer: bit-level reception
- _Link layer protocol (receive)_ [[07 - NetworkLayerDataPlane.pdf#page=18|L8 page 18]]
	- Data Link Layer: e.g. Ethernet
- _Lookup, forwarding, queuing_ [[07 - NetworkLayerDataPlane.pdf#page=18|L8 page 18]]
	- Decentralized switching
		- Using **header field** values, _lookup_ output port using forwarding table in input port memory ("_match plus action_")
		- **Goal**: Complete input port processing at 'line speed'
		- Queuing occurs if datagrams arrive faster than forwarding rate into switch fabric
		
		- _Destination-based forwarding:_ forward based only on destination IP address (**traditional**) [[07 - NetworkLayerDataPlane.pdf#page=19|L8 page 19]]
		- _Generalized forwarding:_ forward based on _any set_ of header field values[[07 - NetworkLayerDataPlane.pdf#page=19|L8 page 19]]

**Destination-based forwarding** [[07 - NetworkLayerDataPlane.pdf#page=20|L8 page 20]]
- Has a _forwarding table_ with destination address ranges and corresponding link interfaces
- Example:
	- 11001000 00010111 00010**00 00000000** through 11001000 0010111 00010**111 11111111** goes to Link Interface **0**
	- 11001000 00010111 00011000 **00000000** through 11001000 00010111 00011000 **11111111** goes to Link Interface **1**
	- 11001000 00010111 00011001 **00000000** through 11001000 00010111 00011111 **11111111** goes to Link Interface **2**
	- Otherwise Link Interface **3**

- To increase speed (i think?) when looking for forwarding table entry for given destination address, use _longest_ address prefix, that matches destination address. [[07 - NetworkLayerDataPlane.pdf#page=21|L8 page 21]]
- Example: We have the following Destination Address Ranges (with the # representing the variables within that range)
	- 11001000 00010111 00010### ######## to link interface **0**
	- 11001000 00010111 00011000 ######## to link interface **1**
	- 11001000 00010111 00011## ######## to link interface **2**
	- Otherwise link interface **3**
- The following inputs are given, and must go the _longest_ address prefix, that matches
	- 11001000 00010111 00010**110 10100001** goes to interface **0** because it has the _longest_ matching prefix
	- 11001000 00010111 00011**000 10101010** goes to interface **1** because it has the _longest_ matching prefix. Notice, that interface **2** ALSO matches, but since interface **1** has a longer prefix, that is chosen.

### Switching fabrics
- Three types of _switching fabrics_ [[07 - NetworkLayerDataPlane.pdf#page=22|L8 page 22]]
	- Transfers packets from input buffer to appropriate output buffer
	- Switching rate is rate at which packets can be transferred from input to output
	- **Memory switching**
	- **Bus switching**
	- **Crossbar switching**
- Input port queuing occurs if switching fabric is slower than input ports _combined_ [[07 - NetworkLayerDataPlane.pdf#page=23|L8 page 23]]
	- Queuing delay and *loss* due to input buffer overflow
- Head of the Line (HOL) blocking occurs when a datagram at front of queue prevents others in queue from moving forward
	- Eg. Port 1 and 3 both have **red** datagram, for **red** output port. The cannot both do it at the same time, so port 1 goes first. Now port 3 has both a **red** and a **green** datagram, but the **green** can't reach its output port before **red** datagram is removed.

### Output ports [[07 - NetworkLayerDataPlane.pdf#page=24|L8 page 24]]
- _Datagram buffer, queuing_
	- **Buffering** is required when datagrams arrive from fabric _faster_ than the transmission rate
		- Datagrams can be lost due to congestion/lack of buffers
- _Link layer protocol (send)_
	- **Scheduling discipline** chooses among queued datagrams for transmission
		- Priority scheduling: Who gets best performance?
- _Line termination_

- Scheduling chooses next packet to send on link [[07 - NetworkLayerDataPlane.pdf#page=25|L8 page 25]]
- **FIFO** scheduling: Send in order of arrival to queue
	- Discard policy: If packets arrive to full queue, who to discard?
	- **Tail drop:** drop arriving packet
	- **Priority:** drop/remove on priority basis
	- **Random:** drop/remove randomly

## Internet Protocol Addressing
**IP datagram format** [[07 - NetworkLayerDataPlane.pdf#page=28|L8 page 28]]
- Length of words = 32 bits
- IP protocol version number
- Header length (number of 32 bit words)
- Type of service (type of data)
- Length (total datagram length (bytes))
- 16-bit identifier **For fragmentation/reassembly**
- Flags **For fragmentation/reassembly**
- Fragment offset **For fragmentation/reassembly**
- TTL (max number of remaining hops. Decremented at _each_ router)
- Upper layer protocol to deliver payload to (TCP/UDP/...)
- Header checksum (16 bits)
- 32 bit source IP address
- 32 bit destination IP address
- Options (if any)
	- E.g Timestamp, record route taken, specify list of routers to visit

_With 20 bytes of TCP overhead and 20 bytes of IP overhead total overhead is ==40 bytes!== + App Layer overhead_

- If a large datagram is sent, it can be split into smaller diagrams. Through the _whole_ transfer process, they are kept small, and _only_ reassembled at **final destination**. [[07 - NetworkLayerDataPlane.pdf#page=29|L8 page 29]]
	- Network links have MTU (max transfer size) = largest possible link-level frame
	- Different link types - Different MTUs
- IP header bits used to identify order related fragments


- _Interface_ is the connection between host/router and physical link
	- Routers typically have _multiple_ interfaces
	- Hosts typically has _one or two_ interfaces (e.g. Wired Ethernet, wireless 802.11)
- **IP addresses associated with each interface**
	- Hosts connected to same router will have similar IP

- Devices on same _subnet_ can physically reach each other _without intervening router_ [[07 - NetworkLayerDataPlane.pdf#page=33|L8 page 33]]
	- Eg. Devices in the same house will be able to communicate with each other without needing to reach residential router
- To determine subnets, detach each interface from its host or router, creating islands of isolated networks [[07 - NetworkLayerDataPlane.pdf#page=34|L8 page 34]]
	- Each isolated network is called a _subnet_

- **CIDR** (**C**lassless **I**nter**D**omain **R**outing) [[07 - NetworkLayerDataPlane.pdf#page=35|L8 page 35]]
	- Subnet portion of address of arbitrary length
	- Address format: _a.b.c.d/x_ where _x_ is number of bits in subnet portion of address
		- Example: **11001000 00010111 0001000**0 00000000
			- 200.23.16.0/**23** because 23 bits (the bold part) is the subnet part, whereas the normal part is the host part
- Can have $2^x$ subnets, because we operate in binary. So for subnet mask /16, number of subnets is $2^{16}=65536$. [[07 - NetworkLayerDataPlane.pdf#page=36±L8 page 36]]

**How to get IP address** [[07 - NetworkLayerDataPlane.pdf#page=37|L8 page 37]]
- Hard-coded by system admin in a file (static IP. Typically for servers I think)
- DHCP (**D**ynamic **H**ost **C**onfiguration **P**rotocol): Dynamically get address from server [[07 - NetworkLayerDataPlane.pdf#page=38|L8 page 38]]
	- **Goal:** Allow host to _dynamically_ obtain its IP address from network server when it joins network
		- Can renew its "lease" on address in use
		- Allows reuse of addresses (only hold address while connected/"on")
		- Support for mobile users who want to join network
- DHCP _protocol_ [[07 - NetworkLayerDataPlane.pdf#page=38|L8 page 38]]
	- Host broadcasts _"DHCP discover"_ msh (optional)
		- _Is there a DHCP server out there?_
	- DHCP server respondes with _"DHCP offer"_ msg (optional)
		- _Yes, that is me_
	- Host requests IP address _""DHCP request"_ msg
		- _Do you have an available IP address?_
	- DHCP server sends address _"DHCP ack"_ msg
		- _Yes, here is an available IP address for you_
- DHCP can also return _more_ than just IP addresses [[07 - NetworkLayerDataPlane.pdf#page=40|L8 page 40]]
	- Address of first-hop router for client
	- Name and IP address of DNS server
	- Network Mask (indicating network versus host portion of address (_a.b.c.d/x_))
- A _network_ gets the subent part of its IP address from _ISP_'s address space [[07 - NetworkLayerDataPlane.pdf#page=41|L8 page 41]]
- An _ISP_ gets block of addresses from **ICANN** (**I**nternet **C**orporation for **A**ssigned **N**ames and **N**umbers)

## NAT
- NAT: **N**etwork **A**ddress **T**ranslation
- Translation for _local_ network (e.g. home network) [[07 - NetworkLayerDataPlane.pdf#page=44|L8 page 44]]
- _All_ datagrams _leaving_ local network have _same_ single source NAT IP address [[07 - NetworkLayerDataPlane.pdf#page=44|L8 page 44]]
	- Different source port numbers
	- Datagrams with source or destination in this network have _a.b.c.d/x_ address for source and destination (as usual)
- **Motivation:** Local network uses just _one_ IP address as far as outside world is concerned [[07 - NetworkLayerDataPlane.pdf#page=45|L8 page 45]]
	- Range of addresses not needed from ISP. Just one IP address for all devices
	- Can change addresses of devices in local network without notifying outside world
	- Can change ISP without changing addresses of devices in local network
	- Devices inside local network not explicitly addressable, visible by outside world (extra security)
- **Implementation** Every NAT router must: [[07 - NetworkLayerDataPlane.pdf#page=46|L8 page 46]]
	- _Outgoing datagrams:_ **Replace** source IP address, port # of EVERY outgoing datagram to NAT IP address, new port #
	- _Remember (in NAT translation table)_ every source IP address, port # to NAT IP address, new port # translation pair
	- _Incoming datagrams:_ **Replace** NAT IP address, new port # in destination fields of every incoming datagram with corresponding source IP address, port # stored in NAT table
- **Nat is controversial** [[07 - NetworkLayerDataPlane.pdf#page=48|L8 page 48]]
	- Routers should only process up to layer 3 (Network Layer)
	- Address shortage should be solved by IPv6
	- Violates E2E argument
		- NAT possibility must be taken into account by app designers e.g. P2P applications
- **Port forwarding** can be used to access hosts within NAT network from outside the network
	- E.g. running a web-applications on a home network. Can be accessed from static IP using port forwarding

## IPv6
- **Motivation** [[07 - NetworkLayerDataPlane.pdf#page=50|L8 page 50]]
	- 32-bit address space completely allocated
	- Header format helps speed processing/forwarding
	- Header changes to facilitate QoS (Quality of Service)
- _IPv6 datagram format_ [[07 - NetworkLayerDataPlane.pdf#page=50|L8 page 50]]
	- Fixed-length 40 byte header
	- No fragmentation allowed
	- No checksum
	- No options
	
	- Version
	- _Priority:_ Identify priority among datagrams in flow
	- _Flow label:_ identify datagrams in same "flow" (concept of "flow" not well defined)
	- Payload length (length of payload)
	- _Next header:_ Identify upper layer protocol for data (in the payload)
	- Hop limit
	- Source address (128 bits)
	- Destination address (128 bits)
- _ICMPv6_ new version of ICMP [[07 - NetworkLayerDataPlane.pdf#page=50|L8 page 50]]
	- Additional message types e.g. "Packet Too Big"
	- Multicast group management functions

- Upgrading from IPv4 to IPv6 is _not_ easy [[07 - NetworkLayerDataPlane.pdf#page=52|L8 page 52]]
	- Not all routers can be upgraded simultaneously
- To operate network with _mixed_ IPv4 and IPv6 routers **tunneling** is used [[07 - NetworkLayerDataPlane.pdf#page=52|L8 page 52]]
	- IPv6 datagram carried as _payload_ in IPv4 datagram among IPv4 routers
	- Automatically packaged by IPv6 router when sending to IPv4 router. And unpacked again by IPv6 router when receiving from IPv4 router
- IPv6 has been 25 years (and counting) under way for deployment [[07 - NetworkLayerDataPlane.pdf#page=54|L8 page 54]]
	- Maybe because of outdated hardware, that is not capable of running IPv6, so IPv4 is still used on those

## Forwarding
- Per-router Control Plane [[07 - NetworkLayerDataPlane.pdf#page=56|L8 page 56]]
	- Each router has a _routing algorithm_ and it interacts with each and every router
- SDN [[07 - NetworkLayerDataPlane.pdf#page=57|L8 page 57]]
	- Each router contains a _flow table_ that is computed and distributed by a _logically centralized_ routing controller

## Control plane
- **Routing** determines route taken by packets from source to destination [[NetworkLayerControlPlane.pdf#page=4|L9 page 4]]
	- Two approaches:
	- _per router control_ (traditional)
	- _logically centralized control_ (software defined networking (**SDN**))
- **Goal:** Determine _good paths_ from sending hosts to receiving host through network of routers [[NetworkLayerControlPlane.pdf#page=5|L9 page 5]]

**Routing algorithm classifications** [[NetworkLayerControlPlane.pdf#page=8|L9 page 8]]
- _Global_
	- All routers have complete topology, link cost info
	- "Link state" (**LS**) algorithms
- _Decentralized_
	- Router knows physically-connected neighbors, link costs to neighbors
	- Iterative process of computation, exchange of info with neighbors
	- "Distance Vector" (**DV**) algorithms

- _Static_
	- Routes change _slowly_ over time
- _Dynamic_
	- routes change more _quickly_
		- Periodic updates
		- In response to link cost changes

### Dijkstra's Algorithm 
- Net topology, link costs known to _all_ nodes [[NetworkLayerControlPlane.pdf#page=9|L9 page 9]]
	- Accomplished via **LS** broadcast
	- All nodes have same info
- Computes _least cost paths_ from one node ('source') to _all other_ nodes
	- Gives _forwarding table_ for that node
- **Iterative**
	- After _k_ iterations, know least cost path to _k_ destinations

**Notation:** [[NetworkLayerControlPlane.pdf#page=9|L9 page 9]]
- *c(x,y)* link cost from node _x_ to _y_ = $\infty$ if not direct neighbors
- _D(v)_ current value of cost path from source to destination _v_
- *p(v)* predecessor node along path from source to _v_
- _N'_ set of nodes whose least cost path definitively known

**Basically, we start from one node, and check all neighbors. Then choose _least cost path_. Then check _new_ node and choose _least cost path_, that takes us _further_ from start node.**

###  Bellman-Ford equation (Dynamic Programming)
- A distance vector (DV) routing algorithm
- Let $d_x(y)$ be the least-cost path from _x_ to _y_ [[NetworkLayerControlPlane.pdf#page=13|L9 page 13]]
- Then $d_x(y)=min_v(c(x,v)+d_v(y))$ [[NetworkLayerControlPlane.pdf#page=13|L9 page 13]]
	- $min_v$ is minimum taken over all neighbors _v_ of _x_
	- $c(x,v)$ is cost from _x_ to neighbor _v_
	- $d_v(y)$ is least-cost from neighbor _v_ to destination _y_

I **think** that some $d_x(y)$ are known, and thus it's easier to choose a path, as you just have to find your way to _x_ that knows the shortest path to _y_

- **Iterative, asynchronous:** [[NetworkLayerControlPlane.pdf#page=15|L9 page 15]]
	- Each local iteration caused by:
	- Local link cost change
	- DV update message from neighbor
- **Distributed** [[NetworkLayerControlPlane.pdf#page=15|L9 page 15]]
	- Each node notifies neighbors only when its DV changes
	- Neighbors then notify _their_ neighbors **ONLY** if necessary

### Comparing LS and DV algorithms [[NetworkLayerControlPlane.pdf#page=18|L9 page 18]]
**Message complexity**
- **LS** with _n_ nodes, _E_ links, _O(nE)_ msgs sent
- **DV** exchange between neighbors _only_
	- Convergence time varies

**Speed of convergence**
- **LS** $O(n^2)$ algorithm as requires _O(nE)_ msgs
- **DV** convergence time varies
	- may be routing loops
	- count-to-infinity problem

**Robustness**: What happens if router malfunctions?
- **LS** node can advertise incorrect _link_ cost
	- each node computes its _own_ table
- **DV** node can advertise incorrect _path_ cost (black-holing)
	- Each node's table used by others
		- Error _propagate_ through network


## Intra Autonomous System Routing
As the communication of node changes would take up _very much_ real estate in the network, it would clog up communications

And with _billions_ of destinations, we can't store all destinations in routing tables [[NetworkLayerControlPlane.pdf#page=20|L9 page 20]]

**Administrative autonomy** [[NetworkLayerControlPlane.pdf#page=20|L9 page 20]]
- Internet = Network of networks
- Each network admin may want to control routing in its own network

- Routers are aggregated into regions know as **AS** (**A**utonomous **S**ystems) a.k.a. _domains_

**Intra AS routing** [[NetworkLayerControlPlane.pdf#page=21|L9 page 21]]
- Routing among hosts and routers in _same_ AS
- All routers in AS must run _same_ intra-domain protocol
- Routers in _different_ AS can run _different_ intra-domain routing protocol
- **Gateway router** at _edge_ of its own AS has link(s) to router(s) in other AS'es

**Inter AS routing** [[NetworkLayerControlPlane.pdf#page=21|L9 page 21]]
- Routing among AS'es
- **Gateway routers** perfrom inter-domain routing (_as well as_ intra-domain routing)


- Forwarding table configured by both intra- and inter-AS routing algorithm [[NetworkLayerControlPlane.pdf#page=22|L9 page 22]]


- Router in AS1 receives datagram destined outside AS1.
- **AS1 must** [[NetworkLayerControlPlane.pdf#page=23|L9 page 23]]
	- Learn which destinations are reachable through connected AS2 and AS3
	- Propagate this reachability info to _all_ routers in AS1

**Kind of like highways and islands I think**
- You come from _Vejle, Jylland_ and need to reach _København_ (example)
- Your local city tells you, you must take the highway to _Fyn_. 
- *Fyn* tells you, you must continue on highway towards _Sjælland_.
- _Sjælland_ knows, that _København_ is on its island, so it routes you towards _København_

### Intra-AS routing
- Also known as _interior gateway protocols (IGP)_
- Most common intra-AS routing protocols: [[NetworkLayerControlPlane.pdf#page=24|L9 page 24]]
	- **RIP** **R**outing **I**nformation **P**rotocol
		- Classic DV: DVs exchanged every 30 secs
		- No longer widely used
	- **EIGRP** **E**nhanced **I**nterior **G**ateway **R**outing **P**rotocol
		- DV based
		- Formerly Cisco-proprietary for decades (became open in 2013)
	- **OSPF** **O**pen **S**hortest **P**ath **F**irst
		- LS routing
		- IS-IS protocol (ISO standard, not RFC standard) essentially same as OSPF

**OSPF** [[NetworkLayerControlPlane.pdf#page=25|L9 page 25]]
- Open: _publically available_
- Uses LS algorithm (Dijktra)
	- Link state packet dissemination
	- Topology map at each node
	- Route computation using Dijktra's algorithm
- Router floods ESPF link-state advertisements to all other routers in _entire_ AS
	- Carried OSPF messages directly over IP (rather than TCP or UDP)
	- Link state for each attached link

Like everything else in networking, OSPF is hierarchical [[NetworkLayerControlPlane.pdf#page=26|L9 page 26]]
- Has _boundary_ router connected to
- _Backbone router(s)_ connected to
- _Area border router(s)_ connected to
- _Internal (area) routers_

### Inter-AS routing
- **BGP** (**B**order **G**ateway **P**rotocol) [[NetworkLayerControlPlane.pdf#page=28|L9 page 28]]
	- The de facto inter-domain routing protocol. _Glue that holds the Internet together_
- BGP provides AS a means to: [[NetworkLayerControlPlane.pdf#page=28|L9 page 28]]
	- Obtain subnet reachability information from neighboring AS'es (**eBGP** (external BGP))
	- Determine routes to other networks bas on reachability information and **policy**
	- Propagate reachability information to all AS-internal routers (**iBGP** (internal BGP))
- Allows subnets to advertise its existence to rest of Internet (**"I am here"**) [[NetworkLayerControlPlane.pdf#page=28|L9 page 28]]
	- IF IT WANTS TO

**Gateway routers run both eBGP and iBGP** as eBGP is used to communicate with _other_ AS'es and iBGP is used to communicate with routers in own AS. [[NetworkLayerControlPlane.pdf#page=29|L9 page 29]]
All routers in AS communicate with _each and every other_ router in AS using iBGP  [[NetworkLayerControlPlane.pdf#page=29|L9 page 29]]

### BGP basics [[NetworkLayerControlPlane.pdf#page=30|L9 page 30]]
- **BGP session:** two BGP routers (peers) exchange BGP messages over TCP
	- Advertising _paths_ to different destination network prefices
	- **BGP is a path vector protocol**
- When _AS3_ gateway router advertises path _AS3,X_ (route through AS3 to X) to _AS2_ gateway router
	- AS3 **promises** to AS2 it will forward datagrams towards _X_

BGP advertises attributes: _prefix + attributes = "route"_ [[NetworkLayerControlPlane.pdf#page=31|L9 page 31]]
- Prefix: destination
- Two important attributes:
	- **AS-PATH** list of AS'es through which prefix advertisements has passed
	- **NEXT-HOP** indicates specific internal-AS router to next-hop AS

**Policy-based routing** [[NetworkLayerControlPlane.pdf#page=31|L9 page 31]]
- Gateway receiving route advertisement uses**import policy** to accept/decline path (eg. never route through AS Y)
- AS policy also determines whether to **advertise** path to other neighboring AS'es

**BGP path advertisement** [[NetworkLayerControlPlane.pdf#page=32|L9 page 32]]
- AS2 gateway router receives path advertisement _AS3,X_ from AS3 gateway router
- Based on AS2 plicy, AS2 gateway router accepts path AS3,X and propagates to _all_ AS2 routers
- Based on AS2 policy, other AS2 gateway router advertises path _AS2, AS3, X_ to AS1 gateway router

Gateway router may learn about _multiple_ paths to destination [[NetworkLayerControlPlane.pdf#page=33|L9 page 33]]
- AS1 gateway router learns path _AS2, AS3, X_ from AS2 gateway router
- AS1 gateway router _also_ learns path _AS3, X_ from AS3 gateway router
- Based on policy, AS1 gateway router chooses path _AS3, X and advertises path within AS1_

A router in AS2 learns, it can route to X (an AS3) through either of its neighbors in AS2 [[NetworkLayerControlPlane.pdf#page=37|L9 page 37]]
- Chooses _local_ gateway that has _least_ intra-domain cost
- Doesn't worry about _inter-domain cost_

An ISP may only want to route traffic to/from its customer networks (does not want to carry transit traffic between other ISPs) [[NetworkLayerControlPlane.pdf#page=34|L9 page 34]]

### Different Intra-/Inter-AS routing [[NetworkLayerControlPlane.pdf#page=38|L9 page 38]]
**Policy**
- Inter-AS: Admin wants control over how its traffic routed, who routes through its net
- Intra-AS: Single admin, so no policy decisions needed

**Scale**
- Hierarchical routing _saves table size_, reduced update traffic

**Performance**
- Intra-AS can focus on performance
- Inter-AS policy may dominate over performance

