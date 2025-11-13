## Direct type I
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

## Direct type II
På det her billede, har den øverste streg i den røde blok, samt de to streger der går ned derfra samme værdi. Vi kalder detten en **w-value** ($w(n)$).
![[Pasted image 20251023085847.png]]

Og vi kan sammensætter disse linjer, da det er det samme.
![[Pasted image 20251023090001.png]]

På den måde kan vi både simplificere vores diagram OG bruge mindre hukommelse på vores computer, når det skal udregnes.

**Når de sammensættes på denne måde kaldes det _Direct type II_.**

Her kan vi se hvordan de sammensættes
![[Pasted image 20251023090305.png]]

- The type I structure uses 2N delay elements, i.e. 2N values must pass through the filter.
- The type II structure uses only N delay elements, which requires less memory.

Hvorfor bruger vi så ikke _hele tiden_ type II?
![[Pasted image 20251023090428.png]]

## Rounding errors
Hvis vi tager eksemplet fra før (sammensætning af type I til type II) hvor vi havde værdien $3,43$. Hvis vi har en rounding error, kunne det blive $3,4$ hvilket gør at vi mister værdien på andet decimals plads.
I sidste ende kan det ende med at vores system opfører sig på en _helt anden_ måde. Derfor skal man passe på med dette.

![[Pasted image 20251023090958.png]]
Da systemet er et loop, kan _én enkelt_ rounding error ende med en større og større fejl, desto højere ordenen af systemet er.

## Problems with direct realization
Normalt, når vi skal realisere (realize) et digital filter med _høj_ orden bruger vi IKKE Direct type I eller Direct type II.
I stedet opdeler vi normalt filteret i sektioner af _lav_ orden (første eller anden orden) og realiserer så HELE systemet vi enten
* [[Cascade and parallel implementation#Cascade realization|Cascade structure]] eller
* [[Cascade and parallel implementation#Parallel Realization|Parallel structure]]

---
#signalprocessing 