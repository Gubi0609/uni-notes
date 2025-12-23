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

- **Forwarding*