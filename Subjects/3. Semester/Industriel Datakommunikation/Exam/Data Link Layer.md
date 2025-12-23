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

- **Framing, link access:** Encapsulates datagram into frame, adding _header_ and _trailer_ [[0]]
- Channel access if shared medium
- **MAC** (**M**edia **A**ccess **C**ontrol) adresses used in frame headers to identify source and destination _nodes_
	- **Different from IP address**
	- 