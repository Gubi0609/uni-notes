
# Indmad
![[Pasted image 20260202083957.png]]

# Modkoblingsprincippet
For en ideel op amp som følgende
![[Pasted image 20260202084042.png]]

Vil det gælde at output spændingen er
## $$V_o=A_{OL}\cdot V_{id}=V_{in}\cdot\alpha-V_{id}\cdot A_{OL}\cdot\beta$$
hvor $A_{OL}$ er _gain open loop_

Vi har nogle lidt lange udtryk i det ovenstående. Vi kan formulere 

Gain vil gå mod uendelig, hvis
## $$V_{id}=e_+-e_-=0\Leftrightarrow e_+=e_-$$

Dette kalder vi **modkoblingsprincippet

Forstærkningen for en modkoblet op amp er
## $$A_{CL}=\frac \alpha \beta$$
Formlerne for $\alpha$ og $\beta$ kan ses i [[Den Realistiske Op Amp]].

# Negativ feedback
![[Pasted image 20260202084253.png]]

For negativ feedback gælder [[Den ideelle Op Amp#Modkoblingsprincippet|modkoblingsprincippet]] også.

Den positive og negative indgangsspænding vil via det negative feedback kredsløb prøve at stabilisere sig, således at de er ens
## $$e_+=e_-$$

$V_o$ for et negativt feedback kredsløb med negativ indgangsspænding er
## $$V_o=-\frac {R_2}{R_1}\cdot V_{in}$$

> [!example]- Negativ feedback kredsløb
> ![[Pasted image 20260202084548.png]]
> 1. **Kredsløb med negativ feedback og negativ $V_{in}$**
> $$V_o=-\frac{R_2}{R_1}\cdot V_{in}$$
> 2. **Kredsløb med negativ feedback og positiv $V_{in}$**
> Vi ved at der skal være 0 V mellem positiv og negativ indgang. Vi kan derfor opstille $R_1$ og $R_2$ som en spændingsdeler mellem $V_o$ og GND
> $$V=\frac {R_1}{R_1+R_2}\cdot V_o$$
> Da vi som sagt har at positiv og negativ indgangsspænding er ens, må $V_{in}$ være lig med dette udtryk. Så kan vi bare isolere
> $$V_{in}=\frac {R_1}{R_1+R_2}\cdot V_o\Leftrightarrow V_o=\frac {R_1+R_2}{R_1}V_{in}$$
> 3. **Kredsløb med negativ feedback og to negative $V_{in}$**
> Vi bruger [[Kirschoffs current law]] der siger at summen af strømme ind i en node (samling) er ligmed summen af strømme ud af en node. Vi kigger på negativ indgang som noden
> $$\frac {V_1}{R_1}+\frac {V_2}{R_2}+\frac {V_o}{R_f}=0\Leftrightarrow V_o=-R_f\left(\frac {V_1}{R_1}+\frac {V_2}{R_2} \right)$$
> 4. **Negativ feedback med modstand mellem indgange**
> Vi kan se bort fra $R_x$ da der er 0 V _mellem_ indgangene. Derfor er kredsløbet det samme som kredsløb 1
> $$V_o=-\frac {R_2}{R_1}\cdot V_{in}$$
> 5. **Negativ feedback med positiv indgangsspænding og modstand på $V_o$**
> Vi kan indsætte en "fiktiv" spænding ved Op Ampens udgang. Vi kalder den $V_1$. Dette laver en spændingsdeler med $V_{in}$
> $$V_1=\frac{R_1+R_2}{R_1}\cdot V_{in}$$
> og vi kan bruge denne til at udregne spændingen over $V_o$ som også er en spændingsdeler
> $$V_o=\frac {R_L}{R_x+R_L}\cdot V_1$$
> De to ligninger kan nu sættes sammen
> $$V_o=\frac {R_L}{R_x+R_L}\cdot\frac{R_1+R_2}{R_1}\cdot V_{in}$$
> 6. **Negativ feedback med positiv indgangsspænding og modstand i parallel med $R_2$**
> Vi laver igen den "fiktive" spænding fra Op Ampens udgang. Vi bruger desudne [[Kirschoffs current law]] til at beskrive strømmen i noden efter $R_x$. Vi ser desuden også at strømmen ud af den opad-gående ledning må være afhængig af $R_1+R_2$
> $$\frac {V_1}{R_x}-\frac {V_o}{R_L}-\frac {V_o}{R_1+R_2}=0$$
> Der er noget med ligesom i **2'eren** men så langt har jeg ikke regnet endnu.

> [!example]- Negativ feedback kredsløb (med værdier)
> ![[Pasted image 20260202092823.png]]
> a. **Negativ feedback med strømforsyning**
> Vi gør brug af [[Kirschoffs current law]] igen til at analysere noden ved negativ indgang.
> $$I_{in}+\frac {V_o}{R_1}=0$$
> Vi kan så isolere $V_o$ og indsætte værdier
> $$V_o=-I_{in}\cdot R_1=-0.002 A\cdot 2000 \Omega =-4 V$$
> b. **Negativ feedback med strømforsyning og positiv spændingsforsyning** 
> Vi ved at strømmen på Op Ampens indgange skal være 0 A, derved ved vi at alt strømmen fra $I_{in}$ må løbe over $R_2$ ([[Kirschoffs current law]]). Vi ved desuden at der er en 0 V forskel på de to indgange, så derfor må spændingen ved den negative indgang være 5 V.
> Vi kan så finde spændingen over $R_2$ vha. strømmen, og $V_o$ må nødvendigvis være spændingen ved den negative indgang minus spændingen over $R_2$ (Da alt strømmen løber i gennem $R_2$ hvilket sidder i serie med $V_o$).
> $$V_o=5 V-3000 \Omega\cdot0.001A=5 V-3 V=2V$$
> c. **Negativ feedback med positiv spændingsforsyning**
> Vi kan bruge ligningen fra **kredsløb 2** i forrige opgaver
> $$V_o=\frac {R_1+R_2}{R_1}\cdot V_{in}=\frac {3000\Omega +4000\Omega}{4000\omega}\cdot 4 V=\frac 7 4 \cdot 4V=7 V$$
> d. **Negativ feedback med strømforsyning ved $V_o$**
> Da den positive indgangsspænding er 0 (går direkte til GND) må den negative indgangsspænding dermed også være 0.
> Dermed er
> $$V_o=0V$$
> e. **Negativ feedback med positiv spændingsforsyning og spændingsforsyning på feedback loop**
> Da der skal være den samme spænding på begge indgange, må der også være 3 V på den negative indgang.
> Da vi har en 2 V forsyning på den negative indgang forbundet på feedback loopet, må
> $$V_o=1 V$$
> da den negative indgang så vil være
> $$2 V+1 V=3 V$$

# Kaskadekobling
![[Pasted image 20260202100851.png]]

Op Amps kan kaskadekobles for at få deres samlede gain.
Man kan også udregne [[Subjects/4. Semester/Forstærkerteknik og fejlberegninger/Topics/Decibel|Decibel]] for sådan en kaskadekobling.

# Forstærker model
![[Pasted image 20260202101622.png]]

En Op Amp (forstærker) kan ses på ovenstående måde.

Da vi nu har både en _indgangsmodstand_ og _udgangsmodstand_ bevæger vi os væk fra den ideelle Op Amp

> [!example]- Kaskadekoblet forstærker model
> ![[Pasted image 20260202101949.png]]
> I sidste ende er $A_3$ belastet med en modstand på 1 k$\Omega$.
> Find spændingsforstærkningen ($A_v = v_o /v_{i1}$) og strømforstærkningen ($A_i = i_o /i_{i1}$).
> Hvad bliver den overordnede spændings- og strømforstærkning i dB?
> 
> Vi kan se at der i hver forstærker er en _spændingsdeler_ mellem $R_{o}$ og $R_i$.
> Dermed har vi for den første forstærker
> $$v_{i2}=A_1\cdot v_{i1}=11\cdot v_{i1}$$
> Og da $R_{o1}=0\Omega$ er der ikke ligefrem en spændingsdeler der
> $$v_{i3}=11\cdot(-10)\cdot v_{i1}$$
> Her har vi heller ikke en spændingsdeler mellem $R_{o2}$ og $R_{i3}$ (da $R_{o2}=0\Omega$)
> $$v_o=11\cdot(-10)\cdot 5.5\cdot v_{i1}$$
> Dette er dog ikke helt rigtigt, da der er en spændingdeler mellem $R_{o3}$ og $R_L$. Dette må vi tage højde for
> $$v_o=11\cdot(-10)\cdot 5.5\cdot\frac {R_L}{R_{o3}+R_L}\cdot v_{i1}=11\cdot(-10)\cdot 5.5\cdot\frac {1000\Omega}{20\Omega+1000\Omega}\cdot v_{i1}$$
> $$v_0=11\cdot(-10)\cdot 5.5\cdot\frac {100}{102}\cdot v_{i1}$$
> Dermed bliver _voltage gain_
> $$A_v=\frac {v_o}{v_{i1}}=11\cdot(-10)\cdot 5.5\cdot\frac {100}{102}=-593.14$$
> 
> Dernæst må _current gain_ regnes.
> Vi må starte med at finde $I_{i1}$. Til dette bruger vi [[Subjects/4. Semester/Forstærkerteknik og fejlberegninger/Topics/Ohms lov|Ohms lov]].
> $$I_{i1}=\frac {v_{i1}}{R_{i1}}=\frac {v_{i1}}{100000\Omega}$$
> $I_o$ kan findes på samme måde
> $$I_o=\frac{v_o}{R_L}=\frac {11\cdot(-10)\cdot 5.5\cdot\frac {100}{102}\cdot v_{i1}}{1000\Omega}$$
> Dermed må _current gain_ være
> $$A_I=\frac {I_o}{I_{i1}}=\frac {\frac {11\cdot(-10)\cdot 5.5\cdot\frac {100}{102}\cdot v_{i1}}{1000\Omega}}{\frac {v_{i1}}{100000\Omega}}$$
> Da $v_{i1}$ står i både tæller og nævner går det ud med hinanden
> $$A_I=\frac {11\cdot(-10)\cdot 5.5\cdot\frac {100}{102}\cdot v_{i1}\cdot 100000\Omega}{v_{i1}\cdot 1000\Omega}=\frac {11\cdot(-10)\cdot 5.5\cdot\frac {100}{102}\cdot 100000\Omega}{1000\Omega}=-59313.73$$
> 
> Vi kan se at current gain (for dette kredsløb) er $A_I=A_v\cdot100$.

---
#electronics 