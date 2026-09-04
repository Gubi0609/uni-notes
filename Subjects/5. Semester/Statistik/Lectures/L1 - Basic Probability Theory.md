
---
**Date:** 2026-09-04

## Preparation

>[!TODO] HOMEWORK
>- [ ] 

> [!DANGER] EXERCISES
> - [ ] 

---
# Relevant documents
[[Lektion 1 slides.pdf]]
[[Agenda lecture 01.pdf]]
[[Solutions lecture 01 v3.pdf]]

# Topics


# Notes
Stokastisk eksperiment er et eksperiment med ukendt udfald
- Har et udfaldsrum (Sample space **S**), som indeholder mængden af alle _mulige_ udfald
	- S kan være diskret eller kontinuert

Event **E** (hændelse)
- Kombination af udfald
	- Enten udfald 1 eller 2: $E=a_1\vee a_2$

## **Union** (foreningsmængde)
-  $E_1 \cup E_2$ (Det der er i den ene, den anden, eller dem begge to) - **Egentlig bare en `OR`**

## **Intersection** (fællesmængde)
- $E_1 \cap E_2$ (Det der er i det område, hvor $E_1$ og $E_2$  _overlapper_) - **En `AND` operation**

## **Complementary**
- $E^\complement=s\textbackslash E$  (Det, der **IKKE** er en del af E)

## **Disjoint events**
- $E_1\cap E_2=\emptyset=\{\}$ (Events som ikke kan opstå på samme tid) - **Ingen fællesmængde**


## Definition af sandsynlighed
- Stokastisk eksperiment
	- Udført $n$ gange
	- Leder efter et event $E$
		- Kunne være at kaste med en terning 100 gange ($n$) og se hvor mange gange man slår 6 ($E$)
	- $N_n(E)=\text{antal gange ud af n hvor E indtræffer}$
	- $P(e)=\lim_{n\rightarrow\infty}\frac {N_n(E)}n$ - **Sandsynligheden for at $E$ sker.**

## Aksiomer
- $P(\emptyset)=0$ - **Sandsynligheden for at der ikke kommer et udfald er 0**
- $P(S) = 1$ - **Sandsynligheden for at der sker noget, når man udfører et eksperiment er 1 (Der skal ALTID ske noget)**
- $0\leq P(E) \leq 1$ - **Sandsynligheden for at noget sker ligger altid mellem 0 og 1**


---
#lecture 