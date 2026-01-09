
# Opsummering
> [!help] Form
> $$H(S)=\mathcal{L}\{h(t)\}=\int^\infty_{0^-}h(t)e^{-st} dt$$

> [!help] Tabel
> ![[Pasted image 20260108205415.png]]

>[!help] Egenskaber
>Differentieret $f(t)$
>$$\mathcal{L}\left(\frac {df} {dt}\right)=sF(s)-f(0)$$
>Integreret $f(t)$
>$$\mathcal{L}\left(\int^t_0f(\tau) d\tau\right)=\frac {F(s)} s$$

> [!help] Overføringsfunktion
> En overføringsfunktion er forholdet mellem det _Laplacetransformerede input_ $u$ og det _Laplacetransformerede output_ $y$.
> $$H(s)=\frac{Y(s)}{U(s)}$$
> hvor $Y(s)$ og $U(s)$ er polynomier ($U$ af højere orden end $Y$) i variablen $s$.
> Rødderne af $Y$ er _nulpunkterne_ af $H(s)$
> Rødderne af $U$ er _polerne_ af $H(s)$

> [!help] Frekvensrespons
> Gælder for _sinusdialt_ input
> $$y(t)=H(s)e^{st}$$
> omskrives
> $$y(t)=A M(\omega)\cos(\omega t+\phi(\omega))$$
> hvor
> $$M(\omega)=|H(j\omega)| \quad \text{og} \quad \phi(\omega)=\angle H(j\omega)$$



---
Er en generalisering af [[Fouriertransformation]] og er defineret som
## $$H(S)=\mathcal{L}\{h(t)\}=\int^\infty_{0^-}h(t)e^{-st} dt$$
hvor $s\in\mathbb{C}$ (kompleks)

# Egenskaber
## Differentieret $f(t)$
Lad $f(t)$ og $df(t)/dt$ være kontinuerlige funktioner. Så gælder
## $$\mathcal{L}\left(\frac {df} {dt}\right)=sF(s)-f(0)$$
Hvor $F(s)=\mathcal{L}(f)$.

## Integreret $f(t)$
Lad $f(t)$ være en kontinuerlig funktion og $F(s)=\mathcal{L}(f)$. Så gælder
## $$\mathcal{L}\left(\int^t_0f(\tau) d\tau\right)=\frac {F(s)} s$$

## Tabel
![[Pasted image 20260108205415.png]]

# Graf ved polers placering
![[Pasted image 20260108205536.png]]

# Overføringsfunktion

## $$H(s)=\int^\infty_{-\infty}h(\tau)e^{-s\tau}d\tau$$
hvor $h(t)$ er impulsresponset. $H(s)$ er **overføringsfunktionen**.

> En overføringsfunktion er forholdet mellem det _Laplacetransformerede input_ $u$ og det _Laplacetransformerede output_ $y$.

## $$H(s)=\frac {Y(s)}{U(s)}$$
Hvor $y$ er output, og $u$ er input.
Det antages at systemets begyndelsesbetingelser er nul.

> [!example]-
> ![[Pasted image 20260108203941.png]]

## Poler og nulpunkter
![[Pasted image 20260108204015.png]]

## Frekvensrespons
Et systems **frekvensrespons** er responset, når et _sinusdialt_ input påtrykkes et system.

Vi har tidligere (se ovenstående eksempel) udtrykt outputtet af et system med input $e^{st}$ ved brug af overføringsfunktionen $H(s)$

## $$y(t)=H(s)e^{st}$$

Eftersom

## $$A\cos(\omega t) = \frac A 2(e^{j\omega t}+e^{-j\omega t})$$
Kan det i stedet skrives
## $$y(t)=\frac A 2(H(j\omega)e^{j\omega t}+H(-j \omega)e^{-j\omega t})$$

På _polær form_ er $H(j \omega) = M(\omega)e^{j\phi(\omega)}$.
Så ovenstående forkortes til
## $$y(t)=A M(\omega)\cos(\omega t+\phi(\omega))$$
hvor
## $$M(\omega)=|H(j\omega)| \quad \text{og} \quad \phi(\omega)=\angle H(j\omega)$$

> [!example]-
> ![[Pasted image 20260108204849.png]]
> ![[Pasted image 20260108204908.png]]
> ![[Pasted image 20260108204922.png]]

---
#math #physics