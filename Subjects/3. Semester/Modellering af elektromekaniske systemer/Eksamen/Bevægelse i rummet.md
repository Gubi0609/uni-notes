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
## $$\mathscr{L} = E_{kin}-E_{pot}$$$$\frac d {dt}*\frac {\delta\mathscr L} {\delta \dot x} -\frac {\delta\mathscr L} {\delta x} = Q$$

hvor $Q$ er de ikke-konservative krafter, hvilket i dette system er $Q=0$

## $$E_{kin}=\frac 1 2 m\dot x^2\quad\text{og}\quad E_{pot}=\frac 1 2kx^2$$
så
## $$\mathscr L=\frac 1 2m\dot x^2-\frac 1 2kx^2$$
og dermed
## $$\frac {\delta\mathscr L} {\delta x}=-kx$$ $$\frac {\delta\mathscr L} {\delta \dot x}=m\dot x$$
Slutteligt
## $$0=\frac d{dt}m\dot x-(-kx)=m\ddot x+kx\Leftrightarrow m\ddot x=-kx$$

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
## $$a(t)=\ddot x(t)=\dot v(t)=\frac d{dt}(-A\frac \gamma 2e^{-\gamma t/2}\cos(\omega_dt+\phi)-Ae^{-\gamma t/2}\omega_d\sin(\omega_dt+\phi))$$ $$a(t)=A\frac {\gamma^2}4e^{-\gamma t/2}\cos(\omega_dt+\phi)+A\frac \gamma 2e^{-\gamma t/2}\omega_d\sin(\omega_dt+\phi)+A\frac \gamma 2e^{-\gamma t/2}\omega_d\sin(\omega_dt+\phi)-Ae^{-\gamma t/2}\omega_d^2\cos(\omega_dt+\phi)$$ $$a(t)=Ae^{-\gamma t /2}(\frac {\gamma^2}4\cos(\omega_dt+\phi)-\omega_d^2\cos(\omega_dt+\phi))+ \gamma\omega_d\sin(\omega_dt+\phi))$$

## Energi
Den kinetiske energi for systemet er 
## $$E_{kin}=\frac 1 2 mv^2$$ $$E_{kin}=\frac 1 2 m(Ae^{-\gamma t/2}(\omega_d\sin(\omega_dt+\phi)-\frac \gamma 2\cos(\omega_dt+\phi)))^2$$ $$E_{kin}=\frac 1 2 mA^2e^{-\gamma t}(\omega_d\sin-\frac \gamma 2\cos)^2$$ $$E_{kin}=\frac 1 2mA^2e^{-\gamma t}(\omega_d^2\sin^2+\frac {\gamma^2}4\cos^2-2\sin\cos)$$
Den potentielle energi er afhængig af positionen
## $$E_{pot}=\frac 1 2kx^2=\frac 1 2k(Ae^{-\gamma t/2}\cos (\omega_d t+\phi))^2=\frac 1 2kA^2e^{-\gamma t}\cos^2(\omega_dt+\phi)$$

# Euler-Lagrange
Dette er en model med en ikke konservativ kraft.
Vi har derfor
## $$E_{kin}=\frac 1 2 m\dot x^2\quad\text{og}\quad E_{pot}=\frac 1 2kx^2$$
og Lagrange modellering:
## $$\mathscr{L} = E_{kin}-E_{pot}$$
## $$\frac d {dt}*\frac {\delta\mathscr L} {\delta \dot x} -\frac {\delta\mathscr L} {\delta x} = Q$$
hvor $Q$ er de ikke-konservative krafter $Q=-b\dot x$
## $$\mathscr L=\frac 1 2m\dot x^2-\frac 1 2kx^2$$
## $$\frac {\delta\mathscr L}{\delta x}=-kx$$
## $$\frac {\delta\mathscr L}{\delta\dot x}=m\dot x$$
dermed
## $$-b\dot x=\frac d {dt}m\dot x-(-kx)=m\ddot x+kx\Leftrightarrow m\ddot x=-kx-b\dot x$$


# Fjeder-Masse-Dæmper-Kraft
![[Pasted image 20260111191531.png]]

Dette er en [[Tvunget harmonisk bevægelse]]
## $$m\ddot x=-kx-b\dot x+F$$
hvor $F=F_0\cos(\omega_tt)$. Vi sætter her $\omega_t=0$, så $F$ er noget, der kun sker én gang, og altså
## $$F=F_0$$
Vi kan så skrive
## $$\ddot x+\gamma\dot x+\omega_0^2x=\frac {F_0} m\cos(\omega_tt)=\frac {F_0}m$$
hvor
## $$\gamma =\frac b m\quad\text{og}\quad \omega_0^2=\frac k m$$
Løsningen til differentialligningen er 
## $$x(t)=A_0\cos(\omega_tt-\alpha)+Ae^{-\gamma t/2}\cos(\omega_dt+\phi)$$
hvor
## $$A_0=\frac{F_0/m}{\sqrt{(\omega_0^2-\omega_t^2)^2+\gamma^2\omega_t^2}}\quad\text{og}\quad\tan\alpha=\frac{\gamma\omega_t}{\omega_0^2-\omega_t^2}$$
Eftersom at $\omega_t=0$ må $\alpha=0$.
## $$A_0= \frac{F_0/m}{\sqrt{(\omega_0^2-0)^2+0}}=\frac {F_0/m}{\omega_0^2}=\frac {F_0/m}{k/m}=\frac {F_0}{k}$$
Så har vi altså
## $$x(t)=\frac {F_0}k+Ae^{-\gamma t/2}\cos(\omega_dt+\phi)$$ $$v(t)=\dot x(t)=Ae^{-\gamma t/2}(\omega_d\sin(\omega_dt+\phi)-\frac \gamma 2\cos(\omega_dt+\phi))$$ $$a(t)=\dot v(t)=Ae^{-\gamma t /2}(\frac {\gamma^2}4\cos(\omega_dt+\phi)-\omega_d^2\cos(\omega_dt+\phi))+ \gamma\omega_d\sin(\omega_dt+\phi))$$
## Energi
Vi kan nu opstille energi
## $$E_{kin}=\frac 1 2mv^2\quad\text{og}\quad E_{pot}=\frac 1 2kx^2$$

## Lagrange
og bruge det til at modeller med Euler-Lagrange
## $$\mathscr{L} = E_{kin}-E_{pot}$$
## $$\frac d {dt}*\frac {\delta\mathscr L} {\delta \dot x} -\frac {\delta\mathscr L} {\delta x} = Q$$
hvor $Q$ er de ikke-konservative krafter $Q=-b\dot x+F_0$.
## $$\mathscr L=\frac 1 2m\dot x^2-\frac 1 2kx^2$$
## $$\frac {\delta\mathscr L}{\delta x}=-kx$$
## $$\frac {\delta\mathscr L}{\delta\dot x}=m\dot x$$
dermed
## $$-b\dot x+F_0=\frac d{dt}m\dot x-(-kx)=-b\dot x+F_0=m\ddot x+kx$$$$\Leftrightarrow m\ddot x=-kx-b\dot x+F_0$$
# Fjeder-Dæmper-Dobbelt masse system
![[Pasted image 20260109115650.png]]

# Lagrange
Vi kan opstille kinetisk energi
## $$E_{kin}=E_{kin,1}+E_{kin,2}=\frac 1 2m_1\dot x_1^2+\frac 1 2m_2\dot x_2^2$$
og potentiel energi
## $$E_{pot}=E_{pot,1}+E_{pot,2}=\frac 1 2kx_1^2+\frac 1 2kx_2^2$$
og bruge det til Euler-Lagrange modellering
## $$\mathscr{L} = E_{kin}-E_{pot}$$
## $$\frac d {dt}*\frac {\delta\mathscr L} {\delta \dot x} -\frac {\delta\mathscr L} {\delta x} = Q$$
hvor $Q$ er de ikke-konservative krafter $Q=F$.
## $$\mathscr L=\left(\frac 1 2m_1\dot x_1^2+\frac 1 2m_2\dot x_2^2\right)-\left(\frac 1 2kx_1^2+\frac 1 2kx_2^2\right)$$
## $$\frac {\delta\mathscr L}{\delta x}=-kx_1-kx_2$$
## $$\frac {\delta\mathscr L}{\delta\dot x}=m_1\dot x_1+m_2\dot x_2$$
Vi kan nu vælge at dele det op i to systemer
## $$\frac d{dt}\begin{bmatrix}m_1\dot x_1\\m_2\dot x_2\end{bmatrix}-\begin{bmatrix}-kx_1\\-kx_2\end{bmatrix}=\begin{bmatrix}0\\F\end{bmatrix}$$$$\begin{bmatrix}m_1\ddot x_1\\m_2\ddot x_2\end{bmatrix}-\begin{bmatrix}-kx_1\\-kx_2\end{bmatrix}=\begin{bmatrix}0\\F\end{bmatrix}$$ $$\begin{bmatrix}m_1\ddot x_1\\m_2\ddot x_2\end{bmatrix}=\begin{bmatrix}0\\F\end{bmatrix}+\begin{bmatrix}-kx_1\\-kx_2\end{bmatrix}=\begin{bmatrix}-kx_1\\F-kx_2\end{bmatrix}$$
Således bliver det for det samlede system
## $$m_1\ddot x_1+m_2\ddot x_2=-kx_1-kx_2+F$$