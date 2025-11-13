
---
**Date:** 2025-11-03

## Preparation

>[!TODO] HOMEWORK
>- [ ] page 333-389

> [!DANGER] EXERCISES
> - [ ]  [[Wireshark_IP_v8.1.pdf]]

> [!QUESTION] Questions
> - 

---
# Relevant documents
[[07 - NetworkLayerDataPlane.pdf]]
[[Wireshark_IP_v8.1.pdf]]
# Topics


# Notes
## Wireshark Lab 6

### Part 1: Basic IPv4
1. Select the first UDP segment sent by your computer via the traceroute command to gaia.cs.umass.edu. (Hint: this is 44th packet in the trace file in the ip-wireshark-trace1-1.pcapng file in footnote 2). Expand the Internet Protocol part of the packet in the packet details window. What is the IP address of your computer?
	1. 10.126.110.119
2. What is the value in the time-to-live (TTL) field in this IPv4 datagram’s header?
	1. Time to Live: 64
3. What is the value in the upper layer protocol field in this IPv4 datagram’s header?
	1. Øhhhhh kan ikke rigtig finde det her
4. How many bytes are in the IP header?
	1. $74-54=20$ bytes
5. How many bytes are in the payload of the IP datagram? Explain how you determined the number of payload bytes.
	1. Se, jeg er lidt i tvivl... Min Total Length under Internet Protocol Version 4 (IPv4) er **74** bytes, men under User Datagram Protocol (UDP) er UDP payload : **46** bytes
6. Has this IP datagram been fragmented? Explain how you determined whether or not the datagram has been fragmented.
	1. Under IPv4 sektionen er Fragment Offset : 0. Derfor går jeg udfra, at der ikke har været nogen fragmentation

7. Which fields in the IP datagram always change from one datagram to the next within this series of UDP segments sent by your computer destined to 10.220.2.24, via traceroute? Why?
	1. Længden ændrer sig
	2. Header checksum ændrer sig selvfølgelig an på hvilken data man sender. Header længden er dog altid 20 bytes.
	3. Source port ændrer sig åbenbart også... Ved ikke hvorfor
8. Which fields in this sequence of IP datagrams (containing UDP segments) stay constant? Why?
	1. Time to Live (TTL) er altid 64. Ingen anelse om hvorfor
	2. IP adresserne for src og dst er altid den samme. Selvfølgelig, fordi den skal sende til samme sted hver gang.
	3. Header længden er altid 20 bytes.
9. Describe the pattern you see in the values in the Identification field of the IP datagrams being sent by your computer.
	1. A'hva??
## ==JEG MANGLER AT SVARE PÅ RESTEN==

1. What is the upper layer protocol specified in the IP datagrams returned from the routers? 
	1. Igen, kan ikke rigtig finde ud af det her "upper layer protocol", men det er **pakke 23**.
2. Are the values in the Identification fields (across the sequence of all of ICMP packets from all of the routers) similar in behavior to your answer to question 9 above?
3. Are the values of the TTL fields similar, across all of ICMP packets from all of the routers?

### Part 2: Fragmentation
Sort the packet listing from Part 1, with any display filters cleared, according to time, by
clicking on the Time column.
13. Find the first IP datagram containing the first part of the segment sent to 128.119.245.12 sent by your computer via the traceroute command to gaia.cs.umass.edu, after you specified that the traceroute packet length should be 3000. (Hint: This is packet 179 in the ip-wireshark-trace1-1.pcapng trace file in footnote 2. Packets 179, 180, and 181 are three IP datagrams created by fragmenting the first single 3000-byte UDP segment sent to 128.119.145.12). Has that segment been fragmented across more than one IP datagram? (Hint: the answer is yes!)
14. What information in the IP header indicates that this datagram been fragmented?
15. What information in the IP header for this packet indicates whether this is the first fragment versus a latter fragment?
16. How many bytes are there in is this IP datagram (header plus payload)?
17. Now inspect the datagram containing the second fragment of the fragmented UDP segment. What information in the IP header indicates that this is not the first datagram fragment?
18. What fields change in the IP header between the first and second fragment?
19. Now find the IP datagram containing the third fragment of the original UDP segment. What information in the IP header indicates that this is the last fragment of that segment?

### Part 3: IPv6
In this final section we’ll take a quick look at the IPv6 datagram using Wireshark. You’ll probably want to review section 4.3.4 in the text. Because the Internet is still primarily at IPv4 network (see section 4.3.4), and your own computer or your ISP may not be configured for IPv6, let’s look at a trace of already captured packets that contain some IPv6 packets. To generate this trace, our web browser opened the youtube.com homepage. Youtube (and Google) provide fairly widespread support for IPv6. Open the file ip-wireshark-trace2-1.pcapng in the .zip file of traces given in footnote 2. Your Wireshark display should look similar to Figure 4.

Let’s start by taking a closer look at the 20th packet in this trace, sent at t=3.814489. This is a DNS request (contained in an IPv6 datagram) to an IPv6 DNS server for the IPv6 address of youtube.com. The DNS AAAA request type is used to resolve names to IPv6 IP addresses.

Answer the following questions:
20. What is the IPv6 address of the computer making the DNS AAAA request? This is the source address of the 20th packet in the trace. Give the IPv6 source address for this datagram in the exact same form as displayed in the Wireshark window5.
21. What is the IPv6 destination address for this datagram? Give this IPv6 address in the exact same form as displayed in the Wireshark window.
22. What is the value of the flow label for this datagram?
23. How much payload data is carried in this datagram?
24. What is the upper layer protocol to which this datagram’s payload will be delivered at the destination? Lastly, find the IPv6 DNS response to the IPv6 DNS AAAA request made in the 20th packet in this trace. This DNS response contains IPv6 addresses for youtube.com.
25. How many IPv6 addresses are returned in the response to this AAAA request?
26. What is the first of the IPv6 addresses returned by the DNS for youtube.com (in the ip-wireshark-trace2-1.pcapng trace file, this is also the address that is numerically the smallest)? Give this IPv6 address in the exact same shorthand form as displayed in the Wireshark window.

---
#lecture 