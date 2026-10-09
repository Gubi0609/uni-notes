
---
**Date:** 2026-10-09

## Preparation

>[!TODO] HOMEWORK
>- [ ] 

> [!DANGER] EXERCISES
> - [ ] 

---
# Relevant documents
[[Agenda lecture 06.pdf]]
[[Lektion 6 slides.pdf]]
[[Solutions lecture 06 v3.pdf]]

# Topics


# Notes


# Confidence Intervals (CI)

Vi har en stokastisk variabel $X$ og en _antaget fordeling_
Vi har desuden en eller flere ukendte parametre $\theta$.
Der laves et estimat $\hat\theta=h(x_1,...x_n)$ hvor $h$ er en funktion af vores observationer $x_1,...,x_n$.

$$\text{CI:}=[A,B]\text{ omkring }\hat\theta$$

Så $\theta$ med konfidens $100\cdot (1-\alpha)\%$ ligger i CI.
- $\alpha$: SIgnifikantsniveau
- $1-\alpha$: Konfidensniveau

Typiske værdier for $\alpha$ er $1\%$, $5\%$, og $10\%$, hvor $5\%$ er mest typisk.
- Det fører til et konfidensniveau på hhv. $99\%$, $95\%$, og $90\%$.

Vi vil gerne have et så smalt som muligt konfidensinterval, men vi vil også gerne have en høj konfidens
![[Pasted image 20261009082635.png|450]]

Konfidensinterval og konfidensniveau arbejder altså lidt i mod hinanden...
Vi kan opnå et smalt konfidensinterval (CI) ved
- At have et lavt konfidensniveau
- Eller have en _større stikprøve_.

# Case
Vi har normalfordeling $N(\mu, \sigma^2)$
- $\sigma^2$ er _kendt_
- CI for $\mu$ er ukendt

Model:
- $x_1,...x_n$ er uafhængige hvor $x_i\sim (\mu,\sigma^2)$ 

Vi estimerer $\mu$. Estimatet er $\hat\mu=\bar X=\frac 1 n \sum^n_{i=1}x_i\sim N(\mu,\frac {\sigma^2}n)$

$$Z=\frac {\bar X-\mu}{\sigma /\sqrt n} \sim N(0, 1)$$
Det oventående er en _test statistic_.

![[Pasted image 20261009083541.png|390]]

For at finde $Z_{\alpha/2}$ i MATLAB, skal vi bruge `norminv(1 - alpha/2)`.

$$P(-z_{\alpha/2}\leq Z\leq z_{\alpha/2})=1-\alpha$$
$$P(-z_{\alpha/2}\leq \frac {\bar X -\mu}{\sigma /sqrt n}\leq z_{\alpha/2}) = 1-\alpha$$

Vi ville gerne have et konfidens interval for $\mu$, så vi omskriver
$$P(\bar X-z_{\alpha/2}\cdot \frac \sigma {\sqrt n} \leq \mu \leq \bar X+z_{\alpha/2}\cdot \frac \sigma {\sqrt n})=1-\alpha$$

---
#lecture 