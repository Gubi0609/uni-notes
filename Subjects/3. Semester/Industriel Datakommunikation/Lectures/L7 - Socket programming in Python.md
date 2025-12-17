
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
[[PythonLab2.pdf]]
[[Python Lab 3.pdf]]

# Topics


# Notes
## Python lab 2

### UDP

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

### TCP

`TCPClient.py`
``` python
from socket import *

serverName = "10.126.58.94"
serverPort = 12345

clientSocket = socket(AF_INET, SOCK_STREAM)
clientSocket.connect((serverName,serverPort))

sentence = input("Input lowercase sentence: ")
clientSocket.send(sentence.encode())

modifiedSentence = clientSocket.recv(1024)
print("From Server: ", modifiedSentence.decode())

clientSocket.close()
```

`TCPServer.py`
``` python
from socket import *

serverName = "0.0.0.0"
serverPort = 8888

serverSocket = socket(AF_INET,SOCK_STREAM)
serverSocket.bind((serverName,serverPort))
serverSocket.listen(1)
print("The server is ready to receive")

while True:
	connectionSocket, addr = serverSocket.accept()
	sentence = connectionSocket.recv(1024).decode()
	print("Received message: ", sentence)
	capitalizedSentence = sentence.upper()
	connectionSocket.send(capitalizedSentence.encode())
	print("Sent message: ", capitalizedSentence)
	connectionSocket.close()
```


Vi kan her se en forbindelse hvor Elias sender til min computer.
Der er 3 kommunikationer/beskeder før hans aktuelle besked bliver sendt. Først en SYN fra ham, så en SYN, ACK fra mig, og dernæst en ACK fra ham.
Først efter det kommer hans besked med en **PSH**, ACK. Jeg sender en ACK for at bekræfte at jeg har modtaget den, og dernæst **PSH**, ACK for at sende min besked tilbage.
Efter det sender jeg en FIN for at lukke forbindelsen og der bliver sendt nogle ACK og FIN frem og tilbage for at bekræfte.
![[Pasted image 20251020093018.png]]

Her kan vi se Elias' besked til mig
![[Pasted image 20251020093545.png]]

Og her er mit svar
![[Pasted image 20251020093558.png]]


### Part 3
Man skal ændre hvad man svarer tilbage med (fx at tælle antal tegn i modtaget besked), men det er simpelthen alt for nemt til at jeg gider.

## Python lab 3


---
#lecture 