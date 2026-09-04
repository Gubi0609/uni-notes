- Events A og B
	- $P(A|B)$ - **Sandsynlighed for A, når B er indtruffet**, _A givet B_
		- Defineret som $\frac {P(A\cap B)}{P(B)}$ 
		- $P(A\cap B)=P(A|B)P(B)$ - **Sandsynligheden for at de begge er indtruffet**
	- A: $T>20^\circ C$ tilfældig dag
	- $B_1$: Dag i januar
	- $B_2$: Dag i august
		- $P(A|B_1)<P(A)<P(A|B_8)$ - **Sandsynligheden for at det bliver over 20 grader er større i august end januar. Sandsynligheden er også større i august end sandsynligheden over hele året ($P(A)$)**
		- Hvis B i stedet var ugedage (mandag, tirsdag, ...), ville B være irrelevant for at finde sandsynligheden for A. Det ville ikke fortælle os meget.

# Multiplikation for betinget sandsynlighed
$$P(A|B)P(B)=P(B|A)P(A)=P(A\cap B)$$

# Total sandsynlighed
Skal have et disjunkt og komplet sæt af events
- $E_1, E_2, ..., E_n$
- $E_i\cap E_j = \emptyset$ - **Disjunkt**
- $E_1 \cup E_2 \cup ... \cup E_n = S$ - **Komplet. Dækker hele sample space**
- Kunne være alle måneder på året. De er disjunkte, da der ikke er nogen dag, der ligger i samme måned, og komplette, da de dækker hele året.

Hvis vi har et event A igen, der er temperaturen, er sandsynligheden for en specifik temperatur
$$P(A)=P(A|E_1)P(E_1) + P(A|E_2)P(E_2)+...+P(A|E_{12})P(E_{12})$$
Hvilket kan generaliseres til $n$
$$P(A)=P(A|E_1)P(E_1) + P(A|E_2)P(E_2)+...+P(A|E_{n})P(E_{n})=\sum^n_{i=1}P(A|E_i)P(E_i)$$
# Bayers formel
Gælder altid.
$$P(A|B)=\frac {P(A\cap B)}{P(B)}=\frac {P(B|A)P(A)} {P(B)}$$
Kan også bruges til sæt ved brug af loven om [[#Total sandsynlighed|total sandsynlighed]]
$$P(E_i|A)=\frac {P(A|E_i)P(E_i)} {P(A)}=\frac {P(A|E_i)P(E_i)}{\sum^n_{i=1}P(A|E_i)P(E_i)}$$

