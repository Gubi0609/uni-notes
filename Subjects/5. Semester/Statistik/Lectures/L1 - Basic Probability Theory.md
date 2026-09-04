
---
**Date:** 2026-09-04

## Preparation

>[!TODO] HOMEWORK
>- [ ] 

> [!DANGER] EXERCISES
> - [ ] 2.1.13, 2.1.22, 2.2.7, 2.2.10, 2.3.8, 2.4.2, 2.5.2, 2.5.7, 2.6.5, 2.7.4, 2.7.11-12, 2.8.1

---
# Relevant documents
[[Lektion 1 slides.pdf]]
[[Agenda lecture 01.pdf]]
[[Solutions lecture 01 v3.pdf]]

# Topics
[[Sandsynlighed Basics]]
[[Betinget Sandsynlighed]]
[[Kombinatorik]]

# Notes
![[Pasted image 20260904104432.png]]
![[Pasted image 20260904104413.png]]

![[Pasted image 20260904104500.png]]
- a. $A\cap B = 12 + 44 = 56$
- b. $A' = 56+36 = 92$ 
- c. $A\cup B =12 + 44 + 40 + 16 + 56 = 168$
- d. $A\cup B' = 12 + 40 + 44 + 16 + 36 = 148$
- e. $A'\cap B' = 36$

![[Pasted image 20260904105058.png]]
- a. Vi er ligeglad med sekvensen, så det er et kombinatorik problem. $n=140$, $r=5$, fejlen $k=10$
$$C^n_r=\frac {P^n_r}{r!}=\frac {n!}{(n-r)!r!} = \frac {140!} {(140-5)!5!}=416965528$$
- b.Vi har nu to events, og vil tælle den uordnede kombination i hver. $E_1$ er de dårlige chips, vi har en sample size på 10, og tager 1 op hver gang. $E_2$ er de gode chips. Her har vi en sample size på 130, og tager 4 op hver gang. Vi kan gange de individuelle antal sammen.
$$\frac {10!}{1!(10-1)!}\cdot \frac {130!} {4!(130-4)!}=113588800$$
- c. Vi kan starte med at finde alle antal af kombinationer (opgave a), og så trækker de kombinationer fra, hvor vi _kun_ trækker gode.
$$\frac {140!} {(140-5)!5!}-\frac {130!} {(130-5)!5!} = 130721752$$

![[Pasted image 20260904111631.png]]
- a. Her har rækkefølgen betydning, da chipsene har forskellige funktioner. Det er permutation
$$P^n_r=\frac {n!}{(n-r)!}=\frac {12!}{(12-5)!}=95040$$
- b. Her har chipsene samme funktion, så det er uordnet. Her bruger vi kombinatorik igen.
$$C^n_r=\frac {P^n_r}{r!}=\frac {n!}{(n-r)!r!} =\frac {12!}{(12-5)!5!}= 792$$

![[Pasted image 20260904112249.png]]
- a.
$$P(A)=\frac {N_n(A)}{n}=\frac {70+16} {70+16+9+5}=\frac {86}{100}=0.86$$
- b.
$$P(B)=\frac {N_n(B)}{n}=\frac {70+9} {70+16+9+5}=\frac {79}{100}=0.79$$
- c.
$$P(A')=\frac {N_n(A')}{n}=\frac {9+5} {70+16+9+5}=\frac {14}{100}=0.14$$
- d.
$$P(A\cap B)=\frac {N_n(A\cap B)}{n}=\frac {70} {70+16+9+5}=\frac {70} {100} =0.70$$
- e.
$$P(A\cup B)=\frac {N_n(A\cup B)}{n}=\frac {70+16+9} {70+16+9+5}=\frac {95}{100}=0.95$$
- f.
$$P(A'\cup B)=\frac {N_n(A'\cup B)}{n}=\frac {70+9+5} {70+16+9+5}=\frac {84}{100}=0.84$$

![[Pasted image 20260904113158.png]]
- a.
$$P(A')=1-P(A)=0.7$$
- b.
$$P(A\cup B) = P(A) + P(B) - P(A \cap B)=0.3+0.2-0.1=0.4$$
- c.
$$P(A'\cap B)=P(B)-P(A\cap B)=0.2-0.1=0.1$$
- d.
$$P(A\cap B')=P(A)-P(A\cap B)=0.3-0.1=0.2$$
- e.
$$P[(A\cup B)']=1-0.4=0.6$$
- f.
$$P(A'\cup B)=P(A')+P(B)-P(A'\cap B) = 0.7+0.2-0.1=0.8$$

![[Pasted image 20260904114309.png]]
- a.
$$P(A)=$$


---
#lecture 