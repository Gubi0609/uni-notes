En bevægelsesligning på formen
## $$\frac {d^2z}{dt^2}=-\Phi z(t)$$
(se [[Simpel harmonisk svingning]])

Kan [[Laplacetransformation|Laplacetransformeres]] for at få den i frekvens domænet.
## $$s^2Z(s)-sz(0)-\frac {dz}{dt}(0)=-\Phi Z(s)$$
fra [[Simpel harmonisk svingning]] ved vi at $\Phi=\omega_0^2$, så vi kan finde $Sz(s)$
## $$Z(s)=\frac {sz(0)+\frac{dz}{dt}(0)}{s^2+\omega_0^2}$$
[[Laplacetransformation#Poler og nulpunkter|polerne]] for systemet er
## $$s^2+\omega_0^2=0\Leftrightarrow s=\frac {-0\pm\sqrt{0^2-4\cdot1\cdot\omega_0^2}}{2\cdot1}=\pm j\omega_0$$
Ved [[Invers Laplacetransformation]] fås
## $$z(t)=z(0)\cos(\omega_0t)+\frac{\frac{dz}{dt}(0)}{\omega_0}\sin(\omega_0t)$$
> [!example]- Udledning af [[Dæmpet simpel harmonisk svingning#Aperiodisk svingning|overdæmpet]] svingning
> Betragt følgende overføringsfunktion og antag at de to poler er reelle og forskellige $p_1 \neq p_2$
> $$X(s)=\frac{sx(0)+\frac {dx}{dt}(0)+\gamma x(0)}{s^2+\gamma s+\omega_0^2}$$
> ![[Pasted image 20260111140704.png]]
> De røde poler på ovenstående figur er de tilhørende poler.
> 
> Lad
> $$a=\frac \gamma 2+\sqrt{\frac {\gamma^2}4-\omega_0^2},\quad b=\frac \gamma 2 -\sqrt{\frac {\gamma^2}4-\omega_0^2}\quad \text{og}\quad \alpha=\frac {dx}{dt}(0)+\gamma x(0)$$
> Så haves
> $$X(s)=\frac {sx(0)+\alpha}{(s+a)(s+b)}$$
> Ved [[Invers Laplacetransformation]] fås
> $$x(t)=\frac {\alpha-ax(0)}{b-a}e^{-at}+\frac{bx(0)-\alpha}{b-a}e^{-bt}