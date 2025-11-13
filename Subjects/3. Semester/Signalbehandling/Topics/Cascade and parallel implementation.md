# Cascade realization
Vi prøver at få vores store system til at ligne noget som dette
![[Pasted image 20251023093357.png]]

hvor $H_1(z),\quad H_2(z),\quad ...\quad H_M(z)$ er sub-systems.

![[Pasted image 20251023093412.png]]

Hvis vi finder polerne og nullerne (rødderne af tæller og nævner), kan vi faktorisere vores udtryk for $H(z)$. Denne faktorisering er så kaskaden (Cascade) som vi ser ovenover, da vi _ganger_ de faktoriset brøker sammen.
Til dette kan man bruge følgende MatLab funktioner
![[Pasted image 20251023093716.png]]

Her kan vi se et eksempel på hvordan et tredje-ordens system bliver faktoriseret til to systemer - et system, der er første-ordens og et system der er anden-ordens.
![[Pasted image 20251023093816.png]]
![[Pasted image 20251023093756.png]]

### Rules for Cascade Realization
1. Normalt, vil vi gerne have at ordenen af tæller og nævner i de opdelte systemer er **den samme**. 
   Vi kan se i vores ovenstående eksempel af de to systemer _ikke_ har samme orden som den anden, **men ordenen af hvert systems tæller og nævner er den samme**.

2. Vi vil desuden også gerne have, at systemets poler og nuller er organiseret således, at de kommer i samme sub-system. Det vil sige, at vi altså _ikke_ har et sub-system med $z_1$ og $p_2$ mens det andet system har $z_2$ og $p_1$. Det er bedre at have $z_1$ med $p_1$ og $z_2$ med $p_2$.

3. Den sidste regel, er at poler og nuller, der er **tæt på hinanden** (når vi plotter dem i enhedscirklen), skal i samme sub-system.
   ![[Pasted image 20251023094742.png]]
På ovenstående billede bliver de poler, der ligger _over for hinanden_ (spejlet i x-aksen) grupperet. I følge regel 2, kommer de tilhørende nuller så i samme system som deres poler.
### MatLab Example
Her kan vi se et eksempel på hvordan vi opdeler et femte-ordens system til 3 mindre systemer.
![[Pasted image 20251023094846.png]]
På Pole-Zero Map her ser det ud som om der kun er ét nul. Det er dog **5 nuller** der ligger meget meget tæt på hinanden.

![[Pasted image 20251023095300.png]]
Når vi kigger på diagrammet her, setter vi sub-systemerne i orden efter hvor blød (???) kurven er. Så vi sætter altså den midterste linje (sub-system) som den første i rækken og så derefter sætter vi den høje bue som den næste i rækken. Dette gør vi fordi at den midterste bue ved $\omega_a=1$ har en forstærkning på $-5 dB$. Dette er et ret svagt signal, så vi forstærker den. Til sidst tager vi den svage bue. På den måde får det mest stabile system.
**Jeg forstår ikke helt den her del...**

For at undgå _overflow_ af sub-systemerne og i sidste ende hoved-systemet, kan vi gøre brug af skalerings-faktorer, for at begrænse sub-systemerne.
![[Pasted image 20251023100051.png]]

# Parallel Realization
Et højere ordens system kan også realiseres på parallel form
![[Pasted image 20251023100153.png]]
![[Pasted image 20251023100200.png]]
![[Pasted image 20251023100251.png]]

**Læg mærke til forskellen her**:
- Cascade realization bliver _ganget_ sammen.
- Parallel realization bliver _plusset_ sammen.

Vi tager her et lille eksempel af det
![[Pasted image 20251023100320.png]]
Se her, at vi bruger _partial brøkopdeling_ (er det det, det hedder??) til at opdele i forhold til før, som var faktorisering.
![[Pasted image 20251023100433.png]]
![[Pasted image 20251023100410.png]]
![[Pasted image 20251023100850.png]]

Puha, det var godt nok et langt eksempel. **Måske jeg fanger det senere, men lige nu er det lidt uoverskueligt**.

### MatLab Example
Heldigvis kan vi også gøre det i MatLab! Her er et eksempel, hvor vi finder det i MatLab:
![[Pasted image 20251023101016.png]]
Her bruger vi funktionerne `residues` og `residuez` til at omskrive transfer funktionen.

Vi kan så lave følgende blok diagram
![[Pasted image 20251023101745.png]]
Læg mærke til at de værdier, der står i tællerne igen er defineret som $a_N$ og at dem i nævnerne igen er $-b_N$.
Se desuden at den $a_{22}$ i det grønne felt egentlig er kan udelades, da der ikke er en tredje værdi i tælleren, og burde betegnes som $=0$.
**Læg også mærke til at i modsætning til før, hvor potenserne for $z$ var negative, er de nu positive. Det er lidt forvirrende, og jeg har ikke helt forstået det endnu**.

# Cascade VS Parallel
![[Pasted image 20251023102054.png]]

# Signal flow graph
Indtil videre har vi snakket om blok-diagrammer. Vi har dog også **Signal flow graph**
![[Pasted image 20251023102435.png]]

![[Pasted image 20251023102500.png]]


---
#signalprocessing 