
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

Lagrangian er noget, der bliver udledt/opstillet for _hele det samlede system_ og IKKE for _punkter_ eller _delsystemer_ i systemet.

> [!example]- Eksempel: Masse-fjeder system
> ![[Pasted image 20251125123438.png]]
> $m\ddot x = f_{net}$
> Læg mærke til at det endelige udtryk indeholder $m\ddot x$. Det er fordi vi tager den tidsafledte af $m\dot x$.

> [!example]- Eksempel: Roterende masse-fjeder system
> ![[Pasted image 20251125123515.png]]
> $I_1\ddot \theta_1 = I_1\dot\omega_1 = \tau_{net}$
> Vær lige opmærksom på, at når man opstiller $I_1\ddot\theta_1$ er det **MEGET** vigtigt at rækkefølgen af theta trukket fra hinanden er rigtig. For $E_{pot}$ er det ligemeget, fordi det alligevel bliver opløftet i 2.
> 
> ![[Pasted image 20251125123522.png]]

> [!example]- Eksempel: Pendul på Vogn
> ![[Pasted image 20251125125428.png]]
> Svar: 2. Rotational og translatorisk
> 
>![[Pasted image 20251125125505.png]]
>På fritlegeme-diagrammet kan vi se de to frihedsgrader.
>Bemærk at $E_{pot}$ indeholder $y_p$ som altså er y koordinatet for pendulet.
>For den kinetiske energi, har den ledet $\frac 1 2 J_p \dot \theta ^2$. Det kan fjernes hvis man ikke tager højde for stangens inertimoment.
>
>![[Pasted image 20251125125551.png]]
>![[Pasted image 20251125125603.png]]


# Ikke-konservative systemer