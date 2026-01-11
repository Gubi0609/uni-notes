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
## $$\omega(t)=v(t)=\dot x(t)=-\sqrt{\frac g l}l\sin\left(\sqrt{\frac g l t}\right)$$
og slutteligt accelerationen for god ordens skyld
## $$\dot\omega(t)=a(t)=\dot v(t)=\ddot x(t)=-\frac g ll\cos\left(\sqrt{\frac g l}t\right)=-\frac g lx(t)$$
Vi kan udregne den kinetiske og potentielle energi for systemet

Den potentielle energi må være afhængig af tyngdekraften og positionen fra $\theta=0$
## $$E_{pot}=mgy_p=mgl(1-\cos(\omega_0t))$$
og
## $$E_{kin}=\frac 1 2 mv^2=\frac 1 2m(-\omega_0Asin(\omega_0t))^2=\frac 1 2m(\omega_0Asin(\omega_0t))^2$$
Da har vi også
## $$E_{mek}=E_{pot}+E_{kin}=mgl(1-\cos(\theta)+\frac 1 2 m(\omega_0A\sin(\omega_0t))^2$$ $$E_{mek}=mgl(1-\cos(\omega_0t))+\frac 1 2m\omega_o^2A^2\sin^2(\omega_0t)$$
Der udnyttes nu at $\omega_0^2=g/l$ og at $A=l$
## $$E_{mek}=mgl(1-\cos(\omega_0t))+\frac 1 2 mgl\sin^2(\omega_0t))$$ $$E_{mek}=mgl(1-cos(\omega_0t)+\frac 1 2\sin^2(\omega_0t))$$
# Fjeder-Masse system
![[Pasted image 20260111191531.png]]
IGNORER DÆMPEREN OG x

Dette er en [[Simpel harmonisk svingning]].
## $$\ddot x(t)=-\Phi x(t)$$
Vi kan opstille følgende for kraften i systemet
## $$F_k=ma=-kx$$
altså er
## $$a=\ddot x=-\frac k m x$$
Derved er
## $$\Phi=\frac k m$$
og vinkelfrekvens samt svingningstid bliver
## $$\omega_0=\sqrt{\frac k m}\quad\text{og}\quad T=2\pi\sqrt{\frac m k}$$
Vi kan nu opstille positionen og hastigheden (samt den endelige acceleration)
## $$x(t)=A\cos(\omega_0t+\phi)=A\cos(\omega_0t)$$ $$v(t)=\dot x(t)=-\omega_0A\sin(\omega_0t)$$ $$a(t)=\ddot x(t)=-\omega_0^2A\cos(\omega_0t)$$
Den kinetiske energi for systemet er
## $$E_{kin}=\frac 1 2 mv^2=\frac 1 2 m(-\omega_0A\sin(\omega_0t))^2=\frac 1 2 m\omega_0^2A^2\sin^2(\omega_0t)$$
Den potentielle energi er
## $$E_{pot}=\frac 1 2kx^2=\frac 1 2kA^2\cos^2(\omega_0t)$$

Så bliver den mekaniske energi
## $$E_{mek}=E_{pot}+E_{kin}=\frac 1 2kA^2\cos^2(\omega_0t)+\frac 1 2m\omega_0^2A^2\sin^2(\omega_0t)$$ $$E_{mek}=\frac 1 2 A^2(k\cos^2(\omega_0t)+m\omega_0^2\sin^2(\omega_0t))$$
Nu udnyttes at $\omega_0^2=k/m$
## $$E_{mek}=\frac 1 2 A^2(m\omega_0^2\cos^2(\omega_0t)+m\omega_0^2\sin^2(\omega_0t))$$ $$E_{mek}=\frac 1 2 A^2 m\omega_0^2(\cos^2(\omega_0t)+\sin^2(\omega_0t))=\frac 1 2A^2m\frac k m(1)=\frac 1 2A^2k$$
## Lagrange
Ud fra kinetisk og potentiel energi, kan vi også opstille systemet via Euler-Lagrange
## $$\mathscr{L} = E_{kin}-E_{pot}$$ $$\mathscr L=\frac 1 2kA^2\sin^2(\omega_0t)-\frac 1 2 kA^2\cos^2(\omega_0t)=-\frac 1 2kA^2$$
## $$\frac d {dt}*\frac {\delta\mathscr L} {\delta \dot x} -\frac {\delta\mathscr L} {\delta x} = Q$$


# Fjeder-masse-dæmper
![[Pasted image 20260111191531.png]]
IGNORER  x

Dette er en [[Dæmpet simpel harmonisk svingning]]