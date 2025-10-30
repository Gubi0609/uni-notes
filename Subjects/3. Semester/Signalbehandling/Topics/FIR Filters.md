> A **_finite impulse response filter (FIR filter)_** has a finite impulse response which defines the size of the filter. **An (N-1)th order discrete time FIR filter has N samples.** Its impulse response sequence is defined as follows

![[Pasted image 20251030083748.png]]

The filter, then has _N_ coefficients $a_n$ for $n=0,1,...,N-1$
![[Pasted image 20251030083853.png]]
For et 6th ordens filter som på billedet, kan vi se, at man har **7** parametre, der kan ændres på. Tænk på ligesom i polynomier, hvor man også har en "konstant" til sidst, som udgør én værdi mere end polynomiets orden.

I modsat til [[Direct realization structures]], har vi $b_n = 0$, så vores filter er kun afhængigt af vores input
![[Pasted image 20251030084438.png]]



---
#signalprocessing  #filter