Ud fra [[Laplacetransformation#Overføringsfunktion|overføringsfunktionen]] 
## $$\frac {Y(s)} {U(s)} = H(s)$$
kan det Laplacetransformerede output
## $$Y(s)=H(s)U(S)$$
bestemmes.
Det er derfor relevant at lave invers Laplacetransformation for at finde
## $$y(t)=\mathcal{L}^{-1}\{Y(s)\}$$
Dette er defineret som
## $$f(t)=\frac 1 {2\pi j} \int^{\sigma_c+j\infty}_{\sigma_c-j\infty}F(s)e^{st} ds$$
_Dette bruges dog ikke normalt. I stedet bruges tabellen her._
![[Pasted image 20260108205415.png]]

# Partialbrøkopspaltning
Vi betrager
## $$H(s) = \frac {b_1s^m+b_2s^{m-1}+...+b_{m+1}}{s^n+a_1s^{n-1}+...+}$$