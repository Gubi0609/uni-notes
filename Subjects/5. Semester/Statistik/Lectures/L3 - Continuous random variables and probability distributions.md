
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
[[Kontinuerte stokastiske variable & fordelinger]]

# Notes

# Exercises
![[Pasted image 20260918102344.png]]

Til alle opgaverne bruges
$$P(a\leq X\leq b)=\int_a^b f_X(x)dx$$
Nedre grænse må være $1$ (se opgave beskrivelse) og øvre grænse må være $\infty$

- a.
$$P(1\leq X<2)=\int_{1}^2 \frac 2 {x^3} dx=\left[-\frac 1 {x^2}\right]_1^2=-\frac 1 {2^2}-\left(-\frac 1 {1^2}\right)=-\frac 1 4+\frac 1 1=\frac 1 3$$
- b.
$$P(5<X<\infty)=\left[-\frac 1 {x^2}\right]_5^\infty=-\frac 1 {\infty^2}-\left(-\frac 1 {5^2}\right)=0+\frac 1 {25}=\frac 1 {25}$$
- c.
$$P(4<X<8)\left[-\frac 1 {x^2}\right]_4^8=-\frac 1{8^2}-\left(-\frac 1 {4^2}\right)=-\frac 1 {64}+\frac 1 {16}=-\frac {16}{1024}+\frac {64}{1024}=\frac {48}{1024}=\frac 3 {64}$$

- d.
$$P(1<X<4 \text{ or }8<X<\infty)=P(1<X<4)\cup P(8<X<\infty)$$
Der er tale om [[Sandsynlighed Basics#**Disjoint events** (disjunkt)|disjoint events]] da deres område ikke overlapper. Vi kan derfor bare addere de individuelle sandsynligheder
$$P(1<X<4)=\left[-\frac 1 {x^2}\right]_1^4=-\frac 1 {4^2}-\left(-\frac 1 {1^2}\right)=1-\frac 1 8=\frac 7 8$$
$$P(8<X<\infty)=\left[-\frac 1 {x^2}\right]_8^\infty=-\frac 1 {\infty^2}-\left(\frac 1 {8^2}\right)=0+\frac 1 {64}=\frac 1 {64}$$

$$P(1<X<4 \text{ or }8<X<\infty)=\frac 7 8+\frac 1 {64}=\frac {56}{64}+\frac 1 {64}=\frac {57}{64}$$

- e.
Vi har
$$P(1<X<x)=\left[-\frac 1 {x^2}\right]_1^x=-\frac 1 {x^2}-\left(-\frac 1 {1^2}\right)=1-\frac 1 {x^2}=0.95$$
Hvor vi skal isolere $x$. Det gider jeg sgu ikke gøre i hånden, så det bliver matlab.
$$x=4.47214$$



![[Pasted image 20260918102358.png]]

$$F_X(x):=F(X\leq x)=\int_{-\infty}^xf_X(u)du$$

Vi har allerede integreret, så vi skal bare indsætte variablerne
$$F_X(x)\left[-\frac 1 {x^2}\right]_{-\infty}^x=-\frac 1 {x^2}-\left(-\frac 1 {(-\infty)^2}\right)=- \frac 1 {x^2}$$


![[Pasted image 20260918102420.png]]

Vi bruger
$$\mu_X=E[X]=\int_{-\infty}^\infty x\cdot f_X(x)=\int_{-1}^1 x\cdot 1.5\cdot x^2$$
og løser i matlab


![[Pasted image 20260918102433.png]]

![[Pasted image 20260918102444.png]]

![[Pasted image 20260918102459.png]]

![[Pasted image 20260918102514.png]]

![[Pasted image 20260918102528.png]]

---
#lecture 