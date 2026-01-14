# Opsummering
> [!help] Harmonisk svingning
> En bevægelsesligning på formen
> $$\frac {d^2z}{dt^2}=\ddot z(t)=-\Phi z(t)$$
> hvor $\Phi\in\mathbb{R}_+$ har en løsning der er en _simpel harmonisk bevægelse_
> $$z(t)=A\cos(\omega_0t+\phi)$$
> med vinkelfrekvens og svingningstid
> $$\omega_0=\sqrt{\Phi}\quad\text{og}\quad T=2\pi\sqrt{\frac 1 \Phi}$$

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
-\int_{x_i}^{x_f}F(x)dx## $$F(t)=ma(t)\quad\text{[N]}$$
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
> [!example]- Eksempel: Pendul
> ![[Pasted image 20260111121420.png]]
> Antag at vinklen $\theta$ er meget lille, så $\sin \theta\approx\theta$.
> Bevægelsen langs tangent retningen fås via [[Subjects/3. Semester/Modellering af elektromekaniske systemer/Topics/Newtons Love#Newtons 2. lov|Newtons 2. Lov]] til
> $$ma_T=ml\frac {d^2\theta}{dt^2}\approx-mg\theta$$
> Denne differentialligning kan skrives
> $$\frac {d^2\theta}{dt^2}\approx-\frac g l\theta$$
> Som har samme form som [[Simpel harmonisk svingning#Opsummering|standard formen]] for en simpel harmonisk svingning.
> Så bliver
> $$\omega_0=\sqrt{\frac g l}\quad\text{og}\quad T=2\pi\sqrt{\frac l g}$$

> [!example]- Eksempel: Pendul stang
> ![[Pasted image 20260111121905.png]]
> Antag at vinklen $\theta$ er meget lille, så $\sin\theta\approx\theta$.
> Bevægelsen om punktet $O$ via [[Impulsmoment og kraftmoment#Impulsmomentsætningen|impulsmomentsætningen]] bliver til
> $$I_O\frac {d^2\theta}{dt^2}\approx-mgl\theta$$
> Denne differentialligning kan skrives
> $$\frac {d^2\theta}{dt^2}\approx-\frac{mgl}{I_O}\theta$$
> Som har samme form som [[Simpel harmonisk svingning#Opsummering|standard formen]] for en simpel harmonisk svingning.
> Så bliver
> $$\omega_0=\sqrt{\frac{mgl}{I_O}}\quad\text{og}\quad T=2\pi\sqrt{\frac{I_O}{mgl}}$$

