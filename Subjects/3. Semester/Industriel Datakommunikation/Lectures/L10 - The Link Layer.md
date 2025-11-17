
---
**Date:** 2025-11-17

## Preparation

>[!TODO] HOMEWORK
>- [ ] 

> [!DANGER] EXERCISES
> - [ ] [[Wireshark Lab 8.pdf]]

---
# Relevant documents
[[09 - The Link Layer.pdf]]
[[Wireshark Lab 8.pdf]]
# Topics
Vi snakkede om Error detection. Se dine noter til [[CRC]] og [[Hamming codes]] for forklaring på CRC (selvfølgelig) og 2-dimensional parity bit

# Notes

## Capturing and analyzing Ethernet frames
1. What is the 48-bit Ethernet address of your computer?
	1. Source: LiteonTechno_6b:05:b9 **`c0:35:32:6b:05:b9`**
2. What is the 48-bit destination address in the Ethernet frame? Is this the Ethernet address of gaia.cs.umass.edu? (Hint: the answer is no). What device has this as its Ethernet address? (Note: this is an important question, and one that students sometimes get wrong. Re-read pages 468-469 in the text and make sure you understand the answer here.)
	1. Destination: **`48:a1:70:a8:79:02`**
	2. No apparently this is not the Ethernet adress of gaia.cs.umass.edu. I do not know why.
	3. The switch that I am connected to has this address.
3. Give the hexadecimal value for the two-byte Frame type field. What upper layer protocol does this correspond to?
	1. **`0x0800`** corresponds to IPv4 protocol
4. How many bytes from the very start of the Ethernet frame does the ASCII “G” in “GET” appear in the Ethernet frame?
	1. **53 bytes in**
	2. ![[Pasted image 20251117111925.png]]


This is for the OK HTTP response message
1. What is the value of the Ethernet source address? Is this the address of your computer, or of gaia.cs.umass.edu (Hint: the answer is no). What device has this as its Ethernet address?
	1. **`48:a1:70:a8:79:02`**
	2. This is the address of the switch, that I am connected to.
2. What is the destination address in the Ethernet frame? Is this the Ethernet address of your computer?
	1. LiteonTechno_6b:05:b9 **`c0:35:32:6b:05:b9`**
	2. This is the address of my computer.
3. Give the hexadecimal value for the two-byte Frame type field. What upper layer protocol does this correspond to?
	1. **`0x0800`** corresponds to IPv4 protocol
4. How many bytes from the very start of the Ethernet frame does the ASCII “O” in “OK” (i.e., the HTTP response code) appear in the Ethernet frame?
	1. **63 bytes in**
	2. ![[Pasted image 20251117112853.png]]

## The Address Resolution Protocol
9. Write down the contents of your computer’s ARP cache. What is the meaning of each column value?
	1. **`_gateway (10.126.96.1) at 48:a1:70:a8:79:02 [ether] on wlo1`**
	2. 

---
#lecture 