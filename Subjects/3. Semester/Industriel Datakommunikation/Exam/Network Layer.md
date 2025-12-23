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
	- Sends and receives _datagrams_ to/from other layer 3 (Neto)