
---
**Date:** 2025-10-06

## Preparation

>[!TODO] HOMEWORK
>- [ ] p. 286 - 314

> [!DANGER] EXERCISES
> - [x] [[Wireshark_TCP_v8.1.pdf]]

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

### TCP Basics

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
	2. Vi kan se at den har et (SYN, ACK) flag, og at både Syn og Acknowledgement er sat til 1.
	3. Raw ACK value er 243244490. Vi kan se at den er lige nøjagtig **1** højere end raw SYN sequence number fra forrige spørgsmål.
	4. Den bestemte nok den værdi ved at lægge én til SYN's raw sequence number
	5. ![[Pasted image 20251006134322.png]]
5. What is the sequence number of the TCP segment containing the header of the HTTP POST command? Note that in order to find the POST message header, you’ll need to dig into the packet content field at the bottom of the Wireshark window, looking for a segment with the ASCII text “POST” within its DATA field. How many bytes of data are contained in the payload (data) field of this TCP segment? Did all of the data in the transferred file alice.txt fit into this single segment?
	1. Vi kan se i det markeret med blå, at der i DATA feltet står POST.
	2. Den har et raw sequence number på 243244490, hvilket er samme som ACK nummeret fra forrige.
	3. Vi kan se på tredje nederste linje i venstre side af vinduet, at der er en TCP payload på 1238 bytes. Da filen er 148.5 kB, må det betyde at hele filen _**ikke**_ er i den her ene besked.
	4. ![[Pasted image 20251006134847.png]]
6. Consider the TCP segment containing the HTTP “POST” as the first segment in the data transfer part of the TCP connection.
	1. At what time was the first segment (the one containing the HTTP POST) in the data-transfer part of the TCP connection sent?
		1. Anden kolonne af ovenstående billede (den "grønne" del) har tiden **18.391998827**.
	2. At what time was the ACK for this first data-containing segment received? 
		1. Jeg går ud fra at det er pakke 44 her, da det er den første ACK _til_ min computer. Den blev modtaget til tiden **18.495285847**.
		2. ![[Pasted image 20251006135521.png|1500]]
	3. What is the RTT for this first data-containing segment?
		1. $RTT = 18.495285847-18.391998827 = 0.10328702$
	4. What is the RTT value the second data-carrying TCP segment and its ACK?
		1. Jeg går ud fra at det er de her to. **Jeg har indset at jeg lavede en fejl i mit forrige svar, men jeg ved ikke hvordan jeg skal rette op på den. ACK fra modtageren skal passe med SEQ fra senderen.** Vi kan se, at Seq på pakke 36 er 2477 og at Ack på pakke 44 er 2477. Altså passer de sammen.
		2. $RTT = 18.495285847-18.392015570=0.103270277$
		3. ![[Pasted image 20251006140743.png|1500]]
	5. What is the EstimatedRTT value (see Section 3.5.3, in the text) after the ACK for the second data-carrying segment is received? Assume that in making this calculation after the received of the ACK for the second segment, that the initial value of EstimatedRTT is equal to the measured RTT for the first segment, and then is computed using the EstimatedRTT equation on page 242, and a value of α = 0.125. Note: Wireshark has a nice feature that allows you to plot the RTT for each of the TCP segments sent. Select a TCP segment in the “listing of captured packets” window that is being sent from the client to the gaia.cs.umass.edu server. Then select: Statistics->TCP Stream Graph- >Round Trip Time Graph.
		1. $EstimatedRTT = (1-\alpha)*EstimatedRTT + \alpha*SampleRTT$
		2. Vi prøver at sætte EstimatedRTT på højre side til at være den RTT jeg udregnede:
		3. $EstimatedRTT = (1-0.125)*0.10328702+0.125*0.103270277=0.103284927$
7. What is the length (header plus payload) of each of the first four data-carrying TCP segments?
	1. 1238 + 32 = 1270
	2. 1238 + 32 = 1270
	3. 1238 + 32 = 1270
	4. 1238 + 32 = 1270
8. What is the minimum amount of available buffer space advertised to the client by gaia.cs.umass.edu among these first four data-carrying TCP segments? Does the lack of receiver buffer space ever throttle the sender for these first four data- carrying segments?
	1. Vi kan se, at Window (som er bufferen) er på 502 bytes. Da det er under længden på hver TCP segment går jeg lidt ud fra at jeg bliver throttled...
	2. ![[Pasted image 20251006142419.png]]
9. Are there any retransmitted segments in the trace file? What did you check for (in the trace) in order to answer this question?
	1. Nej det er der ikke. **Jeg kiggede på farven i "listing of captured packets" vinduet. Hvis der var en pakke, der var sort eller rød, betyder det at der er sket en fejl eller at den er en duplikat af en anden pakke. Der var ikke nogen af de røde/sorte pakker som indeholdte tekst filen i dens data. Derfor kan jeg konkluderer at tekst filens pakker gik igennem i første forsøg.**
10. How much data does the receiver typically acknowledge in an ACK among the first ten data-carrying segments sent from the client to gaia.cs.umass.edu? Can you identify cases where the receiver is ACKing every other received segment (see Table 3.2 in the text) among these first ten data-carrying segments? 
11. What is the throughput (bytes transferred per unit time) for the TCP connection? Explain how you calculated this value.

### TCP congestion control in action
Mangler lige at sætte spørgsmålene ind her...


---
#lecture #tcp 