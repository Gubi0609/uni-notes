
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
$$MS_E=\frac {SS_E}{a(n-1)}=\frac {396.8}{4(5-1)}=24.8$$

$F_{\text{faktor}}$ er $f_0$ som er den _observerede_ test statistic. hvor $F_0$ er
$$F_0:=\frac {S_B^2}{S_W^2}\sim F(a-1, N-a)$$
$MS$ er det samme som de $S$ vi ser her. Oversættelsen er $S_W^2\rightarrow MS_E$, $S_B^2\rightarrow MS_{Tm}$.
$$f_0=\frac {MS_{Tm}} {MS_E}=\frac {39.1} {24.8}=1.5766$$
$p$-værdien er 
$$P(F_0>f_0)=1-P(F(a-1,N-1)<f_0)$$
Den kan vi finde i MATLAB `fcdf(f_0, a-1, N-a)`.
$$p\text{-value}=0.2340$$

Tabellen bliver så

| Source | DF  | SS    | MS   | F      | P-value |
| ------ | --- | ----- | ---- | ------ | ------- |
| Factor | 3   | 117.4 | 39.1 | 1.5766 | 0.2340  |
| Error  | 16  | 396.8 | 24.8 |        |         |
| Total  | 19  | 514.2 |      |        |         |

```matlab
a = 4;
n = 5;

N = a*n;

MS_Tm = 39.1;

SS_F = 117.4;
SS_E = 396.8;
SS_T = 514.2;

DF_E = 16;
DF_T = 19;

DF_F = a-1

MSE = 396.8/(4*(5-1))

f_0 = MS_Tm/MSE

p = 1 - fcdf(f_0, a-1, N-a)
```

- d.

Vi kan se fra factor level means i ANOVA tabellen, at der ikke er betydelig forskel. Derfor kan vi ikke forkaste $H_0$.
Standard for en "lille" p-værdi er 5%. Vi har nu en på 23.4%, så den er altså _ikke_ lille, og vi kan ikke forkaste $H_0$.


![[Pasted image 20261127100838.png]]

- a.

Vi ved at 
$$DF_T=31=an-1$$

Siden vi kender $a=4$ fra opgave beskrivelsen, kan vi bare løse for n
$$n=8$$

- b.

Vi starter med at finde Degrees of Freedom, da de er nemme.
$$DF_F = a-1 = 3$$
$$DF_E = a(n-1)=28$$

Med den information vi har indtil videre kan vi nu finde $p$-værdien
$$P(F_0>f_0)=1-P(F(a-1,N-1)<f_0)$$
Den kan vi finde i MATLAB `fcdf(f_0, a-1, N-a)`.
$$p=0.0115$$

Vi kan nu udregne $MS_E$
$$F_0=MS_{Tm}/MS_E\Leftrightarrow MS_E=MS_{Tm}/F_0=\frac{330.4716}{4.42}=74.7673$$

Til sidst har vi nu alt den information vi skal bruge for at udregne Sum of Squares ($SS$) for alle felter
$$SS_{Tm}=MS_{Tm}\cdot DF_F=330.4716\cdot 3=991.4148$$
$$SS_E=MS_E\cdot DF_E = 74.7673\cdot28 = 2093.5$$
$$SS_T=SS_{Tm}+SS_E=991.4148+2093.5=3084.9$$

Vi kan så udfylde tabellen.

| Source | DF  | SS       | MS       | F    | P-value |
| ------ | --- | -------- | -------- | ---- | ------- |
| Factor | 3   | 991.4148 | 330.4716 | 4.42 | 0.0115  |
| Error  | 28  | 2093.5   | 74.7673  |      |         |
| Total  | 31  | 3084.9   |          |      |         |

- c.
Da standarden for en "lille" p-værdi er 5% og $p<0.05$ samtidig med at der er en betydelig forskel i de to $MS$ værdier, kan vi konkludere, at vi _forkaster_ $H_0$.


![[Pasted image 20261127100850.png]]

- a.


![[Pasted image 20261127100908.png]]



---
#lecture 