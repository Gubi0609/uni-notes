
---
**Date:** 2026-10-09

## Preparation

>[!TODO] HOMEWORK
>- [ ] 

> [!DANGER] EXERCISES
> - [ ] 8.1.3, 8.1.4, 8.1.12, 8.2.1, 8.2.9, 8.2.12, 8.3.3, 8.4.1

---
# Relevant documents
[[Agenda lecture 06.pdf]]
[[Lektion 6 slides.pdf]]
[[Solutions lecture 06 v3.pdf]]

# Topics


# Notes

![[Pasted image 20261009103543.png]]

- a.
Siden det er normalfordelt, på sample mean, være i midten af konfidensintervalerne
$$\mu=\frac {38.02+61.98} 2=50$$
$$\mu = \frac {39.95+60.05} 2=50$$
- b.

Det intercal med 95% sikkerhed må være breddere end det med 90%. Hvis vi derfor finder bredden af hvert interval, kan vi afgøre hvilken er breddest
$$61.98-38.02=23.96$$
$$60.05-39.95=20.1$$
Dermed er intervallet $(38.02,61.98)$ det interval med 95% sikkerhed.


![[Pasted image 20261009103554.png]]

- a.
Vi kan bruge formlen for CI af normalfordeling med kendt $\sigma$.
$$CI:\quad \left[\bar X\pm z_{\alpha/2}\cdot \frac \sigma {\sqrt n}\right]$$
Hvor $z_{\alpha/2}$ findes i matlab ved `norminv(1 - alpha/2)` med `alpha=0.05`
$$z_{\alpha/2}=1.96$$

Vi kan isolere for $n$, siden vi ved at CI skal have en bredde på 40.
Fordi mean er i midten af intervallet, kan vi finde $n$ fra halvdelen af længden af intervallet $40/2=20$.
$$20=z_{\alpha/2}\frac \sigma {\sqrt n}\Rightarrow n=\left(z_{\alpha/2} \frac \sigma {20}\right)^2=\left(1.96\frac {20} {20}\right)^2=1.96^2=3.84\approx4$$

- b.
Samme fremgangsmetode som før. Vi bruger MATLAB igen med `alpha = 0.01`
$$z_{\alpha/2}=2.5758$$

$$n=\left(2.5758\frac {20} {20}\right)^2=2.5758^2=6.635\approx7$$



![[Pasted image 20261009103605.png]]

- a.
$\sigma=0.66$
$2.69, 5.76, 2.67, 1.62, 4.12$

Vi bruger
$$CI:\quad \left[\bar X\pm z_{\alpha/2}\cdot \frac \sigma {\sqrt n}\right]$$

Og bruger MATLAB til at finde $z_{\alpha/2}=1.96$ for $\alpha=0.05$.
$n$ må være 5m, siden vi har 5 datapunkter.
$\bar X$ er gennemsnittet af datasættet
$$\bar X=3.372$$

Så finder vi konfidensintervallet
$$CI:\quad \left[3.372\pm 1.96\cdot \frac {0.66} {\sqrt 5}\right]=\left[2.793, 3.951\right]$$

- b.
Vi kan ud fra konfidensintervallet isolere $n$
$$n=\left(z_{\alpha/2} \frac {\sigma}{\text{width}/2}\right)^2=\left(1.96\cdot \frac {0.66}{0.55/2}\right)^2=22.128\approx 23$$

![[Pasted image 20261009103617.png]]

- a.
$x$
$n = 10$
$\mu=\sum_{i=1}^n x_i/n=25.1848$ 
$SE \mu=1.605$
$\sigma=1.605$
$\sigma^2 =\sigma^2=1.605^2=2.576$
$\sum_{i=1}^n x_i = 251.848$

- b.
Vi bruger
$$CI:\quad \left[\bar X\pm z_{\alpha/2}\cdot \frac \sigma {\sqrt n}\right]$$

hvor $z_{\alpha/2}=1.96$ fundet i MATLAB som i forrige opgaver.
$\bar X=\mu=25.1848$.

$$CI:\quad \left[25.1848\pm 1.96\cdot \frac {1.605}{\sqrt{10}}\right]=\left[24.19,26.18\right]$$



![[Pasted image 20261009103630.png]]



![[Pasted image 20261009103645.png]]

![[Pasted image 20261009103659.png]]

![[Pasted image 20261009103711.png]]

---
#lecture 