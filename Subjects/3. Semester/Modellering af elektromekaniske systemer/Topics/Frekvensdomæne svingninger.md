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
## $$z(t)=z(0)\cos(\omega_0t)+\frac{\frac{dz}{dt}(0)}{}$$