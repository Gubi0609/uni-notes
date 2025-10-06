
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

---
#lecture #tcp 