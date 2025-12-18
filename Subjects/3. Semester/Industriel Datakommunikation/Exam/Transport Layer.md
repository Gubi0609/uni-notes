# Relevant Lectures
- [[L3 - The Application layer 1]] more specifically [[TheApplicationLayer_I.pdf#page=24|page 24]] to [[TheApplicationLayer_I.pdf#page=28|page 28]]
- [[L5 - The Transport layer 1]]
- [[L6 - The Transport layer 2]]

# Relevant Materials
- L5: p. 215 - 289
- L6: p. 286 - 314

# Relevant Themes
- Surrounding layers [[TransportLayer 1.pdf#page=7|L5 page 7]]
	- Upper: _Socket_ to Application Layer. Sends and delivers messages through socket
	- Lower: Sends and receives segments to and from remote host
- Packets at this level is called **Segments** [[TransportLayer 1.pdf#page=7|L5 page 7]]
- What transport service does an app need? [[TransportLayer 1.pdf#page=10|L5 page 10]]
	- Reliable data transfer
	- Timing
	- Throughput
	- Security
- What can be expected of Transport Layer? [[TransportLayer 1.pdf#page=11|L5 page 11]]
	- Must haves:
		- Breaking messages into _segments_.
		- Multiplexing/demultiplexing
	- Connection management
	- Reliable data transfer
		- Error detection and recovery
		- In order delivery (packet1, packet2, ... )
	- Timing
	- Throughput
		- Flow control
		- Congestion control
	- Security
- In contrast to Network Layer (that focuses on communication between hosts), Transport Layer focuses on communication between _processes_ [[TransportLayer 1.pdf#page=12|L5 page 12]]