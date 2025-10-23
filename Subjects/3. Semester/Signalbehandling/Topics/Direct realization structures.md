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

Dette
![[Pasted image 20251023085133.png]]

bliver omskrevet til dette
![[Pasted image 20251023085153.png]]
Læg mærke til at tælleren bliver til alle dem der har noget med $x(n)$ at gøre, og at nævneren bliver **negativ** og er alle dem, der har med $y(n)$ at gøre.
Se desuden, at konstanter i tælleren bliver ganget med $x(n)$ når vi omskriver, mens konstanter i nævneren forsvinder.

Som vi så kan tegne et blok diagram af (som kommer til at ligne det øverste blok diagram med blå og grønne felter. Denne gang indsætter vi bare værdier for $a_N$ og $-b_N$ ).

Det samme system kan også omskrives/om-tegnes for at være det "spejlvendte"
![[Pasted image 20251023085608.png]]
**Der er en lille fejl i ovenstående billede, hvor $a$ og $b$ har byttet plads. Det burde selvfølgelig være $a$ der er positiv og $b$ der er negativ.**

På det her billede, har den øverste streg i den røde blok, samt de to streger der går ned derfra samme værdi. Vi kalder detten en **Double-value**(???).
![[Pasted image 20251023085847.png]]

---
#signalprocessing 