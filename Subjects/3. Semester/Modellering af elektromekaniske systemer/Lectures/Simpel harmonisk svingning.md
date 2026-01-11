Vi betragter systemer med _periodiske bevægelser_, hvilket vil sige at bevægelsen gentages hver $T$ sekund
## $$T=\frac 1 f \quad\text{[s]}$$
hvor $T$ er periodetiden $\text{[s]}$ og $f$ er frekvensen $\text{[Hz]}$.

Vi kan også beskrive vinkelfrekvensen $\omega_0$
## $$\omega_0=\frac {2\pi}{T}=2\pi  f\quad\text{[rad/s]}$$
# Egenskaber
En partikel siges at have en **simpel harmonisk bevægelse** hvis dens position er givet som
## $$x(t)=A\cos(\omega_0t+\phi)$$
hvor $A$ er amplituden, $\omega_0$ er vinkelfrekvensen og $\phi$ er fasekonstanten.

Hastigheden kan beskrives
## $$v(t)=\dot x(t)=-\omega_0A\sin(\omega_0t+\phi)$$
og accelerationen
## $$a(t)=\dot v(t)=\ddot x(t)=-\omega_0^2A\cos(\omega_0t+\phi)=-\omega_0^2x(t)$$

For en vilkårlig harmonisk svingning, vil disse ligninger se ud som følgende
![[Pasted image 20260111104226.png]]

# Kraft
Fra [[Subjects/3. Semester/Modellering af elektromekaniske systemer/Topics/Newtons Love#Newtons 2. lov|Newtons 2. Lov]] har vi
## $$F(t)=ma(t)\quad\text{[N]}$$
Hvis $a(t)=-\omega_0^2x(t)$ fra [[Simpel harmonisk svingning#Egenskaber|før]] bruges haves
## $$F(t)=-m\omega_0^2x(t)\quad\text{[N]}$$
Som er på samme form som [[Gængse kræfter#Fjederkraft|Hooks lov]]
## $$F(t)=-kx(t)\quad\text{[N]}$$
hvor $k=m\omega_0^2$.

Vi kan derfor også isolere vinkelfrekvensen
## $$\omega_0=\sqrt