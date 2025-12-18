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
	- Uses IP and Port numbers
- **Sender side:** Receives message from App layer → Breaks message into segments → Passes to Network layer [[TransportLayer 1.pdf#page=14|L5 page 14]]
- **Receiver side:** Receives segments from Network layer → Reassembles segments to message → passes to App layer [[TransportLayer 1.pdf#page=14|L5 page 14]]
- Most common protocols on internet: TCP and UDP [[TransportLayer 1.pdf#page=14|L5 page 14]]

## UDP
- Must have:
	- Breaking messages into segments: **Yes**
	- Multiplexing/demultiplexing: **Yes**
- Connection management: Connectionless communication (doesn't establish channel before sending segments)
- Reliable data transfer: **No ("best effort")**
	- Error Detection: Checksum
	- Error recovery: No
	- In order delivery No
- Timing: None
- Throughput: No
	- Flow control: None
	- Congestion Control: None
- Security: None
- UDP Header [[TransportLayer 1.pdf#page=19|L5 page 19]]
	- Source port: Socket of sender (16 bits)
	- Destination Port: Socket of receiver (16 bits)
	- Length: Length, in bytes, of UDP segment, including header (16 bits)
	- Checksum (16 bits)

## TCP
- Must have:
	- Breaking messages into segments: **Yes**
	- Multi-/demultiplexing: **Yes**
- Connection management: Connection-oriented communication (establishes connection bfore sending segments)
- Reliable data transfer: **Yes**
	- Error detection: Checksum
	- Error recovery: Yes
	- In order deliver: Yes
- Timing: None
- Throughput: No
	- Flow control: Yes
	- Congestion control: Yes
- Security: None
- Point-to-point (one sender, one receiver) [[TransportLayer 1.pdf#page=24|L5 page 24]]
- Reliable