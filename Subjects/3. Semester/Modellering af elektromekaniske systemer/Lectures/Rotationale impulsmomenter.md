![[Pasted image 20251104140243.png]]
## Rotation af stift legeme
Et masse element $m_i$ bidrager til impulsmomentet $\vec L_O$ omkring punktet O med
## $$\vec L_{i,O} = \vec r_i \times \vec p_i = m_i\vec r_i \times (\vec\omega \times \vec r_i)$$
![[Pasted image 20251104122507.png]]

Hvis vi lader $\vec r_i = (x_i, y_i, z_i)$ og $\vec \omega = (\omega_x, \omega_y, \omega_z)$ så er
![[Pasted image 20251104122623.png]]
Hvor den første "matrice" betegner determinanten af den matrice (se formen af siderne).

Så kan vi altså få følgende udtryk for $\vec L_{i,O}$
![[Pasted image 20251104122723.png]]

Vi kan omskrive diagonalen i den sidste 3x3 matrix til $I_{xx}, I_{yy}, I_{zz}$:
![[Pasted image 20251104122913.png]]

**Vi kan så skrive det endelige udtryk for $L_O$ som:**
![[Pasted image 20251104123125.png]]
Hvor $\tilde I$ er inertitensoren

## Diagonalisering af inertitensor
Inertitensoren er en symmetrisk matrix, så den kan diagonaliseres:
![[Pasted image 20251104123239.png]]

Hvor de akser, der diagonaliserer $I$ kaldes **hovedakser** eller **principale akser**.

## Perpendicular axis theorem
Hvis vi betragter et plan objekt, hvor z-aksen er vinkelret på objektet mens x- og y-akserne er i planen. Så gælder
## $$I_z=I_x+I_y$$
Hvor $I_x,I_y,I_z$ er inertimomenterne om hver deres akser.

## Eksempler
> [!example]- Eksempel: Udregning af intertitensor for cylinder (I & II)
> ![[Pasted image 20251104123726.png]]
> ![[Pasted image 20251104123750.png]]
> Da vi kigger på _uendeligt små skiver_, kan [[#Perpendicular axis theorem]] bruges, da den gælder for et _plan_ objekt.
> ![[Pasted image 20251104123807.png]]
> ![[Pasted image 20251104123815.png]]

> [!example]- Eksempel: Svinghjul (I)
> Da [[#Perpendicular axis theorem]] gælder for _plane_ objekter, kan vi bruge den i det her eksempel
> ![[Pasted image 20251104123849.png]]

> [!example]- Eksempel: Svinghjul (II)
> ![[Pasted image 20251104123916.png]]
> ![[Pasted image 20251104123929.png]]

Bemærk på **Eksempel: Svinghjul (II)** ovenover, bliver første aksen $e_1$ valgt til at pege _ud_ af objektet. ==DET ER IKKE OMDREJNINGSAKSEN, DET ER STADIG z==. Vi kunne sagtens vælge en anden akse (fx $e_2$eller $e_3$ ), **det vigtige er bare, at den akse vi vælger, ikke ligger parallelt med z-aksen.** Dette er fordi, det så ikke ville være en "skæv" rotation (det ville ende med at være ligesom **Eksempel: Svinghjul (II)**)

---
#physics 