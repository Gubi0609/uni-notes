Vi betragter nedenstående system hvor $O'$ accelerer med $a'$ i forhold til $S$. Desuden roterer $S'$ med en vinkelhastighed på $\omega$ i forhold til $S$.
![[Pasted image 20251009125558.png|700]]

Bevægelsen af partikel $P$ i henførelsessystemet $S$ kan beskrives ved
## $$ \vec r = x\vec e_x + y\vec e_y + z\vec e_z$$
## $$\vec v = \frac {dx}{dt}\vec e_x + \frac {dy}{dt}\vec e_y + \frac {dz}{dt}\vec e_z$$
## $$\vec a = \frac {d\vec v_x}{dt}\vec e_x + \frac {d\vec v_y}{dt}\vec e_y + \frac {d\vec v_z}{dt}\vec e_z$$
Bevægelsen af partikel $P$ i henførelsessystemet $S'$ kan beskrives ved
## $$ \vec r' = x'\vec e'_x + y'\vec e'_y + z'\vec e'_z$$
## $$\vec v' = \frac {dx'}{dt}\vec e'_x + \frac {dy'}{dt}\vec e'_y + \frac {dz'}{dt}\vec e'_z$$
## $$\vec a' = \frac {d^2\vec x'}{dt^2}\vec e'_x + \frac {d^2\vec y'}{dt^2}\vec e'_y + \frac {d^2\vec z'}{dt^2}\vec e'_z$$
Bemærk at $\vec v' \neq d\vec r'/{dt}$ og at $\vec a' \neq d\vec v'/dt$.

> [!example]- Udledning af $dr/dt$ og $dv/dt$
> Hastighed
> ![[Pasted image 20251009131915.png|800]]
>Acceleration
>![[Pasted image 20251009132000.png|800]]
>![[Pasted image 20251009132045.png|800]]
>![[Pasted image 20251009132129.png|800]]

![[Pasted image 20251009132154.png]]

Newtons 2. lov kan benyttes i $S$ da det er et inertialsystem. Så kan accelerationen (billedet ovenover) bruges til at opskrive Newtons 2. lov:
## $$m\vec a = m\vec a_o + m\frac {d\vec\omega}{dt}\times \vec r' + m\vec\omega\times(\vec v' + \vec\omega\times\vec r') + m\vec a' + m\vec\omega\times\vec v' = \vec F_{natur}\quad [N]$$
Hvor $\vec F_{natur}$ er den 

---
#physics #fictive-forces