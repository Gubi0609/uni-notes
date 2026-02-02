
# Indmad
![[Pasted image 20260202083957.png]]

# Modkoplingsprincippet
For en ideel op amp som følgende
![[Pasted image 20260202084042.png]]

Vil det gælde at output spændingen er
## $$V_o=A_{OL}V_{id}$$
hvor $A_{OL}$ er _gain open loop_

Gain vil gå mod uendelig, hvis
## $$V_{id}=e_+-e_-=0\Leftrightarrow e_+=e_-$$

Dette kalder vi **modkoplingsprincippet

## Negativ feedback
![[Pasted image 20260202084253.png]]

For negativ feedback gælder [[Den ideelle Op Amp#Modkoplingsprincippet|modkoplingsprincippet]] også.

Den positive og negative indgangsspænding vil via det negative feedback kredsløb prøve at stabilisere sig, således at de er ens
## $$e_+=e_-$$

$V_o$ for et negativt feedback kredsløb med negativ indgangsspænding er
## $$V_o=-\frac {R_2}{R_1}\cdot V_{in}$$

> [!example]- Negativ feedback kredsløb
> ![[Pasted image 20260202084548.png]]
> 1. Kredsløb med negativ feedback og negativ $V_{in}$
> $$V_o=-\frac{R_2}{R_1}\cdot V_{in}$$
> 2. Kredsløb med negativ feedback og positiv $V_{in}$
> Vi ved at der skal være 0 V mellem positiv og negativ indgang. Vi kan derfor opstille $R_1$ og $R_2$ som en spændingsdeler mellem $V_o$ og GND
> $$V=\frac {R_1}{R_1+R_2}\cdot V_o$$
> Da vi som sagt har at positiv og negativ indgangsspænding er ens, må $V_{in}$ være lig med dette udtryk. Så kan vi bare isolere
> $$V_{in}=\frac {R_1}{R_1+R_2}\cdot V_o\Leftrightarrow V_o=\frac {R_1+R_2}{R_1}V_{in}$$
> 3. Kredsløb med negativ feedback og to negative $V_{in}$
> Vi bruger [[Kirschoffs current law]] der siger at summen af strømme ind i en node (samling) er ligmed summen af strømme ud af en node. Vi kigger på negativ indgang som noden
> $$\frac {V_1}{R_1}+\frac {V_2}{R_2}+\frac {V_o}{R_f}=0\Leftrightarrow V_o=-R_f\left(\frac {V_1}{R_1}+\frac {V_2}{R_2} \right)$$
> 4. Negativ feedback med modstand mellem indgange
> Vi kan se bort fra $R_x$ da der er 0 V _mellem_ indgangene. Derfor er kredsløbet det samme som kredsløb 1
> $$V_o=-\frac {R_2}{R_1}\cdot V_{in}$$
> 5. Negativ feedback med positiv indgangsspænding og modstand på $V_o$
> 6. Negativ feedback med positiv indgangsspænding og modstand i parallel med $R_2$

---
#electronics 