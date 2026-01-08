
Er en generalisering af [[Fouriertransformation]] og er defineret som
## $$H(S)=\mathcal{L}\{h(t)\}=\int^\infty_{0^-}h(t)e^{-st} dt$$
hvor $s\in\mathbb{C}$ (kompleks)

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

På _polær form_ er $H(j)


---
#math #physics