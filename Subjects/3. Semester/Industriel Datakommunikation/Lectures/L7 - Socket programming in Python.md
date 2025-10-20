
---
**Date:** 2025-10-20

## Preparation

>[!TODO] HOMEWORK
>- [ ] 

> [!DANGER] EXERCISES
> - [ ] 

> [!QUESTION] Questions
> - 

---
# Relevant documents


# Topics


# Notes
## Python lab 2

`UDPClient.py`
```python
from socket import *

serverName = "10.126.58.94" # IP Adress of server (in this case Elias' computer)
serverPort = 12345 # Port of server

clientSocket = socket(AF_INET, SOCK_DGRAM)
message = input("Input lowercase sentence: ")
clientSocket.sendto(message.encode(),(serverName, serverPort))

modifiedMessage, serverAddress = clientSocket.recvfrom(2048)
print(modifiedMessage.decode())

clientSocket.close()
```

`UDPServer.py`
```python
from socket import *

serverName = "0.0.0.0" # Lyt på alle aktive netværker (på egen computer altså)
serverPort = 8888

serverSocket = socket(AF_INET, SOCK_DGRAM)
serverSocket.bind((serverName, serverPort))
print("The server is ready to receive!")

while True:
	message, clientAddress = serverSocket.recvfrom(2048)
	print("Received message: ", message)
	modifiedMessage = message.decode().upper()
	print("Modified message: ", modifiedMessage)
	serverSocket.sendto(modifiedMessage.encode(), clientAddress)
```

Jeg kørte både client og server koden samtidigt og kommunikerede med Elias' computer. Her kan ses resultatet af kommunikationen.
Vi kan se at først har Elias sendt mig en besked fra IP 10.126.58.94 (port 51375) og min server svarer tilbage til samme IP og port.
Elias sender mig så endnu en besked fra en ny port (port 60937) og jeg svarer igen tilbage til den samme port.

Dernæst sender jeg Elias en besked fra IP 10.126.110.119 (port 56323) og han svarer tilbage til samme IP og port.
![[Pasted image 20251020090428.png]]

Vi kan her se min besked til Elias (packet 387)
![[Pasted image 20251020091026.png]]

Og hans svar
![[Pasted image 20251020091038.png]]


---
#lecture 