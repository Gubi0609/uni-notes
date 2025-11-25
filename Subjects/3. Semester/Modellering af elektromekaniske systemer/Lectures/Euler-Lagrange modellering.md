
# Konservative systemer
Indeholder konservative krafter
	Uafhængigt af vejen vil summen af krafter være 0, når du starter og slutter samme sted (tyngdekraften, fjederkraft osv)

## Newton-Euler Modellering
## $$ W = \int^B_AF(x)\quad dx$$
> [!example]- Eksempel med fjederkraft
> ## $$F_f(x)=-kx$$
> ## $$W_f = \int^{x_2}_{x_1}-kx\quad dx$$
> ## $$=-\frac k 2 [x^2]^{x_2}_{x_1}=0$$

## Euler-Lagrange Modellering
Benyttes til at finde en dynamisk model for et mekanisk system ud fra systemets potentielle energi og kinetiske energi.

Vi benytter _Lagrangian_ $\mathscr{L}$ 

## $$\mathscr{L} = E_{kin}-E_{pot}$$

Vi modellerer med _n_ frihedsgrader. Disse er givet af værdierne for _n **generaliserede koordinater**_ $q_1,....,q_n$

De generaliserede koordinater skal være
- **Minimale**
- **Uafhængige**
  Hvis alle undtagen et koordinat fastholdes, så skal det sidste koordinat kunne tage værdier i et kontinuerligt område.
- **Fuldstændige**
  Kunne beskrive alle konfigurationer til alle tider

_Skal overholde specifikke krav, men er i dette kursus bare positioner og vinkler for systemerne._

![[Pasted image 20251125123159.png]]
Bemærk at hele systemet er afhængig af vektorer og _0_ her er en **nul vektor**.

> [!example]- Eksempel: Masse-fjeder system
> ![[Pasted image 20251125123438.png]]

> [!]
# Ikke-konservative systemer