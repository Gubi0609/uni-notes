
---
**Date:** 2026-11-27

## Preparation

>[!TODO] HOMEWORK
>- [ ] 

> [!DANGER] EXERCISES
> - [ ] 13.2.1, 13.2.2, 13.2.3, 13.2.8

---
# Relevant documents
[[Agenda lecture 11.pdf]]
[[Lektion 11 slides.pdf]]
[[Solutions lecture 11 v2.pdf]]

# Topics


# Notes
![[Pasted image 20261127100827.png]]![[Pasted image 20261127101251.png]]

- a.
Ved at kigge på fakta kassen [[ANOVA 1#ANOVA tabel|i ANOVA 1]] kan vi se at DF Error og DF Total er udregnet som
$$DF_E = a(n-1)$$
$$DF_T=an-1$$
Da vi har resultaterne for dette, har vi to ligninger med to ukendte. Vi kan så udregne antallet af faktor niveauer $a$

$$a(n-1)=16$$
$$an-1=19$$
Ved at løse det i MATLAB får vi
$$a=4$$
$$n=5$$
```matlab
%% 13.2.1
clear; clc; close all;

syms a n

E = [a*(n-1) == 16, a*n - 1 == 19];

solve(E, a, n)
```

- b.
Vi refere til udregningerne i forrige opgave. _Replicates_ er $n$:
$$n=5$$

- c.
Vi referer igen til fakta kassen i [[ANOVA 1#ANOVA tabel|ANOVA 1]].

Vi kan se at DF Faktor er udregnet som $a-1$
$$DF_F=a-1=4-1=3$$
$MS_E$ er mean squares for error. I samme faktorkasse kan vi se at den udregnes
$$MS_E=\frac {SS_E}{a(n-1)}=\frac {396.8}{}


![[Pasted image 20261127100838.png]]

![[Pasted image 20261127100850.png]]

![[Pasted image 20261127100908.png]]



---
#lecture 