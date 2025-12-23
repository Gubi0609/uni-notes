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
		- Control plane: e.g. ICMP
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
- _Lookup forwarding queuing_ [[07 - NetworkLayerDataPlane.pdf#page=18|L8 page 18]]
	- Decentralized switching
		- Using **header field** values, _lookup_ output port using forwarding table in input port memory ("_match plus action_")
		- **Goal**: Complete input port processing at 'line speed'
		- Queuing occurs of datagrams arrive faster than forwarding rate into switch fabric
		
		- _Destination-based forwarding:_ forward based only on destination IP address (**traditional**) [[07 - NetworkLayerDataPlane.pdf#page=19|L8 page 19]]
		- _Generalized forwarding:_ forward based on _any set_ of header field values[[07 - NetworkLayerDataPlane.pdf#page=19|L8 page 19]]

**Destination-based forwarding** [[07 - NetworkLayerDataPlane.pdf#page=20|L8 page 20]]
- Has a _forwarding table_ with destination address ranges and corresponding link interfaces
- Example:
	- 11001000 00010111 00010**00