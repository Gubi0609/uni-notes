
# Relevant Lectures
- [[L3 - The Application layer 1]]
- [[L4 - The Application layer 2 (DNS)]]

# Relevant Themes
- OSI model [[L1 - Introduction]]
- Application: Supporting network applications [[TheApplicationLayer_I.pdf]]
- Protocols
	- Examples for different applications [[TheApplicationLayer_I.pdf#page=11]]
- Surrounding layers and API
	- None above
	- Transport below (according to IP stack) [[TheApplicationLayer_I.pdf#page=4|TheApplicationLayer_I page 4]]
		- Sockets [[TheApplicationLayer_I.pdf#page=7]]
	- Presentation below (according to OSI)) [[Intro.pdf#page=33|Intro page 33]]
- Hosts the application (Webpage, Program, E-mail. P2P file, VoIP etc.)
- Architectures [[TheApplicationLayer_I.pdf#page=13]]
	- Client-Server
		- Server: Always on host, permanent IP dresss, Data centers for scaling [[TheApplicationLayer_I.pdf#page=14|L3 page 14]]
		- Client: Communicate with server, maybe intermittently connected, dynamic IP, not direct P2P communication (always Client-Server-Client)
	- P2P
		- _Not_ always on server, different end systems communicate directly, Peers request from other peers (provides service to other peers in return) **Self scalability**, dynamic IP adresses and intermittently connected peers. [[TheApplicationLayer_I.pdf#page=15|L3 page 15]]
	- Publisher-Subscriber (IoT)
		- Register _Topic_ at _Message Broker_. Example MQTT (used by ROS i think)
			- Lightweight and efficient
			- Scalable
			- Bi-directional Communication
		- [[TheApplicationLayer_I.pdf#page=17|L3 page 17]]
	- Cloud
		- Decentralized "virtual" srver, dynamic resource management, scalable, complex [[TheApplicationLayer_I.pdf#page=16|L3 page 16]]
- 