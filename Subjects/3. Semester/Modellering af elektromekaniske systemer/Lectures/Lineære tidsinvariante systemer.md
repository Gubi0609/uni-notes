
# Egenskaber
## Linearitet
## $$f(x+y)=f(x)+f(y) \quad \text{Superposition}$$$$f(\alpha x) = \alpha f(x) \quad \text{Homogenitet}$$
> [!example]- Eksempel på linearitet
> Tag følgende eksempel med input $u_1$, $u_2$, og $u_1+u_2$, og output $y_1$, $y_2$, og $y_1+y_2$
> Vi kan se at *Superposition* gælder, da $u_1+u_2$ producerer output $y_1+y_2$
> ![[Pasted image 20260108195851.png]]


## Tidsinvarians
## $$y(t-\tau)=\sigma(t,u(t-\tau))$$
for alle tider $t\in \mathbb{R}$, hvor $y$ betegner udgangsignalet for systemet, $\sigma$ er indgangs signalet, og $u$ er... ja det ved jeg faktisk ikke

> [!example]- Eksempel på tidsinvariant system
> Kanonens opførsel her ændrer sig ikke an på om den bliver affyret klokken 15 eller klokken 18
> ![[Pasted image 20260108200647.png]]

![[Pasted image 20260108200756.png]]

På ovenstående kan vi se, at input $p_{1,0}+p_{2,0}$ producerer output $p_1+p_2$.

# Respons
Det ønskes at finde et lineært systems input-output opførsel.

Det er muligt at bestemme et lineær systems respons til ethvert input $u$ ud fra kendskab til systemets impulsrespons.

## Impuls
Konceptet af en **impuls** $\delta(t)$ indføres. _Dette er et meget kort og kraftigt signal, der har følgende egenskaber_.
## $$\int^\infty_{-\infty}u(\tau)\delta(t-\tau)d\tau=u(t)$$
hvor $u$ er en kontinuerlig funktion og $\delta$ er en **Dirac delta-funktion**.

Udtrykket kan tolkes som en vægtet sum af impulser, der giver funktionen $u(t)$, dvs. hvis systemets respons til en impuls kendes, så kan systemets respons til $u(t)$ findes som en sum af impulser, grundet **superpositionsprincippet**.


**Impulsresponset** $h(t,\tau)$ for et lineært system defineres som responset (outputtet) til tiden $t$ når en impuls et tilføjet som input til tiden $\tau$.
_Hvis systemet er tidsinvariant, kan impulsresponset defineres ud fra $t-\tau$. I dette tilfælde skrives $h(t-\tau)$._

## Superpositionsintegralet
## $$y(t)=\int^\infty_{-\infty}u(\tau)h(t,\tau)d\tau$$
Gælder for lineære systemer (pga. superpositionsprincippet)

## Foldningsintegralet
## $$y(t)=\int^\infty_{-\infty}u(\tau)h(t-\tau)d\tau=\int^\infty_{-\infty}u(t-\tau)h(\tau)d\tau$$
Gælder for lineære tidsinvariante systemer

## Eksempel på impulsrespons
> [!example]-
> ![[Pasted image 20260108201838.png]]
> ![[Pasted image 20260108201856.png]]
> ![[Pasted image 20260108201909.png]]


## Enheds step funktion
## $$1(t)=$$

---
#math #physics #signalprocessing 