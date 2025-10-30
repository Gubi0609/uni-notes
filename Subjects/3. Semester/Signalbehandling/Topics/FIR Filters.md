> A **_finite impulse response filter (FIR filter)_** has a finite impulse response which defines the size of the filter. **An (N-1)th order discrete time FIR filter has N samples.** Its impulse response sequence is defined as follows

# FIR Design summary
![[Pasted image 20251030102033.png]]

# FIR filter
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
hvor $\gamma = f/f_0$ og $f_0$ er Nyquist frekvensen.
Nyquist: $f_0 = f_s/2$ 

$a_M$ i midterste ligning, er amplituden af den midterste værdi.

## Example
![[Pasted image 20251030094207.png]]
$M = 5$ fordi vi starter fra 0, så midten er $0,1,2,3,4,5$.

![[Pasted image 20251030095126.png]]
![[Pasted image 20251030095345.png]]

## Design of FIR filter
**Fourier transform of impulse response = frequency response of the desire filter**

# Fourier transform of a FIR filter
![[Pasted image 20251030100037.png]]
![[Pasted image 20251030100243.png]]

### Example Low pass filter
![[Pasted image 20251030100945.png]]
**FEJL: Når vi omskriver integralet til ikke at gå fra $-f_s/2$ til $f_s/2$ om til $0$ til $f_0$ skal der egentlig stå $f_a$ i stedet for $f_0$.**
![[Pasted image 20251030101357.png]]
![[Pasted image 20251030101703.png]]

### Example High pass filter
![[Pasted image 20251030101919.png]]

### Example Bandpass filter
![[Pasted image 20251030101941.png]]

### Example Bandstop filter
![[Pasted image 20251030101957.png]]

# Window functions in FIR
![[Pasted image 20251030102930.png]]
Betyder basically, at vi bare koncentrerer os på _et vindue_ af vores signal. Jeg vil gå ud fra, at det er fordi signalet bare en periodisk gentagelse af dette vindue.

**Truncate betyder, at hvis man har et signal/noget som helst, så beholder man noget af det (vinduet...) og fjerner resten** Total mindblowing.

### Typical window functions
 Rectangular window
 Bartlett window
 Hamming window
 Hanning window
 Kaiser window

# Frequency response
![[Pasted image 20251030103711.png]]
![[Pasted image 20251030103821.png]]
![[Pasted image 20251030103859.png]]
![[Pasted image 20251030103909.png]]

# Window functions continued
### Rectangle window
![[Pasted image 20251030104419.png]]

### Bartlett window
![[Pasted image 20251030104432.png]]

### Hamming and Hanning window
![[Pasted image 20251030104452.png]]
![[Pasted image 20251030104510.png]]
**Der er en meget lille forskel på de to billeder her, men kig på stavelsen ud for grafen, og at der er en _lille bitte_ forskel på begge grafer.** Fuck det her.

### Kaiser window
![[Pasted image 20251030104635.png]]
![[Pasted image 20251030104644.png]]

### MatLab functions
- `bartlett(L)`
- `hammming(L)`
- `hann(L)`
- `kaiser(L, beta)`

## Design procedure
The construction of an FIR filter can proceed according to the following procedure
1. **Select window.** This selection is made according to the specified stopband and passband ripple.
2. **Determine filter order.** The filter order 2𝑀𝑀 is determined from the transition band ∆𝑓𝑓𝑎𝑎
3. **Calculate filter coefficients.** The filter coefficients are calculated as $𝑎_𝑖 = 𝑐_{m−i} \omega_{𝑀−𝑖}$
4. **Verification.** The amplitude characteristic of the filter is checked and, if necessary, the filter redesigned (M-value is corrected).

## Specs of a FIR filter
When designing an FIR filter, the following must be specified
1. The cut-off frequency $f_a$
2. Maximum permissible width o transition area $\Delta f_a$ 
3. Maximum permissible stopband gain $H_s$
4. Maximum permissible pass band ripple $H_r$ 

## Determination of filter order
When designing an FIR filter, its length cannot be determined exactly in advance.
Normally, we try different values and see whether the filter can achieve our desired filter specifications.
![[Pasted image 20251030105320.png]]
![[Pasted image 20251030105509.png]]



---
#signalprocessing  #filter