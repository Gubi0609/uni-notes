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
## $$\mathscr{L} = E_{kin}-E_{pot}$$ $$\mathscr L=\frac 1 2kA^2\sin^2(\omega_0t)-\frac 1 2 kA^2\cos^2(\omega_0t)=\frac 1 2kA^2(\sin^2(\omega_0t)-\cos^2(\omega_0t)$$ $$\mathscr L=\frac 1 2kA^2(sin^2(\theta)-\cos^2(\theta))$$
## $$\frac d {dt}*\frac {\delta\mathscr L} {\delta \dot\theta} -\frac {\delta\mathscr L} {\delta \theta} = Q$$
==HUSK LIGE HER AT DU HAR TO LIGNINGER GANGET SAMMEN==
## $$\frac {\delta\mathscr L}{\delta \dot\theta}=\frac {\delta\mathscr L}{\delta \dot\theta}\left(\frac 1 2m\omega_0^2A^2(\sin^2(\omega_0t)-\cos^2(\omega_0t)\right)$$ $$=m\omega_0A^2t(\frac 1 2(1-\cos(2\omega_0t))-\frac 1 2(1+\cos(2\omega_0t)))$$ $$=\frac 1 2m\omega_0A^2t(1-\cos-1-\cos)=\frac 1 2m\omega_0A^2t(-2\cos(\omega_0t))$$$$\frac {\delta\mathscr L}{\delta \dot\theta}=-\omega_0A^2t\cos(\omega_0t)$$

# Fjeder-masse-dæmper
![[Pasted image 20260111191531.png]]
IGNORER  x

Dette er en [[Dæmpet simpel harmonisk svingning]]

Kraften kan skrives
## $$m\ddot x=-kx-b\dot x$$
og kan omskrives til
## $$\ddot x+\gamma \dot x+\omega_0^2x=0$$
hvor 
## $$\gamma = \frac b m \quad\text{og}\quad \omega_0^2=\frac k m$$
Vi kan opstille rødderne
## $$R=-\frac \gamma 2\pm j\sqrt{\omega_0^2-\frac{\gamma^2}4}$$
og prøve at indsætte værdier forskellige værdier for $k$ og $b$ for at lave forskellige løsninger

## Dæmpet svingning
$\omega_0^2>\gamma^2/4\rightarrow \omega_d\in\mathbb{R}$ hvor $\omega_2=\sqrt{\omega_0^2-\frac{\gamma^2}4}$
$b=4$, $m=1$, $k=8$
$\gamma=4/1=4$, $\omega_0^2=8/1=8$
## $$R=-\frac 4 2\pm j\sqrt{8-\frac{4^2}4}=-2\pm j\sqrt{8-4}=-2\pm j\sqrt{4}=-2\pm j2$$
Så er løsningen for $x(t)$
## $$x(t)=Ae^{-\gamma t/2}\cos (\omega_d t+\phi)$$ $$x(t)=Ae^{-2t}\cos(2t+\phi)$$
hvis vi har at $x(0)=5$, kan vi prøve at løse for $A$. Vi sætter $\phi=0$
## $$5=Ae^0\cos(0)=A*1*1=A\Leftrightarrow A=5$$
altså afhænger $A$ af begyndelsesbetingelsen (når $\phi=0$).
## Aperiodisk grænsetilfælde
$\omega_0^2=\gamma^2/4\rightarrow \omega_d=0$
$b=4$, $m=1$, $k=4$
$\gamma=4/1=4$, $\omega_0^2=4/1=4$

## $$R=-\frac 4 2\pm j\sqrt{4-\frac {4^2}4}=-2\pm j\sqrt{4-4}=-2$$

Så er løsningen $x(t)$
## $$x(t)=Ae^{-\gamma t/2}+Be^{-\gamma t/2}=Ae^{-2t}+Be^{-2t}$$
## Aperiodisk svingning
$\omega_0^2<\gamma^2/4\rightarrow\omega_d\in\mathbb{C}$
$b=8$, $m=1$, $k=4$
$\gamma=8/1=8$, $\omega_0^2=4/1=4$

## $$R=-\frac 8 2\pm j\sqrt{4-\frac {8^2} 4}=-4\pm j\sqrt{4-16}=-4\pm j\sqrt{-12}$$ $$R=-4\pm j^2\sqrt{12}=-4\pm\sqrt{12}$$

Så er løsningen $x(t)$
## $$x(t)=Ae^{(-4+\sqrt{12})t}Be^{(-4-\sqrt{12})t}$$

## Bevægelsesligninger
Vi tager udgangspunkt i en dæmpet svingning
## $$v(t)=\dot x(t)=\frac d {dt}(Ae^{-\gamma t/2}\cos (\omega_d t+\phi))$$ $$v(t)=-A\frac \gamma 2e^{-\gamma t/2}\cos(\omega_dt+\phi)-Ae^{-\gamma t/2}\omega_d\sin(\omega_dt+\phi)$$
og accelerationen
## $$a(t)=\ddot x(t)=\dot v(t)=\frac d{dt}(-A\frac \gamma 2e^{-\gamma t/2}\cos(\omega_dt+\phi)-Ae^{-\gamma t/2}\omega_d\sin(\omega_dt+\phi))$$ $$a(t)=A\frac {\gamma^2}4e^{-\gamma t/2}\cos(\omega_dt+\phi)+A\frac \gamma 2e^{-\gamma t/2}$$

## Energi
Den kinetiske energi for systemet er (for en dæmpet svingning)
