
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

# Case 1: Normalfordeling, $\mu$
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

Konfidensintervallet er så
$$CI:\quad \left[\bar X\pm z_{\alpha/2}\cdot \frac \sigma {\sqrt n}\right]$$

Hvis vi vil have et breddere interval:
$$2z_{\alpha/2}\frac \sigma {\sqrt{n}}$$

Hvis vi vil have et _smallere_ interval
$$\left\{ \begin{array}{} n {\text{ larger} \\ (1-\alpha} \text{smaller}\end{array}\right.$$

## 1-sidet CI for $\mu$

Vi har en PDF for $Z$. **Billedet er genbrugt fra ovenover, men det skulle faktisk være $\alpha$ i stedet for $\alpha/2$. Bare lav den erstatning i hovedet.**
![[Pasted image 20261009083541.png|390]]

Så kan vi finde _lower bound_ CI for $\mu$. Forvirrende nok kalder nogen det også _upper CI_.
$$\left[\bar X + z_{\alpha} \frac \sigma {\sqrt n} , \infty \right[$$

Vi kan finde _upper bound_ CI for $\mu$. Lige så forvirrende, er der nogen der kalder det _lower CI_.
$$\left]-\infty, \bar X z_{\alpha} \frac \sigma {\sqrt n} \right]$$


I MATLAB kan man bruge `ztest` til at gøre det hele automatisk.

# Case 2: Normalfordeling, $\sigma$ ukendt
Vi har normalfordeling $N(\mu,\sigma^2)$
- $\sigma^2$ er ukendt
- CI for $\mu$

Test statistic
$$Z:=\frac {\bar X-\mu}{\sigma/\sqrt n}\sim N(0,1)$$
Vi kender dog ikke $\sigma$, så vi må estimere.
$$\hat {\sigma^2}=S^2=\frac 1{n-1}\sum_{i=1}^n(x_i-\bar x)\sim?$$
Vi introducerer en ny fordeling, 
## _Chi i anden_, $\mathcal X^2$
$$\mathcal X^2(n):=z_1,...,z_n,\sim N(0,1)\Rightarrow \sum_{i=1}^n z_i^2\sim\mathcal X^2(n)$$
hvor $n$ er frihedsgrader. $z_1,...,z_n$ er normalfordelt.
Dette har PDF'en
![[Pasted image 20261009090418.png|338]]
(Linjen krydser aldrig 0, jeg er bare dårlig til at tegne)

Desuden introducerer vi endnu en ny fordeling,
## _Student t_, $t$
$$t(n):=\left\{\begin{array}{}Z\sim N(0,1)\\ V\sim \mathcal X^2(n)\end{array}\right.\Rightarrow T=\frac Z{\sqrt{\frac V n}}\sim t(n)$$

hvor $n$ er frihedsgrader.
![[Pasted image 20261009091053.png]]

Vi ved at nedenstående udtryk er en normalfordeling
$$\frac {\bar X-\mu} {\sigma/\sqrt n}\sim N(0,1)$$
Vi kan skrive
$$\frac {S^2}{\sigma^2}\sim \frac {\mathcal X^2(n-1)}{n-1}$$
Og bruge de to udtryk til at få
$$\frac {\frac {\bar X-\mu}{\sigma/\sqrt n}}{\sqrt{\frac {S^2}{\sigma^2}}}=\frac {\bar X-\mu}{S/\sqrt n}\sim t(n-1)$$

Vi har dermed vores student-t fordeling
![[Pasted image 20261009093152.png|348]]

I MATLAB kan vi finde $t(n-1)_{\alpha/2}$ ved `tinv(1 - alpha/2, n-1)`.

På samme måde er der også en $-t(n-1)_{\alpha/2}$ ved venstre side. Denne kan også findes i matlab som `tinv(alpha/2, n-1)`.

$$P\left(-t(n-1)_{\alpha/2}\leq \frac {\bar X -\mu}{S/\sqrt n}\leq t(n-1)_{\alpha/2}\right)=1-\alpha$$

Vi kan så finde CI for $\mu$
$$CI: \quad \left[\bar X \pm t(n-1)_{\alpha/2}\cdot \frac S {\sqrt n}\right]$$

Vi kan finde upper og lower bound på samme måde som [[#1-sidet CI for $ mu$|1-sidet CI for mu]] med den forskel, at vi har $t(n-1)$ i stedet for $z_\alpha$.

# Case 3: Normalfordeling, $\sigma^2$

Vi har $N(\mu,\sigma^2)$
- Finder CI for $\sigma^2$

$$\hat {\sigma^2}=S^2=\frac 1 {n-1}\sum_{i=1}^n (x_i-\bar X)^2 \sim \frac {\sigma^2}{n-1}\mathcal X^2(n-1)$$

$$(n-1)\frac {S^2}{\sigma^2}\sim \mathcal X^2(n-1)$$
![[Pasted image 20261009094623.png]]

Vi kan finde $\mathcal X^2(n-1)_{\alpha/2}$ i MATLAB ved at bruge `chi2inv(1 - alpha/2, n-1)`

Den venstre $\alpha/2$ har selvfølgelig også en $\mathcal X^2$, med den forskel at subskriptet er ændret: $\mathcal X^2(n-1)_{1-\alpha/2}$.
- Denne kan også findes i MATLAB: `chi2inv(alpha/2, n-1)`


$$P\left(\mathcal X^2(n-1)_{1-\alpha/2}\leq (n-1)\frac {S^2}{\sigma^2}\leq \mathcal X^2(n-1)_{\alpha/2}\right)=1-\alpha$$
Vi kan omskrive for at få konfidensintervallet for $\sigma^2$
$$CI: \quad \left[\frac {(n-1 S^2)}{\mathcal X^2(n-1)_{\alpha/2}}, \frac {(n-1 S^2)}{\mathcal X^2(n-1)_{1-\alpha/2}}\right]$$

# Case 4: Prediction Interval for next observation
Stadigvæk normalfordeling
$N(\mu,\sigma^2)$
- Vi har $n$ observationer
- Vi finder prediktion af næste observation $x_{n+1}$.

$$x_{n+1}\sim N(\mu, \sigma^2)$$
$$\hat x_{n+1}=\bar X = N\left(\mu, \frac {\sigma^2} n\right)$$

Vi kan sige at
$$\hat x_{n+1}-x_{n+1}\sim N\left(0, \sigma^2\left(1+\frac 1 n\right)\right)$$

$$\frac {\hat x_{n+1}-x_{n+1}}{\sqrt{\sigma^2\left(1+\frac 1 n\right)}}\sim N(0,1)$$
Som er standard normalfordelt.

$$\frac {\hat x_{n+1}-x_{n+1}}{\sqrt{S^2\left(1+\frac 1 n\right)}} \sim t(n-1)



---
#lecture 