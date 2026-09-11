
---
**Date:** 2026-09-11

## Preparation

>[!TODO] HOMEWORK
>- [ ] 

> [!DANGER] EXERCISES
> - [ ] 3.1.10, 3.1.11, 3.2.8, 3.3.1, 3.3.7, 3.4.1, 3.5.2, 3.5.4, 3.5.13, 3.6.1, 3.8.2

---
# Relevant documents
[[Agenda lecture 02.pdf]]
[[Lektion 2 slides.pdf]]
[[Solutions lecture 02 v3.pdf]]

# Topics


# Notes

# Diskrete stokastiske variable & fordelinger
Vi har et _stokastisk eksperiment_ med udfaldsrummet (sample space) S. I S har vi vores udfald e.g. $a_1$

**Stokastiske variable skrives $X$**
$$X : a_i\in S\rightarrow X=x_1$$
![[Pasted image 20260911082136.png|501]]

## Probability mass function, PMF
På dansk hedder det en **sandsynlighedsfunktion**
$$f_X(x_i):=P(X=x_i)$$
![[Pasted image 20260911082544.png|405]]

$$\sum_{x_i\in S} f_X(x_i)=1,\quad 0\leq f_X(x_i)\leq 1$$

## Cumulative probability function, CMF
Adderet fra venstre mod højre.

På dansk: **fordelingsfunktion** (ikke vidt brugt term, brug hellere engelsk)

 $$F_X(x_i):=P(X\leq x_i)=\sum_{x_j\leq x_i} P(X=x_j)=\sum_{x_j \leq x_i} f_X(x_j)$$
 ![[Pasted image 20260911083621.png|472]]
 
$$0\leq F_X(x)\leq 1, \quad \lim_{x\rightarrow -\infty}F_X(x)=0, \quad \lim_{x\rightarrow \infty}F_X(x)=1$$
$$P(x_i< X\leq x_j)=F_X(x_j)-F_X(x_i)$$
Hvis vi derimod også vil have $x_i$ med, skal vi få dens sandsynlighed med også.
$$P(x_i\leq X\leq x_j)=F_X(x_j)-F(x_i)+f_X(x_i)$$
Hvis ingen af dem er med
$$P(x_i<X<x_j)=F_X(x_j)-F_X(x_i)-f_X(x_j)$$
Til sidst, hvis det kun er $x_i$ der er med, og ikke $x_j$
$$P(x_i\leq X<x_j)=F_X(x_j)-F_X(x_i)+f_X(x_i)-f_X(x_j)$$

## Middelværdi (Mean) af X
$$\mu_X=E[X]:=\sum\text{mulige udfald} \cdot \text{sandsynlighed}=\sum_{x_o\in S} x_i\cdot f_X(x_i)$$
$E$ står for _expectation_

Kan opfattes som et **tyngdepunkt** eller _center of gravity **COG**_ (tror jeg)
![[Pasted image 20260911085610.png|444]]

$$E[aX+b]=E[aX]+E[b]=a\cdot\mu_X+b$$
$$E[h(X)]=\sum_{x_i\in S}h(x_i)+f_X(x_i)$$
Forskellige sandsynlighedsfordelinger, kan have samme middelværdi _hvis de e.g. har forskellige spredning om samme punkt (COG)_

## Varians (Variance) af X
Beskriver spredningen af sandsynlighedsfordelingen
$$\sigma_X^2=V[X]=E[(X-\mu_X)^2]=\sum_{x_i\in S}(x_i-\mu_X)^2\cdot f_X(x_i)\geq 0$$
![[Pasted image 20260911090308.png|349]]![[Pasted image 20260911090315.png|350]]

$$\sigma_X^2=E[X^2]+E[\mu_X^2]-2\mu_XE[X]=E[X^2]+\mu_X^2-2\mu_X\cdot\mu_X=E[X^2]-\mu_X^2=\sum_{x_i\in S}x_i^2\cdot f_X(x_i)-\mu_X^2$$
Ligesom før, kan vi lave ekstra matematik med variansen
$$V[aX+b]=V[aX]+V[b]=a^2\sigma_X^2+0$$

### Standardafvigelsen
$$\sigma_X=+\sqrt{\sigma_X^2}$$
Har samme enhed som X

## Case 1: Uniform fordeling
$$X\sim UD(a,b),\quad a,b\in \mathbb{Z}$$
$\sim$ betyder _"fordelt som"_, $UD$ er _navn_ og $a,b$ er _parametre_
![[Pasted image 20260911092919.png]]

$$\text{antal udfald} = b-a+1$$
**[[#Probability mass function, PMF|PMF]]**
$$f_X(x)=\left\{\begin{array} & \frac 1 {b-a+1}, & a\leq x\leq b \\ 0, & \text{ellers}\end{array}\right., \quad x\in \mathbb Z$$
**[[#Middelværdi (Mean) af X|Middelværdi]]**
$$\mu_X=E[X]=\frac {a+b} 2$$
**[[#Varians (Variance) af X|Varians]]**
$$\sigma_X^2=\frac {(b-a+1)^2-1}{12}$$

## Case 2: Binomial fordeling
_Kun 2 mulige udfald:_ **Succes eller fiasko**

$$X\sim \text{Bin}(n,p)$$
$\text{Bin}$ er navnet for _binomial_, $n$ er _antal forsøg_, $p$ er _succes rate_

### Bernouilly forsøg
Betyder: **udført kun _1_ gang**, $n=1$

$$f_X(x)=\left\{\begin{array} & p, & x=1, & \text{succes}\\ 1-p, & x=0, & \text{fiasko}\end{array}\right.$$

**[[#Middelværdi (Mean) af X|Middelværdi]]**
$$\mu_X=E[X]=\sum_{x_i}x_if_X(x_i)=1\cdotp+0\cdot(1-p)=p$$
**[[#Varians (Variance) af X|Varians]]**
$$E[X^2]=\sum_{x_i}x_i^2f_X(x_i)=1^2\cdot p+0^2(1-p)=p$$
$$\sigma_X^2=V[X]=p-p^2=p(1-p)$$
![[Pasted image 20260911094235.png|379]]

### For $n>1$
$$X\sim \text{Bin}(n,p)$$
Udfør $n$ uafhængige af [[#Bernouilly forsøg|Bernouilly forsøg]]
![[Pasted image 20260911094613.png|572]]

$$P(X=x)=P(\text{x succeser blandt n forsøg})=f_X(x)=p^x(1-p)^{n-x}, \quad 0\leq x\leq n$$
hvor $p^x$ er succeserne, og $(1-p)^{n-x}$ sørger for, at resten er fiasko

Vi mangler stadig at tjekke hvor mange forskellige metoder de kan kombineres på
$$P(X=x)=f_X(x)=\left(\begin{array}& n \\ x\end{array}\right)p^x(1-p)^{n-x},\quad 0\leq x\leq n$$
Dette er vores **[[#Probability mass function, PMF|PMF]]**, hvor $x$ er antallet af forsøg (tror jeg...), i ovenstående er
$$\left(\begin{array}& n \\ x\end{array}\right)=\frac {n!}{(n-x)!x!}$$
**[[#Middelværdi (Mean) af X|Middelværdi]]**
$$\mu_X=n\cdot p$$
**[[#Varians (Variance) af X|Varians]]**
$$\sigma_X^2=n\cdot p(1-p)$$

## Case 3: Geometrisk fordeling
$$X\sim\text{Geo}(p)$$
hvor $\text{Geo}$ er navnet _Geometrisk_
$$X:\text{ antal forsøg indtil første succes}$$
![[Pasted image 20260911095847.png]]

_Vi stopper forsøget, når vi får vores første succes_

**[[#Probability mass function, PMF|PMF]]**
$$f_X(x)=1-p^{x-1}\cdot p,\quad 1\leq x\leq \infty$$
hvor $x$ er antal forsøg

**[[#Middelværdi (Mean) af X|Middelværdi]]**
$$\mu_X=E[X]=\frac 1 p$$

**[[#Varians (Variance) af X|Varians]]**
$$\sigma_X^2=V[X]=\frac {1-p}{p^2}$$

## Case 4: Poisson fordeling
Bruges til **ankomstprocesser**

Vi måler **ankomstintensiteten** $\lambda$ med enheden $s^{-1}$

$$X\sim \text{Poisson}(\lambda),\quad \lambda \geq 0$$
$$f_X(x)=P(\text{x ankomster i }[0,t])=\frac {(\lambda t)}{},\quad 0\leq x\leq\infty, \quad x\in\mathbb N$$





---
#lecture 