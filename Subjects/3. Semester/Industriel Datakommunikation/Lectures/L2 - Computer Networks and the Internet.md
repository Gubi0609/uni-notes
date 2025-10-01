
---
**Date:** YYYY-MM-DD

## Preparation

>[!TODO] HOMEWORK
>- [ ]  Chapter 1 of the book (p. 31 - 96)

> [!DANGER] EXERCISES
> - [ ] 

> [!QUESTION] Questions
> - 

---
# Relevant documents


# Topics


# Notes
Lab 1 resultat (besøg [http://gaia.cs.umass.edu/wireshark-labs/INTRO-wireshark-file1.html](http://gaia.cs.umass.edu/wireshark-labs/INTRO-wireshark-file1.html)) og opserver pakken med wireshark

![[Pasted image 20251001095203.png]]

1. Which of the following protocols are shown as appearing (i.e., are listed in the Wireshark “protocol” column) in your trace file: TCP, QUIC, HTTP, DNS, UDP, TLSv1.2?
    1. HTTP
2. How long did it take from when the HTTP GET message was sent until the HTTP OK reply was received? (By default, the value of the Time column in the packet-listing window is the amount of time, in seconds, since Wireshark tracing began. (If you want to display the Time field in time-of-day format, select the Wireshark View pull down menu, then select Time Display Format, then select Time-of-day.)
    1. Jeg kan ikke se, at jeg også fik HTTP OK, men mellem GET og HTTP gik der kun omkring 100 milisekunder
3. What is the Internet address of the [gaia.cs.umass.edu](http://gaia.cs.umass.edu/) (also known as [www-net.cs.umass.edu](http://www-net.cs.umass.edu/))? What is the Internet address of your computer or (if you are using the trace file) the computer that sent the HTTP GET message?
    1. [gaia.cs.umass.edu](http://gaia.cs.umass.edu): 128.119.245.12 (Since our computer sends the GET message, gaia must be the destination)
    2. computer: 10.126.101.244

To answer the following two questions, you’ll need to select the TCP packet containing the HTTP GET request (hint: this is packet number $286$). The purpose of these next two questions is to familiarize you with using Wireshark’s “Details of selected packet window”; see Figure 3. To do this, click on Packet 286 (your screen should look similar to Figure 3). To answer the first question below, then look in the “Details of selected packet” window toggle the triangle for HTTP (your screen should then look similar to Figure 5); for the second question below, you’ll need to expand the information on the Transmission Control Protocol (TCP) part of this packet.

1. Expand the information on the HTTP message in the Wireshark “Details of selected packet” window (see Figure 3 above) so you can see the fields in the HTTP GET request message. What type of Web browser issued the HTTP request? The answer is shown at the right end of the information following the “User-Agent:” field in the expanded HTTP message display. This field value in the HTTP message is how a web server learns what type of browser you are using.]•Firefox, Safari, Microsoft Internet Edge, Other
    1.  Se billedet lige under her
![[Pasted image 20251001095331.png]]
2. Expand the information on the Transmission Control Protocol for this packet in the Wireshark “Details of selected packet” window (see Figure 3 in the lab writeup) so you can see the fields in the TCP segment carrying the HTTP message. What is the destination port number (the number following “Dest Port:” for the TCP segment containing the HTTP request) to which this HTTP request is being sent?
    1. Destination port: 80
![[Pasted image 20251001095415.png]]
3. Print the two HTTP messages (GET and OK) referred to in question 2 above. To do so, select Print from the Wireshark File command menu, and select the “Selected Packet Only” and “Print as displayed” radial buttons, and then click OK
![[Pasted image 20251001095502.png]]
---
#lecture 