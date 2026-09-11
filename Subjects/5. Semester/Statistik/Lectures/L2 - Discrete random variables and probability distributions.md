
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

Kan opfattes som et **tyngdepunkt** eller __



---
#lecture 