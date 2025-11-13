
---
**Date:** YYYY-MM-DD

## Preparation

>[!TODO] HOMEWORK
>- [ ] p. 215-289

> [!DANGER] EXERCISES
> - [x] Wireshark lab 4

> [!QUESTION] Questions
> - 

---
# Relevant documents


# Topics


# Notes
### Wireshark Lab UDP/DNS

1. Select the first UDP segment in your trace. What is the packet number of this segment in the trace file? What type of application-layer payload or protocol message is being carried in this UDP segment? Look at the details of this packet in Wireshark. How many fields there are in the UDP header? (You shouldn’t look in the textbook! Answer these questions directly from what you observe in the packet trace.) What are the names of these fields?
    
    1. Packet number: 10
    2. Application layer payload er DNS protokelen
    3. Der er 4 felter i headeren; Source, Destination, Length og Checksum
![[Pasted image 20251001115410.png]]


2. By consulting the displayed information in Wireshark’s packet content field for this packet (or by consulting the textbook), what is the length (in bytes) of each of the UDP header fields?
    
    1. Hver information har 4 HEX værdier (eg. 00 E2), og hver HEX værdi fylder 4 bits. Ergo må hver information fylde 16 bits = **2 bytes**. Da headeren har Source, Destination, Length og Checksum, må størrelsen af headeren være 2 * 4 = 8 bytes
3. The value in the Length field is the length of what? (You can consult the text for this answer). Verify your claim with your captured UDP packet.
    
    1. Length: 56.
    2. Det symboliserer i bytes størrelsen af ALT den sendte data. Altså både application data og header data.
4. What is the maximum number of bytes that can be included in a UDP payload? (Hint: the answer to this question can be determined by your answer to 2. above)
    
    1. UDP payload: 48 bytes. Størrelsen af UDP payload kan maks være length - størrelsen af header: 56 bytes - 8 bytes = 48 bytes.
5. What is the largest possible source port number? (Hint: see the hint in 4.)
    
    1. Da størrelsen af hvert felt i headeren er 2 bytes = 16 bits, må det største mulige source port nummer være $2^16 = 65536$. Men da vi også skal kunne vise 0, må det være 65535.
6. What is the protocol number for UDP? Give your answer in decimal notation. To answer this question, you’ll need to look into the Protocol field of the IP datagram containing this UDP segment (see Figure 4.13 in the text, and the discussion of IP header fields).
    
    1. Protocol (UDP): 17
7. Examine the pair of UDP packets in which your host sends the first UDP packet and the second UDP packet is a reply to this first UDP packet. (Hint: for a second packet to be sent in response to a first packet, the sender of the first packet should be the destination of the second packet). What is the packet number of the first of these two UDP segments in the trace file? What is the packet number of the second of these two UDP segments in the trace file? Describe the relationship between the port numbers in the two packets.
    
    1. Vi tager udgangspunkt i packet no 10 og 13, da de bruger samme IPv4 protokol. Angående ports, så er source port i no. 10: 60097 og destination port: 53. I no. 13 er det lige omvendt.
![[Pasted image 20251001115439.png]]

---
#lecture #tcp #udp