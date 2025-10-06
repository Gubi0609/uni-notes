
---
**Date:** 2025-10-06

## Preparation

>[!TODO] HOMEWORK
>- [ ] p. 286 - 314

> [!DANGER] EXERCISES
> - [ ] [[Wireshark_TCP_v8.1.pdf]]

> [!QUESTION] Questions
> - 

---
# Relevant documents
[[TCP_continued.pdf]]
[[Wireshark_TCP_v8.1.pdf]]

# Topics
[[Congestion control]]

# Notes
Det kan ses for et HTTP POST protokol i wireshark hvilke TCP pakker der indeholder filen, som man uploader:
![[Pasted image 20251006132942.png]]

Her ses de TCP pakker der står for handshake (31 og 32) samt den pakke, der begynder at sende filen. Vi kan se at det er den, der begynder at sende filen, fordi den har en længde på xxxx bytes
![[Pasted image 20251006133256.png]]

1. What is the IP address and TCP port number used by the client computer (source) that is transferring the alice.txt file to gaia.cs.umass.edu? To answer this question, it’s probably easiest to select an HTTP message and explore the details of the TCP packet used to carry this HTTP message, using the “details of the selected packet header window” (refer to Figure 2 in the “Getting Started with Wireshark” Lab if you’re uncertain about the Wireshark windows).
	1. Her kan ses TCP port nummeret på Source er 42600. Min IP adresse kan ses på billedet ovenover, hvor den er 10.126.105.132
	2. ![[Pasted image 20251006133456.png]]
2. What is the IP address of gaia.cs.umass.edu? On what port number is it sending and receiving TCP segments for this connection?
	1. IP adressen kan ses på det andet øverste billede er 128.119.245.12 og porten er 80
3. What is the sequence number of the TCP SYN segment that is used to initiate the TCP connection between the client computer and gaia.cs.umass.edu? (Note: this is the “raw” sequence number carried in the TCP segment itself; it is NOT the packet # in the “No.” column in the Wireshark window. Remember there is no such thing as a “packet number” in TCP or UDP; as you know, there are sequence numbers in TCP and that’s what we’re after here. Also note that this is not the relative sequence number with respect to the starting sequence number of this TCP session.). What is it in this TCP segment that identifies the segment as a SYN segment? Will the TCP receiver in this session be able to use Selective Acknowledgments (allowing TCP to function a bit more like a “selective repeat” receiver, see section 3.4.5 in the text)?
	1. Vi kan se på det her screenshot af den første TCP SYN, at det raw sequence number er 243244489 (relative sequence number er 0). 
	2. Vi kan se, at det, som definerer TCP beskeden som et SYN segment er dens Flag, der er sat til SYN. Hvis vi kigger på den næste (SYN, ACK) har den et (SYN, ACK) flag.
	3. Jeg ved godt nok ikke, om den kan bruge Selective Acknowledgements... Det kan jeg ikke se mig ud af.
	4. ![[Pasted image 20251006133944.png]]
4. What is the sequence number of the SYNACK segment sent by gaia.cs.umass.edu to the client computer in reply to the SYN? What is it in the segment that identifies the segment as a SYNACK segment? What is the value of the Acknowledgement field in the SYNACK segment? How did gaia.cs.umass.edu determine that value?
	1. Vi kan se at SYNACK har et raw sequence number på 1832525081
	2. Vi kan se at den har et (SYN, ACK) flag, og at både S
	3. ![[Pasted image 20251006134322.png]]

---
#lecture #tcp 