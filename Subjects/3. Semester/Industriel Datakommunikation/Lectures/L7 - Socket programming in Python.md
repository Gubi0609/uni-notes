
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
serverPort = 12345

clientSocket = socket(AF_INET, SOCK_DGRAM)
message = input("Input lowercase sentence: ")
clientSocket.sendto(message.encode(),(serverName, serverPort))

modifiedMessage, serverAddress = clientSocket.recvfrom(2048)
print(modifiedMessage.decode())

clientSocket.close()
```

![[Pasted image 20251020090428.png]]


---
#lecture 