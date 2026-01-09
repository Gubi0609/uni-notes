# Opsummering
> [!help] Invers Laplacetransformation
> $$y(t)=\mathcal{L}^{-1}\{Y(s)\}$$
> Defineres som 
> $$f(t)=\frac 1 {2\pi j} \int^{\sigma_c+j\infty}_{\sigma_c-j\infty}F(s)e^{st} ds$$

> [!help] Tabel
> ![[Pasted image 20260108205415.png]]

> [!help] Partialbrøkopspaltning
> $$H(s) = \frac {b_1s^m+b_2s^{m-1}+...+b_{m+1}}{s^n+a_1s^{n-1}+...+a_n}$$
> Kan faktoriseres
> $$H(s)=K\frac {\prod^m_{i=1}(s-z_i)}{\prod^n_{i=1}(s-p_i)}$$
> hvor $z$ er nulpunkt og $p$ er en pol.
> 
> Antag at alle poler er forskellige, så skriver vi
> $$H(s)=\frac {C_1} {s-p_1}+\frac {C_2} {s-p_2}+...\frac {C_n} {s-p_1n}$$
> hvor
> $$C_i=(s-p_i)H(s)|_{s=p_i}$$

> [!help] Invers Laplacetransformation af partialbrøkopspaltet overføringsfunktion
> $$h(t)=\sum^n_{i=1}C_i e^{p_it}$$

---
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
Vi betragter
## $$H(s) = \frac {b_1s^m+b_2s^{m-1}+...+b_{m+1}}{s^n+a_1s^{n-1}+...+a_n}$$
Dette kan faktoriseres
## $$H(s)=K\frac {\prod^m_{i=1}(s-z_i)}{\prod^n_{i=1}(s-p_i)}$$
hvor $z$ er nulpunkt og $p$ er en pol.

Vi antager at alle poler er forskellige, så skrives overføringsfunktionen
![[Pasted image 20260108211310.png]]

## Find $C_i$
![[Pasted image 20260108211336.png]]
![[Pasted image 20260108211349.png]]

> [!example]-
> ![[Pasted image 20260108211433.png]]
> ![[Pasted image 20260108211446.png]]