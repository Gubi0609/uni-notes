
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

## **Complementary** (komplimentær)
- $E^\complement=s\textbackslash E$  (Det, der **IKKE** er en del af E)

## **Disjoint events** (disjunkt)
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
- $0\leq P(E) \leq 1$ - $P : E\subseteq S \rightarrow [0,1]$ - **Sandsynligheden for at noget sker ligger altid mellem 0 og 1**
- Disjoint events: $E_1\cap E_2=\emptyset\Rightarrow P(E_1\cup E_2)=P(E_1)+P(E_2)$ - **Hvis fællesmængden af $E_1$ og $E_2$ er tom, er sandsynligheden for, at enten $E_1$ eller $E_2$, sker er summen af deres individuelle sandsynlighed**

## Additions regler
- **Sandsynligheden for at enten $E_1$ eller $E_2$ indtræffer:** $P(E_1\cup E_2) = P(E_1) + P(E_2) - P(E_1 \cap E_2)$  (_Læg mærke til, at den for disjoint events også passer her, da $P(E_1 \cap E_2)$ da er 0)
	- $P(A\cup B\cup C) = P(A) + P(B) + P(C) - P(A\cap B) - P(A\cap C) - P(B\cap C) + P(A\cap B\cap C)$ - For flere events (_Vi lægger den samlede intersection til igen, da vi i minus-delen har trukket den fra for meget)_
- **Disjoint set af events:** $E_1, E_2, ..., E_n \quad (E_i \cap E_j =\emptyset)$ 
	- $P(E_1\cup E_2\cup ... \cup E_n)=P(\cup^n_{i=1}E_i)$
- **Komplementær hændelse:** $E^\complement = s\textbackslash E$
	- $P(E^\complement)=1-P(E)$

## Multiplikations regler
- Må ==**KUN**==  ske, hvis $E_1$ og $E_2$ er _uafhængige_
	- $P(E_1\cap E_2)=P(E_1)\cdot P(E_2)$
	- Uafhængighed kan ikke bevises eller ses på data, men skal argumenteres (som f.eks. Hvad er sandsynligheden for at det bliver 15 grader i dag, og at min underviser har grønne sokker på?)
		- Må ikke være i samme sample space, så anderledes fra Disjoint Events, da de er i samme sample space.
		- Temperatur er ét sample space, og farve af sokker er et andet sample space.

## Betinget sandsynlighed
- Events A og B
	- $P(A|B)$ - **Sandsynlighed for A, når B er indtruffet**, _A givet B_
		- Defineret som $\frac {P(A\cap B)}{P(B)}$ 
		- $P(A\cap B)=P(A|B)P(B)$ - **Sandsynligheden for at de begge er indtruffet**
	- A: $T>20^\circ C$ tilfældig dag
	- $B_1$: Dag i januar
	- $B_2$: Dag i august
		- $P(A|B_1)<P(A)<P(A|B_8)$ - **Sandsynligheden for at det bliver over 20 grader er større i august end januar. Sandsynligheden er også større i august end sandsynligheden over hele året ($P(A)$)**
		- Hvis B i stedet var ugedage (mandag, tirsdag, ...), ville B være irrelevant for at finde sandsynligheden for A. Det ville ikke fortælle os meget.

### Multiplikation for betinget sandsynlighed
$$P(A|B)P(B)=P(B|A)P(A)=P(A\cap B)$$

### Total sandsynlighed
Skal have et disjunkt og komplet sæt af events
- $E_1, E_2, ..., E_n$
- $E_i\cap E_j = \emptyset$ - **Disjunkt**
- $E_1 \cup E_2 \cup ... \cup E_n = S$ - **Komplet. Dækker hele sample space**
- Kunne være alle måneder på året. De er disjunkte, da der ikke er nogen dag, der ligger i samme måned, og komplette, da de dækker hele året.

Hvis vi har et event A igen, der er temperaturen, er sandsynligheden for en specifik temperatur
$$P(A)=P(A|E_1)P(E_1) + P(A|E_2)P(E_2)+...+P(A|E_{12})P(E_{12})$$
Hvilket kan generaliseres til $n$
$$P(A)=P(A|E_1)P(E_1) + P(A|E_2)P(E_2)+...+P(A|E_{n})P(E_{n})=\sum^n_{i=1}P(A|E_i)P(E_i)$$
### Bayers formel
Gælder altid.
$$P(A|B)=\frac {P(A\cap B)}{P(B)}=\frac {P(B|A)P(A)} {P(B)}$$
Kan også bruges til sæt ved brug af loven om [[#Total sandsynlighed|total sandsynlighed]]
$$P(E_i|A)=\frac {P(A|E_i)P(E_i)} {P(A)}=\frac {P(A|E_i)P(E_i)}{\sum^n_{i=1}P(A|E_i)P(E_i)}$$


## Combinatorics - Kombinatorik
Tælleregler, der bruges ofte i sandsynligheds regning

### Ordnede sekvenser - Permutation

#### Ordnede sekvenser af $n$
Der er $n$ objekter
- Vi vil finde ud af hvor mange måder, man kan stille dem i forskellig rækkefølge
- $P_n^n = \text{antal ordnede sekvenser af n objekter}$
	- For hver gang man "trækker" op af posen, er der en mindre mulighed
$$P_n^n=n(n-1)(n-2)...2\cdot 1 = n!$$
#### Ordnede sekvenser af $r$
Der er $n$ objekter
- Vi udtager $r$ mængde af objekter
- $P^n_r=\text{antal af uordnede r-sekvenser udtaget blandt n objekter}$
$$P^n_r=n(n-1)(n-2)...(n-(r-1))=\frac {n!}{(n-r)!}$$

### Uordnede sekvenser - Kombinationer
Der er $n$ objekter, vi udtager $r$ blandt $n$
- $C^n_r=\text{antal r-mængder udtaget blandt n}$
$$C^n_r=\frac {P^n_r}


---
#lecture 