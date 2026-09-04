Tælleregler, der bruges ofte i sandsynligheds regning

# Ordnede sekvenser - Permutation

## Ordnede sekvenser af $n$
Der er $n$ objekter
- Vi vil finde ud af hvor mange måder, man kan stille dem i forskellig rækkefølge
- $P_n^n = \text{antal ordnede sekvenser af n objekter}$
	- For hver gang man "trækker" op af posen, er der en mindre mulighed
$$P_n^n=n(n-1)(n-2)...2\cdot 1 = n!$$
## Ordnede sekvenser af $r$
Der er $n$ objekter
- Vi udtager $r$ mængde af objekter
- $P^n_r=\text{antal af uordnede r-sekvenser udtaget blandt n objekter}$
$$P^n_r=n(n-1)(n-2)...(n-(r-1))=\frac {n!}{(n-r)!}$$
# Uordnede sekvenser - Kombinationer
Der er $n$ objekter, vi udtager $r$ blandt $n$
**Vi er ligeglade med rækkefølgen ting er blevet trukket, men vil kun se det endelige resultat**
- E.g. _Vi er ligeglad med hvilken rækkefølge vi slår seks 6'ere i yahtzee, kun at vi slår seks 6'ere

- $C^n_r=\text{antal r-mængder udtaget blandt n}$
$$C^n_r=\frac {P^n_r}{r!}=\frac {n!}{(n-r)!r!}$$
**I 9/10 tilfælde er det uordnede sekvenser, der er relevant.**
