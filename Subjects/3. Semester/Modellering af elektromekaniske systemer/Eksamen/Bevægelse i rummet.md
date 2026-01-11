- Beskrivelse af translation og rotation
- Opstilling af bevægelsesligninger for mekaniske systemer
- Harmoniske svingninger
- Beskrivelse af hastighed og acceleration (bl.a. ved brug af Jakobianten)

# Pendul
![[Pasted image 20260111121420.png]]

## $$F_t=mg$$
positionen (i y-aksen) kan skrives
## $$x(t)=l\cos(\theta t)$$
så bliver hastigheden
## $$v(t)=\dot x(t)=-\theta l\sin(\theta t)$$
og accelerationen
## $$a(t)=\dot v(t)=\ddot x(t)=-\theta^2 l\cos(\theta t)=-\theta^2x(t)$$

og kraften fra pendulet (isoleret) bliver
## $$ma(t)=-\theta^2mx(t)=-\theta^2ml\cos(\theta)$$

Dette tager dog kun højde for pendulet, og ikke tyngdekraften, så det bliver i stedet
## $$F_{net}=F_p-F_t=-\theta^2ml\cos(\theta t)-mg$$
og $a(t)$ bliver således
## $$a(t)=\ddot x(t)=F_{net}=-\theta^2l\cos(\theta t)-g$$
hvilket betyder at $v(t)$ må blive
## $$v(t)=\int a(t)d\theta=-\theta^3\sin$$