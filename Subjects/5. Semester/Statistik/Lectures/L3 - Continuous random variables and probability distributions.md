
---
**Date:** 2026-09-18

## Preparation

>[!TODO] HOMEWORK
>- [ ] 

> [!DANGER] EXERCISES
> - [ ] 4.1.2, 4.2.4, 4.3.1, 4.4.1, 4.5.1, 4.5.4, 4.5.13, 4.6.1, 4.7.13

---
# Relevant documents
[[Agenda lecture 03.pdf]]
[[Lektion 3 slides.pdf]]
[[Solutions lecture 03 v3.pdf]]

# Topics


# Notes

Ligesom [[Diskrete stokastiske variable & fordelinger]] har vi et sample space $S$ og et sæt af stokastiske variable $X$.
$$X: S\rightarrow I\subseteq \mathbb R$$

# Probability *Density* Function, PDF
På dansk kunne man kalde det en sandsynligheds-*tætheds* funktion

Skrevet $f_X(x)$ ligesom [[Diskrete stokastiske variable & fordelinger#Probability mass function, PMF|PMF]].
![[Pasted image 20260918082149.png|284]]

$$f_X(x):=\frac {P(X\in[x,x+dx])}{dx}$$
![[Pasted image 20260918082328.png|309]]
$$P(a\leq X\leq b)=\int_a^b f_X(x)dx$$

$f_X(x)$ er _likelihood_.

Der gælder
$$\int_{-\infty}^\infty f_X(x)dx=1\quad [P(s)=1]$$
$$f_X(x)\geq 0$$

Da vi bruger integraler her, gælder der også
$$P(X=x)=0$$
Da arealet for et specifikt x-punkt er 0.

# Cumulative Probability Density Function, CDF
På dansk: fordelingsfunktion

Skrevet $F_X(x)$.
$$F_X(x):=F(X\leq x)=\int_{-\infty}^xf_X(u)du$$
![[Pasted image 20260918083233.png|323]]

_Svagt monoton_, stiger langsomt. Starter i 0, og stiger til 1.

Vi kan finde $f_X(x)$ fra $F_X(x)$
$$f_X(x)=\frac {dF_X(x)}{dx}\geq 0$$

$$\lim_{x\rightarrow -\infty}F_X(x)=0$$
$$\lim_{x\rightarrow \infty}F_X(x)=1$$
Det ovenover skriver bare, at den starter i 0 og slutter i 1.

$$P(a\leq X\leq b)=\int_a^b f_X(x)dx=F_X(b)-F_X(a)$$
I modsætning til [[Diskrete stokastiske variable & fordelinger#Cumulative probability function, CMF|CMF]] behøver vi ikke fire forskellige udgaver af ovenstående formel. Noget med Dirac Delta, som vi ikke bruger. Anyways, det virker bare!

# Middelværdi (Mean) af X
Skrevet $\mu_X$

$$\mu_X=E[X]=\int_{-\infty}^\infty x\cdot f_X(x)$$
Hvor $E[X]$ er _forventet værdi_ eller _expectancy_
![[Pasted image 20260918084209.png|369]]

Man kan også tænke på middelværdien som _tyngdepunkt_. Hvis vi have en længere hale, ville tyngdepunktet blive påvirket meget af den, og altså rykke sig længere langs den.

$$E[h(x)]=\int_{-\infty}^\infty h(x)\cdot f_X(x)dx$$
hvor $h(x)$ er en tilfældig funktion af $x$.

# Varians (Variance) af X
Bruges til at beskrive spredningen(ikke helt sikker på, at det er det rigtige ord at bruge), da flere kan have samme [[#Middelværdi (Mean) af X|middelværdi]] men anderledes varians
![[Pasted image 20260918084723.png]]

$$\sigma^2=V[X]:=E[(X-\mu_X)^2]=E[X^2]-\mu_X^2 =\int_{-\infty}^\infty (x-\mu_X)^2\cdot f_X(x) dx\geq 0$$

Hvis vi i stedet for $X^2$ bruger $X^3$ hedder det _skewness_, men det bruger vi ikke rigtig.
## Standardafvigelse
$$\sigma_X=+\sqrt{\sigma_X^2}$$
Har samme enhed som $X$.

# Case 1: Uniform fordeling
_Continuos uniform distribution_
Betyder at alle udfald er lige sandsynlige
$$X\sim U(a,b)\quad a,b\in \mathbb R$$

I matlab, skrives `x=a+b*rand`. `rand` generer et tilfældigt tal mellem 0 og 1.

## PDF
![[Pasted image 20260918085853.png|366]]
Arealet under grafen er 1. Dette er i henhold til [[#Probability *Density* Function, PDF|PDF]].

$$f_X(x)=\left\{\begin{array} &  \frac 1 {b-a} & a\leq x \leq b \\ 0 & ellers \end{array}\right.$$

## CMF
![[Pasted image 20260918090124.png|357]]

## Middelværdi
Middelværdien ligger nødvendigvis i midten, da alle udfald i mellem a og b er lige sandsynlige
$$\mu_X=E[X]=\frac {a+b}2$$
## Varians
$$\sigma^2=V[X]=\frac {(b-a)^2}{12}$$
Kommer af den generelle formel for [[#Varians (Variance) af X|Varians]], men vi gider ikke udlede det.


---
#lecture 