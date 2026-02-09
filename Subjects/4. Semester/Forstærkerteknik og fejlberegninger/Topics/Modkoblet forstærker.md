En modkoblet forstærker har et kredsløb som dette
![[Pasted image 20260209082430.png]]

Hvor det ovenstående er en forstærker med _negativ feedback_ (da feedback går til den negative indgangsport).

Forstærkningen for en modkoblet op amp er
## $$A_{CL}=\frac \alpha \beta$$
De generelle formler for $\alpha$ og $\beta$ er
## $$\alpha=\frac {V_{id}}{V_{in}}\quad\beta=-\frac {V_{id}}{V_o}$$

# Inverterende forstærker
![[Pasted image 20260209082514.png]]

Har følgende $\alpha$ og $\beta$ værdier
## $$\alpha = -\frac {R_2} {R_1 + R_2}\quad \beta = \frac {R_1}{R_2 + R_1}$$
> [!example]- $\alpha$ og $\beta$ for en inverterende forstærker
> ![[Pasted image 20260209082739.png]]
> Med de ovenstående formler og værdierne $R_1 = 10k\Omega$, og $R_2 = 100k\Omega$ får vi følgende
> $$\alpha = -\frac {100k\Omega}{110k\Omega} = \frac {10}{11}\quad \beta = \frac {10k\Omega}{110k\Omega}=\frac {1}{11}$$

# Ikke-inverterende forstærker
![[Pasted image 20260209082631.png]]

Har følgende $\alpha$ og $\beta$ værdier
## $$\alpha = 1 \quad \beta = \frac {R_1}{R_1+R_2}$$
