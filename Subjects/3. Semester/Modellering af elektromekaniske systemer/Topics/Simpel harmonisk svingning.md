
---
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
## $$\omega_0=\sqrt{\frac k m}\quad\text{[rad/s]}$$
Dette gælder både for [[Bevægelse af stive legemer|translatoriske]] og [[Bevægelse af stive legemer#Inertimoment|roterende]] systemer.

# Energi
Den [[Subjects/3. Semester/Modellering af elektromekaniske systemer/Topics/Mekanisk energi|samlede energi]] for en simpel harmonisk svingning er konstant
![[Pasted image 20260111105405.png]]

Den totale energi for et [[Gængse kræfter#Fjederkraft|masse-fjeder system]] er
## $$E_{mek}=E_{pot}+E_{kin}=\frac 1 2kx^2+\frac 1 2mv^2\quad\text{[J]}$$
Dette kan forkortes
## $$E_{mek}=\frac 1 2 kx^2+\frac 1 2 mv^2$$
Formlerne for position og hastighed bruges fra [[Simpel harmonisk svingning#Egenskaber|egenskaberne]].
## $$=\frac 1 2k(A\cos(\omega_0t+\phi))^2+\frac 1 2m(-\omega_0A\sin(\omega_0t+\phi))^2$$ $$=\frac 1 2A^2(k\cos^2(\omega_0t+\phi)+m\omega_0^2\sin^2(\omega_0t+\phi))$$
Vi bruger $\omega_0^2=k/m$ fra [[Simpel harmonisk svingning#$$ omega_0= sqrt{ frac k m} quad text{[rad/s]}$$|før]].
## $$=\frac 1 2A^2(m\omega_0^2\cos^2(\omega_0t+\phi)+m\omega_0^2\sin(\omega_0t+\phi))$$ $$=\frac 1 2A^2m\omega_0^2(\cos^2+\sin^2)$$ $$E_{mek}=\frac 1 2m\omega_0^2A^2\quad\text{[J]}$$
