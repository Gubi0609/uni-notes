
---
**Date:** 2025-11-10

## Preparation

>[!TODO] HOMEWORK
>- [ ] 

> [!DANGER] EXERCISES
> - [ ] [[Wireshark Lab 7.pdf]]

---
# Relevant documents
[[NetworkLayerControlPlane.pdf]]
[[Wireshark Lab 7.pdf]]

# Topics


# Notes

## Wireshark Lab 7


### ICMP and Ping
Printout from terminal
![[Pasted image 20251110105924.png]]

Wireshark result
![[Pasted image 20251110105958.png]]

1. What is the IP address of your host? What is the IP address of the destination host?
	1. IP of destination host: **143.89.209.9**
	2. IP of source host: **10.126.110.119**
2. Why is it that an ICMP packet does not have source and destination port numbers?
	1. Pas...
3. Examine one of the ping request packets sent by your host. What are the ICMP type and code numbers? What other fields does this ICMP packet have? How many bytes are the checksum, sequence number and identifier fields?
	1. ![[Pasted image 20251110110409.png]]
	2. Checksum size: **16 bits** (**2 bytes**) (same for sequence number and identifier fields)
4. Examine the corresponding ping reply packet. What are the ICMP type and code numbers? What other fields does this ICMP packet have? How many bytes are the checksum, sequence number and identifier fields?
	1. ![[Pasted image 20251110110542.png]]
	2. Checksum size: **16 bits** (**2 bytes**) (same for sequence number and identifier fields)


### ICMP and Traceroute

Printout from terminal
![[Pasted image 20251110114458.png]]

Wireshark result (I'm using Linux, so some of the questions wouldn't be answerable from my results. Therefore I use the provided standard result from gaia.cs.umass.edu )
![[Pasted image 20251110112804.png]]


5. What is the IP address of your host? What is the IP address of the target destination host?
	1.  IP address of source host: **192.168.1.101**
	2. IP address of destination host: **138.96.146.2**
6. If ICMP sent UDP packets instead (as in Unix/Linux), would the IP protocol number still be 01 for the probe packets? If not, what would it be?
	1. No, then it would be **17**, as that is the protocol number for UDP
7. Examine the ICMP echo packet in your screenshot. Is this different from the ICMP ping query packets in the first half of this lab? If yes, how so?
	1. ![[Pasted image 20251110112947.png]]
	2. Well first of all, this doesn't have a response, like it did in the first exercise.
	3. And obviously the packet/communication link specific data (checksum, identifier, sequence number) is different.
	4. Type and code are the same though.
8. Examine the ICMP error packet in your screenshot. It has more fields than the ICMP echo packet. What is included in those fields?
	1. ![[Pasted image 20251110113605.png]]
	2. For the outer ICMP the type is different (**11**), and it doesn't have Identifier or Sequence number.
	3. For the inner ICMP the type is the same (**8**), and it has both Identifier and Sequence number.
	4. _So basically, there is an outer and inner ICMP field, that each have their fields, making the total larger._
	5. **NOTICE, THAT THE INNER ICMP FIELD, IS THE ORIGINAL ICMP REQUEST FROM SOURCE!!**
	6. It calculates a new checksum, to check if the data is wrong, and that is why it didn't reach its target (the checksum is good, so it isn't that)
9. Examine the last three ICMP packets received by the source host. How are these packets different from the ICMP error packets? Why are they different?
	1. ![[Pasted image 20251110113827.png]]
	2. The above is just one of them. They are pretty much alike in structure, so I won't show the others.
	3. The type is **0** instead of **8** or **11**. That is because it is a successful reply, and not a request or error.
	4. Identifier is the same as the inner ICMP of the error, and so is sequence number.
10. Within the tracert measurements, is there a link whose delay is significantly longer than others? Refer to the screenshot in Figure 4, is there a link whose delay is significantly longer than others? On the basis of the router names, can you guess the location of the two routers on the end of this link?
	1. Between packet **9** and **10** (in the tracert screenshot above) there is a jump from 25 ms to 96 ms.
	2. Packet **9** has its host located in NYC (New York City, USA) and packet **10** has its host located in Pastourelle (France). So obviously it takes a little longer to travel across the Atlantic.

---
#lecture 