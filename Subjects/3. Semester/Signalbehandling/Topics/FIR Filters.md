> A **_finite impulse response filter (FIR filter)_** has a finite impulse response which defines the size of the filter. **An (N-1)th order discrete time FIR filter has N samples.** Its impulse response sequence is defined as follows

![[Pasted image 20251030083748.png]]

The filter, then has _N_ coefficients $a_n$ for $n=0,1,...,N-1$
![[Pasted image 20251030083853.png]]
For et 6th ordens filter som på billedet, kan vi se, at man har **7** parametre, der kan ændres på. Tænk på ligesom i polynomier, hvor man også har en "konstant" til sidst, som udgør én værdi mere end polynomiets orden.

I modsat til [[Direct realization structures]], har vi $b_n = 0$, så vores filter er kun afhængigt af vores input
![[Pasted image 20251030084438.png]]

## Impulse response
![[Pasted image 20251030084932.png]]

Hvis vi tager invers z-transformation af ovenstående $Y(z)$, får vi følgende resultat
![[Pasted image 20251030085036.png]]

**BEMÆRK AT I DET OVENSTÅENDE, skal der i toppen af summen stå $N$ og ikke $N-1$.**
**Det er fordi at der her er tale om antal _samples_, mens der normalt bruges $N$ til at tale om orden af filteret.**



---
#signalprocessing  #filter