![[Pasted image 20251002084202.png]]
Hvor 
## $$z = e^{sT}$$ 
og 
## $$s = \sigma + j\omega$$
![[Pasted image 20251002084429.png]]

Z-transformen af $x(n)$ er defineret som
## $$X(z)=\sum^\infty_{n=0}x(n)z^{-n}$$
![[Pasted image 20251002084713.png]]
![[Pasted image 20251002085029.png]]
Det er sgu da mega forvirrende at se på... Men der er måske et mønster?
Grunden til at origo i s-domænet bliver rykket til (1,0) i z-domænet, er fordi 
## $$(0+j0)_s = (e^{0+j0})_z=1$$
Vi kan også se at positionen på y-aksen af s-domænet svarer til en rotation med en hvis radian i z-domænet. I de tilfælde er $\sigma=0$ da $\sigma$ er den reelle del af s-domænet.
Hvis vi kun fokuserer på den reelle del af s-domænet, vil $\omega = 0$ i stedet, da den kun påvirker den imaginære del.
Vi kan se på spiral pilene i z-domænet, at placeringen på den reelle akse af s-domænet påvirker distancen fra centrum af cirklen i z-domænet.
Ud fra den formel der står på billedet for z, kan vi se hvordan radius og vinkling bestemmes. Kig eventuelt også på exercise herunder.

Hvis systemet er stabilt, er vores "poler" (???) på venstre side af s-domænet, hvor $\sigma<0 \rightarrow |z|=e^{\sigma/f_s} < 1$. Det betyder, at værdierne ligger på indersiden af cirklen i z-domænet, så de altså er en del af cirklens areal. 

> [!HELP]- Exercise
![[Pasted image 20251002091919.png]]

![[Pasted image 20251002094327.png]]
![[Pasted image 20251002093849.png]]
Vi bruger ofte regel Z1 og Z2 i dette [[Signalbehandling|kursus]].

![[Pasted image 20251002094601.png]]
![[Pasted image 20251002095618.png]]
![[Pasted image 20251002101556.png]]
![[Pasted image 20251002105031.png]]

---
#signalprocessing #z-transform