

---
**Date:** YYYY-MM-DD

## Preparation

>[!TODO] HOMEWORK
>- [ ]  p. 155-198

> [!DANGER] EXERCISES
> - [x]  Lab 3: Wireshark
> - [x] Python lab: Getting started

> [!QUESTION] Questions
> - 

---
# Relevant documents


# Topics


# Notes
Domain Name System (DNS) translates between domain name and IP-adress of the hosts.

Hvis man skriver et domain name i sin browser, sidder der en DNS server et sted, som oversætter det til IP-adressen for host, sender dig svaret og så kan du finde den rigtige vej.

Host aliasing er når en host også har et andet navn fx. [gmail.com](http://gmail.com) → [googlemail.com](http://googlemail.com)

Mange host-navne til én IP

Load distribution er når ét domain navn er delt op over flere IP-adresser fx et internationalt netværk af serverer

Decentralized netværk er oftest bedre end centralized, da du så har flere servere spredt over hele verdenen. På den måde skal folk fra USA ikke kommunikere med en DNS server i europa for at få IP adressen for en hjemmeside i USA. Og hvis én server går ned, er der stadig flere serverer der er oppe.

En DNS server har et hearaki i det du har en Root DNS, så har du en TLD (Top Level Domain) server med .com, .net, .org osv som indeholder domain navnene med den endelse.

Der er også en Local DNS server (Er ikke helt sikker på hvad den gør, så undersøg lidt nærmere). Den fungerer åbenbart også som en proxy (hvad er det??)

En DNS server kan cache et domain name/IP par, for hurtigere at omdirigere brugeren. Serveren gemmer kun informationen i et bestemt stykke tid. Normalt 12 timer til 2 dage.

RFC (Request For Comments) 2136 er vidst noget der køres lidt mere offentligt, som gør det mindre sikkert at bruge som host (???)
![[Pasted image 20251001100104.png]]
ttl betyder time to live, som er hvor længe DNS serveren skal gemme informationen.

### LAB 1 Python
``` python
from datetime import datetimeimport sys

# Opgave 1. Find nuværende tid for systemet.# date = datetime.now()
# print(date.time())

# ---------------------------------------------------- #

# Opgave 2. Gem input og tidstempel i en .txt fil
# inp = input("Please type a message to save: ")

# date = datetime.now()
# time = date.time()
# message = str(time) + " " + inp + "\n"

# with open("log.txt", "a") as file:
#     file.write(message)

# ---------------------------------------------------- #

# Opgave 3. Tilføj command line argument
if len(sys.argv) < 2:    
	inp = input("Please type a message to save: ")
else:    
	inp = sys.argv[1]

date = datetime.now()
time = date.time()
message = str(time) + " " + inp + "\n"

with open("log.txt", "a") as file:    
	file.write(message)

# ---------------------------------------------------- #

# Opgave 4. Print alle linjer af log filen efter input.
with open("log.txt", "r") as file:    
	print(file.read())    
```
### LAB 3 Wireshark DNS

**Opgave 1**

1. Run nslookup to obtain the IP address of the web server for the Indian Institute of Technology in Bombay, India: [www.iitb.ac.in](http://www.iitb.ac.in/). What is the IP address of [www.iitb.ac.in](http://www.iitb.ac.in/)

```bash
$ nslookup www.iitb.ac
Server:		127.0.0.53
Address:	127.0.0.53#53

Non-authoritative answer:
Name:	www.iitb.ac
Address: 199.59.243.228
```

1. What is the IP address of the DNS server that provided the answer to your nslookup command in question 1 above?

```bash
Server:		127.0.0.53
```

1. Did the answer to your nslookup command in question 1 above come from an authoritative or non-authoritative server?
    
    1. Non authorative, meaning that it was cached in a DNS server, and I got the cached answer returned
2. Use the nslookup command to determine the name of the authoritative name server for the [iitb.ac.in](http://iit.ac.in/) domain. What is that name? (If there are more than one authoritative servers, what is the name of the first authoritative server returned by nslookup)? If you had to find the IP address of that authoritative name server, how would you do so?
    

```bash
$ nslookup -type=NS iitb.ac.in
Server:		127.0.0.53
Address:	127.0.0.53#53

Non-authoritative answer:
iitb.ac.in	nameserver = dns1.iitb.ac.in.
iitb.ac.in	nameserver = dns2.iitb.ac.in.
iitb.ac.in	nameserver = dns3.iitb.ac.in.

Authoritative answers can be found from:
```

1. Så er den første authorative name server [iitb.ac.in](http://iitb.ac.in/) nameserver = [dns1.iitb.ac.in](http://dns1.iitb.ac.in/).

---

**Opgave 2**

1. Clear the DNS cache in your host, as described above

```bash
sudo resolvectl flush-caches
```

2. Open your Web browser and clear your browser cache.
    
3. Open Wireshark and enter ip.addr == <your_IP_address>into the display filter, where <your_IP_address>is the IPv4 address of your computer4. With this filter, Wireshark will only display packets that either originate from, or are destined to, your host.
    
    ```bash
    $ hostname -I
    10.126.101.244
    ```
    
4. Start packet capture in Wireshark.
    
5. With your browser, visit the Web page: [http://gaia.cs.umass.edu/kurose_ross/](http://gaia.cs.umass.edu/kurose_ross/)
    
6. Stop packet capture.
![[Pasted image 20251001100300.png]]
7. Locate the first DNS query message resolving the name [gaia.cs.umass.edu](http://gaia.cs.umass.edu/). What is the packet number in the trace for the DNS query message? Is this query message sent over UDP or TCP?
    1. Som kan ses på nedenstående billede, er protokolet UDP
![[Pasted image 20251001100347.png]]
8. Now locate the corresponding DNS response to the initial DNS query. What is the packet number in the trace for the DNS response message? Is this response message received via UDP or TCP?
    1. Den er også via UDP. packet number er 41, og forrige var 38.
![[Pasted image 20251001100411.png]]
9. What is the destination port for the DNS query message? What is the source port of the DNS response message?
    1. Vi kan se her at destination port (min computer) er 44205, og at source port (serveren) er 53
![[Pasted image 20251001100434.png]]
10. To what IP address is the DNS query message sent?
    1. 10.220.2.24
11. Examine the DNS query message. How many “questions” does this DNS message contain? How many “answers” answers does it contain?
![[Pasted image 20251001100458.png]]
12. Examine the DNS response message to the initial query message. How many “questions” does this DNS message contain? How many “answers” answers does it contain?
![[Pasted image 20251001100528.png]]
13. The web page for the base file [http://gaia.cs.umass.edu/kurose_ross/](http://gaia.cs.umass.edu/kurose_ross/) references the image object [http://gaia.cs.umass.edu/kurose_ross/header_graphic_book_8E_2.jpg](http://gaia.cs.umass.edu/kurose_ross/header_graphic_book_8E_2.jpg) , which, like the base webpage, is on [gaia.cs.umass.edu](http://gaia.cs.umass.edu/). What is the packet number in the trace for the initial HTTP GET request for the base file [http://gaia.cs.umass.edu/kurose_ross/](http://gaia.cs.umass.edu/kurose_ross/)? What is the packet number in the trace of the DNS query made to resolve [gaia.cs.umass.edu](http://gaia.cs.umass.edu/) so that this initial HTTP request can be sent to the [gaia.cs.umass.edu](http://gaia.cs.umass.edu/) IP address? What is the packet number in the trace of the received DNS response? What is the packet number in the trace for the HTTP GET request for the image object [http://gaia.cs.umass.edu/kurose_ross/header_graphic_book_8E2.jpg](http://gaia.cs.umass.edu/kurose_ross/header_graphic_book_8E2.jpg)? What is the packet number in the DNS query made to resolve [gaia.cs.umass.edu](http://gaia.cs.umass.edu/) so that this second HTTP request can be sent to the [gaia.cs.umass.edu](http://gaia.cs.umass.edu/) IP address? Discuss how DNS caching affects the answer to this last question.
    1. Jeg kørte programmet igen, fordi jeg kom til at søge med https i stedet for http. Derfor passer nogle af tallene ikke helt
        1. Første DNS query for at få hjemmesiden har packet nr. 4.
        2. HTTP GET har packet nr 10.
        3. DNS resolve HTTP har også packet nr. 4, da HTTP bruger den IP-adresse vi fik fra den første DNS query
        4. DNS response har packet nr. 6
        5. HTTP GET for billedet har packet nr. 443
        6. DNS resolve HTTP nr. 2 har også packet nr. 4, da den bare bruger den IP-adresse fra før, da destinationen er den samme, og den er gemt i cache.
    2. DNS caching påvirker det ved at vi så ikke skal sende en DNS query hver evig eneste gang vi skal få noget fra hjemmesiden, men kun første gang, og så refererer vi til den IP-adresse fremover for samme domain navn.
![[Pasted image 20251001100601.png]]
#### Opgave 4
Now let’s play with nslookup.

- Start packet capture.
- Do an nslookup on [www.cs.umass.edu](http://www.cs.umass.edu/)
- Stop packet capture.

1. What is the destination port for the DNS query message? What is the source port of the DNS response message?
    1. Destination port for query er 53
![[Pasted image 20251001100637.png]]
	2. Source port for response er også 53
![[Pasted image 20251001100720.png]]
rg
2. To what IP address is the DNS query message sent? Is this the IP address of your default local DNS server?
    
    1. Destination IP for query er 10.170.8.11.
    2. Jeg fandt min default local DNS server således. Vi kan se, at 10.170.8.11 er en af de DNS servere der står på listen. Altså er det den samme.
    
    ```bash
    $ resolvectl status
    Global
             Protocols: -LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
      resolv.conf mode: stub
    
    Link 2 (enp2s0)
        Current Scopes: none
             Protocols: -DefaultRoute -LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
    
    Link 3 (wlo1)
        Current Scopes: DNS
             Protocols: +DefaultRoute -LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
    Current DNS Server: 10.170.8.12
           DNS Servers: 10.170.8.11 10.170.8.12
    ```
    
3. Examine the DNS query message. What “Type” of DNS query is it? Does the query message contain any “answers”?
    
    1. Det er en type A, som kan ses på billedet her. På billedet nedenunder kan man se hvad den indeholder, og den ser ikke ud til at have nogle “Answer”s.
![[Pasted image 20251001115047.png]]
4. Examine the DNS response message to the query message. How many “questions” does this DNS response message contain? How many “answers”?
    1. Hvis vi kigger på response, kan vi se at der både er ét answer og ét question
![[Pasted image 20251001115112.png]]

#### Opgave 5

Last, let’s use nslookup to issue a command that will return a type NS DNS record, Enter the following command: nslookup –type=NS [umass.edu](http://umass.edu/) and then answer the following questions :

1. To what IP address is the DNS query message sent? Is this the IP address of your default local DNS server?
    1. query message bliver sendt til 10.170.8.12. Det er nærmest den samme IP-adresse som sidst der var det her spørgsmål (med undtagelse af 11 der nu er 12). Vi kan se fra forrige opgave med lignende problemstilling, at 10.170.8.12 også er på listen af DNS servere.
2. Examine the DNS query message. How many questions does the query have? Does the query message contain any “answers”?
    1. Ligesom før er der kun ét question og nul answer
![[Pasted image 20251001115148.png]]
3. Examine the DNS response message. How many answers does the response have? What information is contained in the answers? How many additional resource records are returned? What additional information is included in these additional resource records?
    1. Vi kan se, at der nu er 3 answers i vores response message. Desuden kan vi se på billedet under, hvad de Answers indeholder, hvilket er name serverne for [umass.edu](http://umass.edu), deres levetid, typen osv osv.
![[Pasted image 20251001115210.png]]

---
#lecture #dns