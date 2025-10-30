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
Når man laver et filter, er det derfor vigtigt at definere, hvad N står for, da der er forskellige metoder at gøre det på.

### Matlab funktion
##### `conv(input_sig, fir_filter, 'same');`
![[Pasted image 20251030085536.png]]

Vi kan se, at Gausian FIR filter, virker som et low pass filter, da signalet _ligner_ vores originale signal, bare uden høj frekvens støj.
1st Differential FIR viser hvor vi har en "kant" i signalet. Vi kan se, at den ligger omkring 0, indtil vores signal har en kant _op_, så er der en lille spike i filteret. Det samme sker, når vi går _ned_ og _op_ i midten, og _ned_ hen mod enden.

## Poles and Zeros
![[Pasted image 20251030092052.png]]

Det følgende eksempel er for et ottende ordens FIR filter
![[Pasted image 20251030092310.png]]

## Linear phase
Et FIR filter med $N\geq 2$  samples, har _linear phase_, hvis den er symmetrisk om midtpunktet
![[Pasted image 20251030092546.png]]

## Amplitude and Phase
![[Pasted image 20251030093639.png]]
hvor $\gamma = f/f_0

---
#signalprocessing  #filter