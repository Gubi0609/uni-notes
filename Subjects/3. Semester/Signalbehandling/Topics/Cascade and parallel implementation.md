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

Normalt, vil vi gerne have at ordenen af tæller og nævner i de opdelte systemer er **den samme**.
Vi kan se i vores ovenstående eksempel af de to systemer _ikke_ har samme orden som den anden, **men ordenen af hvert systems tæller og nævner er den samme**.

Vi vil desuden også gerne have, at systemets poler og nuller er organiseret således, at de kommer i samme sub-system. Det vil s

---
#signalprocessing 