![[Pasted image 20251104140338.png]]
## Rotationsmatrix
En rotationsmatrix er en 3x3 matrix, hvor følgende gælder $R \in \mathbb R^{3\times 3}$ .

For rotation om x-aksen er rotationsmatrixen:
![[Pasted image 20251104133602.png]]

Og rotationen:
![[Pasted image 20251104133615.png]]
hvor x-aksen peger ud af skærmen.

Rotationsmatricer er ortogonale matricer med determinant 1. Det betyder:
* Ortogonal matrix: $RR^T=I(R^{-1}=R^T)$
* Determinant: $det(R)=1$

![[Pasted image 20251104133757.png]]

## Homogen transformation
En transformations matrix er en $4\times 4$ matrix:
![[Pasted image 20251104133824.png]]
![[Pasted image 20251104133930.png]]

Hvis vi vil beskrive et punkt $p^1$ i 0's koordinatramme, kan vi finde $p^0$ således:
![[Pasted image 20251104134141.png]]

## Hastighed
For at beskrvie bevægelsen af en robot, må vi kunne beskrive dens hastighed.
For at opstille formler for den lineære hastighed af værktøjet $\dot p_e$ og dens vinkelhastighed $\vec \omega_e$ på følgende form
![[Pasted image 20251104134318.png]]
og $n$ er antallet af led i robot(armen).

### Den tidsafledte af en rotationsmatrix
![[Pasted image 20251104134428.png]]

Så kan vi udregne hastigheden af punktet $q$ givet ved
$$\vec q=R(t)\vec p$$
hvor $\vec p$ er en konstant vektor og R(t) er en rotationsmatrix.

Så bliver hastigheden
## $$ \vec q=\dot R(t) \vec p=S(t)R(t)\vec p$$
Vi ved desuden at
![[Pasted image 20251104134645.png]]

Så kan $S(t)$ findes til at være
![[Pasted image 20251104134716.png]]

## Hastighed af punkt i anden ramme
![[Pasted image 20251104134847.png]]

## Link hastighed
Vi har følgende link
![[Pasted image 20251104135000.png]]

### Translatorisk link hastighed
Positionen for origo af ramme $i$ er
![[Pasted image 20251104135053.png]]

Så får vi hastigheden til
![[Pasted image 20251104135133.png]]

### Vinkelhastighed af link
![[Pasted image 20251104135151.png]]

==For dette (og det nedenstående) vil subscriptet "$i-1,i$" betyde $i$ set fra $i-1$ (fx hastigheden af i set fra i-1)==
### Link hastighed (drejeled)
![[Pasted image 20251104135238.png]]

## Jakobiant for drejeled
For dette system
![[Pasted image 20251104135309.png]]

Kan vi skrive Jakobiantens translatoriske del som
![[Pasted image 20251104135354.png]]

Når vi betragter [[#Link hastighed (drejeled)|drejeled]] får vi
![[Pasted image 20251104135502.png]]
(Lineær hastighed for drejeled)

For selv samme system, kan Jakobiantens rotationelle del skrives
![[Pasted image 20251104135542.png]]

Og når vi betragter [[#Link hastighed (drejeled)|drejeled]] får vi
![[Pasted image 20251104135442.png]]
(Vinkelhastighed af drejeled)
Læg mærke til, at det er sådan, fordi vi _kun_ roterer om z-aksen i dette eksempel

Samlet bliver jakobianten så
![[Pasted image 20251104135622.png]]


---
#physics #kinematics 