- Beskrivelse af translation og rotation
- Opstilling af bevægelsesligninger for mekaniske systemer
- Harmoniske svingninger
- Beskrivelse af hastighed og acceleration (bl.a. ved brug af Jakobianten)

# Pendul
![[Pasted image 20260111121420.png]]

Dette er en [[Simpel harmonisk svingning]]

For simple harmoniske bevægelser gælder
## $$\frac {d^2\theta}{dt^2}=\ddot \theta(t)=-\Phi\theta(t)$$
Accelerationen er udelukkende afhængig af tyngdeaccelerationen og vinklen, derfor må den være
## $$\ddot \theta=-\frac g l\sin(\theta)$$
Hvis vi antager, at der er at gøre med små vinkler, kan vi approksimere med $\sin\theta\approx\theta$.
## $$\ddot\theta\approx-\frac g l\theta$$
Så har vi altså reglen for en simpel harmonisk bevægelse opfyldt, og
## $$\Phi=\frac g l$$
Så bliver vinkelfrekvensen og svingningstiden
## $$\omega_0=\sqrt{\frac g l}\quad\text{og}\quad T=2\pi\sqrt{\frac l g}$$

Vi kan nu opstille positionen
## $$x(t)=A\cos(\omega_0t+\phi)=l\cos\left(\sqrt{\frac g l}t\right)$$
hastigheden
## $$\omega(t)=v(t)=\dot x(t)=\sqrt{\frac g l}l\sin\left(\sqrt{\frac g l t}\right)$$
og slutteligt accelerationen for god ordens skyld
## $$\dot\omega(t)=a(t)=\dot v(t)=\ddot x(t)=-\frac g ll\cos\left(\sqrt{\frac g l}t\right)=-\frac g lx(t)$$
Vi kan udregne den kinetiske og potentielle energi for systemet

Den potentielle energi må være afhængig af tyngdekraften og positionen fra $\theta=0$
## $$E_{pot}=\frac 1 2 gx^2=\frac $$
