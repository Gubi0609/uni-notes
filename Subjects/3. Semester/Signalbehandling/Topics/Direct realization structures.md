![[Pasted image 20251023083034.png]]
På ovenstående billede, er det fint farve koordineret, hvordan hver del passer ind i diagrammet. Det "+" markeret med rød, er faktisk det minus, vi ser i udtrykket for $y(n)$, men da den grønne del er negativ, bliver det et minus.
Vi kan se, at SUM tegnet i ligningen bliver gjort til en summerings-række af alle de $a_ix(n-i)$ enheder, der er (hvor firkanten med $z^{-1}$ er delay og trekanten med $a_N$ eller $-b_N$ (læg mærke til negativ fortegn på $b_N$) er multiplikation).

Vi kan også se at ovenstående er et _loop_ da $y(n)$ indgår i ligningen (og "blok"-diagrammet) for sig selv.
For linjerne mellem hver _blok_ er den enhed, der "flyder" på linjen den samme (ligesom et elektrisk kredsløb). Det betyder altså, at efter det røde "+" flyder $y(n)$. En del af $y(n)$ går så ned igennem blokken med $z^{-1}$ og bliver til $y(n-1)$. Dette deler sig så og går enten gennem endnu en $z^{-1}$ eller en $-b_1$. Sådan fortsætter vi, og summerer dette signal til sidst, og lægger det sammen med $x(n)$ summeringen.
**Læg mærke til, at $b_N$ har negativt fortegn. Dette betyder at summeringen af $y(n)$ altså bliver _mindre_ for hvert loop. Man ville ellers tro, at man endte med et uendeligt stort signal, men det burde gerne gå mod et "konstant" signal.**

Det kan generelt set skrives således:
![[Pasted image 20251023083650.png]]

Another example
![[Pasted image 20251023084543.png]]



---
#signalprocessing 