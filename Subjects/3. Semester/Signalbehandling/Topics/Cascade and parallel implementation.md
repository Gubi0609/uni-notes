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
Normalt, vil vi gerne have at ordenen af tæller og nævner i de opdelte systemer er **den samme**.
Vi kan se i vores ovenstående eksempel af de to systemer _ikke_ har samme orden som den anden, **men ordenen af hvert systems tæller og nævner er den samme**.

Vi vil desuden også gerne have, at systemets poler og nuller er organiseret således, at de kommer i samme sub-system. Det vil sige, at vi altså _ikke_ har et sub-system med $z_1$ og $p_2$ mens det andet system har $z_2$ og $p_1$. Det er bedre at have $z_1$ med $p_1$ og $z_2$ med $p_2$.

Den sidste regel, er at poler og nuller, der er **tæt på hinanden** (når vi plotter dem i enhedscirklen), skal i samme sub-system.
![[Pasted image 20251023094742.png]]

### MatLab Example
Her kan vi se et eksempel på hvordan vi opdeler et femte-ordens system til 3 mindre systemer.
![[Pasted image 20251023094846.png]]
På Pole-Zero Map her ser det ud som om der kun er ét nul. Det er dog **5 nuller** der ligger meget meget tæt på hinanden.

På ovenstående billede bliver de poler, der ligger 

---
#signalprocessing 