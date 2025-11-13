Vi betragter nedenstående system hvor $O'$ accelerer med $a'$ i forhold til $S$. Desuden roterer $S'$ med en vinkelhastighed på $\omega$ i forhold til $S$.
![[Pasted image 20251009125558.png|700]]

# Bevægelse af partikler i henførelsessystemer
Bevægelsen af partikel $P$ i henførelsessystemet $S$ kan beskrives ved
## $$ \vec r = x\vec e_x + y\vec e_y + z\vec e_z$$
## $$\vec v = \frac {dx}{dt}\vec e_x + \frac {dy}{dt}\vec e_y + \frac {dz}{dt}\vec e_z$$
## $$\vec a = \frac {d\vec v_x}{dt}\vec e_x + \frac {d\vec v_y}{dt}\vec e_y + \frac {d\vec v_z}{dt}\vec e_z$$
Bevægelsen af partikel $P$ i henførelsessystemet $S'$ kan beskrives ved
## $$ \vec r' = x'\vec e'_x + y'\vec e'_y + z'\vec e'_z$$
## $$\vec v' = \frac {dx'}{dt}\vec e'_x + \frac {dy'}{dt}\vec e'_y + \frac {dz'}{dt}\vec e'_z$$
## $$\vec a' = \frac {d^2\vec x'}{dt^2}\vec e'_x + \frac {d^2\vec y'}{dt^2}\vec e'_y + \frac {d^2\vec z'}{dt^2}\vec e'_z$$
Bemærk at $\vec v' \neq d\vec r'/{dt}$ og at $\vec a' \neq d\vec v'/dt$.

# Hastighed af partikel i henførelsessystemer
> [!example]- Udledning af $d\vec r/dt = \vec v$
> ![[Pasted image 20251009131915.png|800]]
## $$\frac {d\vec r}{dt} = \vec v = (\vec v_o + \vec\omega\times\vec r') + \vec v' \quad [m/s]$$

# Acceleration af partikel i henførelsessystemer
> [!example]- Udledning
> >![[Pasted image 20251009132000.png|800]]
>![[Pasted image 20251009132045.png|800]]
>![[Pasted image 20251009132129.png|800]]

## $$\vec a = \vec a_o + \frac {d\vec\omega}{dt}\times \vec r' + \vec\omega\times(\vec v' + \vec\omega\times\vec r') + \vec a' + \vec\omega\times\vec v'\quad [m/s^2]$$

![[Pasted image 20251009132154.png]]


# Newtons 2. lov i roterende henførelsessystemer
Newtons 2. lov kan benyttes i $S$ da det er et inertialsystem. Så kan accelerationen (billedet ovenover) bruges til at opskrive Newtons 2. lov:
## $$m\vec a = m\vec a_o + m\frac {d\vec\omega}{dt}\times \vec r' + m\vec\omega\times(\vec v' + \vec\omega\times\vec r') + m\vec a' + m\vec\omega\times\vec v' = \vec F_{natur}\quad [N]$$
Hvor $\vec F_{natur}$ er den resulterende kraft, der virker på $P$.

![[Pasted image 20251009132916.png]]


---
#physics #fictive-forces