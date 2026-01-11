# Opsummering
> [!help] Definition
> Hvis en [[Dæmpet simpel harmonisk svingning|dæmpet harmonisk svingning]] eller en [[Simpel harmonisk svingning|simpel harmonisk svingning]] påtrykkes en _periodisk_ kraft, skrives dynamikken for systemet således
> $$m\ddot x=-kx-b\dot x+F$$
> hvor $F=F_0\cos(\omega_tt)$ er en ekstern kraft med vinkelfrekvens $\omega_t$.

> [!help] Omskrivning
> Vi kan ligesom for [[Dæmpet simpel harmonisk svingning|en dæmpet harmonisk svingning]] skrive differentialligningen som
> $$\ddot x+\gamma\dot x+\omega_0^2x=\frac {F_0}m\cos(\omega_tt)$$
> hvor
> $$\gamma=\frac b m\quad\text{og}\quad\omega_0^2=\frac k m$$

> [!help]

---
Hvis en [[Dæmpet simpel harmonisk svingning|dæmpet harmonisk svingning]] eller en [[Simpel harmonisk svingning|simpel harmonisk svingning]] påtrykkes en _periodisk_ kraft, skrives dynamikken for systemet således
## $$m\ddot x=-kx-b\dot x+F$$
hvor $F=F_0\cos(\omega_tt)$ er en ekstern kraft med vinkelfrekvens $\omega_t$.

Vi kan ligesom for [[Dæmpet simpel harmonisk svingning|en dæmpet harmonisk svingning]] skrive differentialligningen som
## $$\ddot x+\gamma\dot x+\omega_0^2x=\frac {F_0}m\cos(\omega_tt)$$
hvor
## $$\gamma=\frac b m\quad\text{og}\quad\omega_0^2=\frac k m$$
# Løsning
Løsningen til differentialligningen
## $$\ddot x+\gamma\dot x+\omega_0^2x=\frac {F_0}m\cos(\omega_tt)$$
er
## $$x(t)=A_0\cos(\omega_tt-\alpha)+Ae^{-\gamma t/2}\cos(\omega_dt+\phi)$$
hvor
## $$A_0=\frac{F_0/m}{\sqrt{(\omega_0^2-\omega_t^2)^2+\gamma^2\omega_t^2}}\quad\text{og}\quad\tan\alpha=\frac{\gamma\omega_t}{\omega_0^2-\omega_t^2}$$
 
Løsningens to led er 
## $$A_0\cos(\omega_tt-\alpha)\rightarrow \text{Stationær bevægelse}$$
som primært kommer fra $F$, og
## $$Ae^{-\gamma t/2}\cos(\omega_dt+\phi)\rightarrow \text{Transient bevægelse}$$
som kommer fra den [[Dæmpet simpel harmonisk svingning|dæmpede harmonisk svingning]].
Læg mærke til, at den _Transiente_ del, har samme form som en [[Dæmpet simpel harmonisk svingning#Dæmpet svingning|dæmpet svingning]].

I starten($t=0$ s), vil den _Transiente_ bevægelse have en stor amplitude, men denne vil mindskes eksponentielt (hvis $\gamma>0$).
Når tiden $t$ er stor, er
## $$x(t)\approx A_0\cos(\omega_tt-\alpha)$$

Amplituden og fasen for den [[Tvunget harmonisk bevægelse#$$x(t)A_0 cos( omega_tt- alpha)+Ae {- gamma t/2} cos( omega_dt+ phi)$$|førnævnte]] løsning afhænger af inputtets vinkelfrekvens $\omega_t$.
![[Pasted image 20260111130820.png]]
Vi kan se at grafen for amplitude minder om et [[External/External/Kasper's Notes/Uni/Notes/Multivariable Calculus/Noter/BODE plot|BODE plot]].

Det ses at $A_0$ er maksimal i **resonansfrekvensen**
## $$\omega_{t,r}=\sqrt{\omega_0^2-\frac{\gamma^2}2}\quad\text{[rad/s]}$$
