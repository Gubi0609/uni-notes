
---
**Date:** 2026-11-06

## Preparation

>[!TODO] HOMEWORK
>- [ ] 

> [!DANGER] EXERCISES
> - [ ] 

---
# Relevant documents
[[Agenda lecture 08.pdf]]
[[Lektion 8 slides.pdf]]
[[Solutions lecture 08 v2.pdf]]

# Topics


# Notes

# Hypotese test (2 populationer)

# Recept
- Model + model check
- $H_0$, $H_1$
- Estimatere de størrelser der indgår i hypoteserne
- Definer test-statistic og fordeling
- Data + $H_0$ $\rightarrow$ TS-værdi
- _Enten_ vælg $\alpha$ og find A og C områder
- _Eller_ beregn p-værdi

# Case 1: Non-paired test (forskel i middelværdier) med _kendt_ varians
Vi har normalfordelt data:
- $X_{1i}\sim N(\mu_i, \sigma_1^2)$, $i=1,...,n_1$
- $X_{2i} \sim N(\mu_2,\sigma_2^2)$, $i=1,...,n_2$

Vi tjekker om modellen er sandsynlig ved model-check

> Ved at finde forskellen i middelværdierne kan vi tjekke om en ny model er bedrte end den gamle (e.g. hvis data repræsenterer tid, kan vi tjekke hvilken der er hurtigst).
## Hypoteser
$$H_0:\quad \mu_1-\mu_2=\Delta_0$$
hvor $\Delta_0$ er den postulerede størrelse. _$\Delta_0$ er ofte ligmed 0_.
$$H_1:\quad \mu_1-\mu_2\neq \Delta_0$$
Vi kan se ud fra $H_1$ at dette er en _to-sidet test_, da vi bruger $\neq$.

## Estimatorer
Vi estimerer $\mu_1$
$$\hat\mu_1=\bar X_1 = \frac 1 n \sum_{i=1}^{n_1} x_{1i}\sim N(\mu_1, \sigma_1^2)$$
og $\mu_2$
$$\hat\mu_2=\bar X_2 = \frac 1 n \sum_{i=1}^{n_2} x_{2i}\sim N(\mu_2, \sigma_2^2)$$

Vi kan så også finde forskellen i de to normalfordelinger
$$(\bar x_1-\bar x_2)\sim N(\mu_1-\mu_2, \frac {\sigma_1^2} {n_1} + \frac {\sigma_2^2} {n_2})$$
## Test statistic
Vi kan så definere test-statistic
$$Z_0:= \frac {(\bar X_1 - \bar X_2)-(\mu_1-\mu_2)}{\sqrt{\frac {\sigma_1^2}{n_1}+\frac {\sigma_2^2}{n_2}}}=^{H_0}\frac {(\bar X_1 - \bar X_2)-\Delta_0}{\sqrt{\frac {\sigma_1^2}{n_1}+\frac {\sigma_2^2}{n_2}}}\sim N(0,1)$$

## Indsæt data og $H_0$
Vi indsættet estimatorer og $H_0$: $Z_0=z_0$

![[Pasted image 20261106083340.png]]

Vi forkaster $H_0$ for $|z_0|>z_{\alpha/2}$.

Og et [[Confidence Intervals (CI)]] kan opsættes for $\mu_1 - \mu_2$.
$$P\left(-z_{\alpha/2} < \frac {(\bar X_1 - \bar X_2)-\Delta_0}{\sqrt{\frac {\sigma_1^2}{n_1}+\frac {\sigma_2^2}{n_2}}} < z_{\alpha_2}\right) = 1-\alpha \Rightarrow$$
$$CI:\quad \left[(\bar X_1 - \bar X_2)\pm z_{\alpha/2}\sqrt{\frac {\sigma_1^2}{n_1} + \frac {\sigma_2^2}{n_2}}\right]$$
_Hvis $H_0$ forkastes er $\Delta_0$ ikke indeholdt i CI._


Eller for $p$-værdi
![[Pasted image 20261106083553.png]]

$$p=2P(Z>|z_0|)=2(1-P(Z<|z_0|))$$
Hvor $P(Z<|z_0|)$ kan findes med `normcdf(|z_0|)`.

# Case 2: Hypoteste test (forskel i middelværdi) med _ukendt men ens_ varians
Vi har normalfordelt data:
- $X_{1i}\sim N(\mu_i, \sigma_1^2)$, $i=1,...,n_1$
- $X_{2i} \sim N(\mu_2,\sigma_2^2)$, $i=1,...,n_2$

hvor $\sigma_1^2=\sigma_2^2=\sigma^2$

Vi tjekker om modellen er sandsynlig ved model-check.

## Test statistic
Vi genbruger $Z_0$ fra forrige case:
$$Z_0:= \frac {(\bar X_1 - \bar X_2)-\Delta_0}{\sigma\sqrt{\frac {1}{n_1}+\frac {1}{n_2}}}\sim N(0,1)$$
Vi kan estimere $\sigma^2$:
$$S_1^2=\frac 1 {n_1-1} \sum_{i=1} ^{n_1} (X_{1i}-\bar X_1)^2\sim \frac {\sigma^2}{n_1-1}\mathcal X^2(n_1-1)$$
Eller ved brug af $X_2$
$$S_2^2=\frac 1 {n_2-1} \sum_{i=1} ^{n_2} (X_{2i}-\bar X_2)^2\sim \frac {\sigma^2}{n_2-1}\mathcal X^2(n_2-1)$$
Vi kan kombinere dem (_pooling_) for at lave en fælles estimator. Dette bliver et _vægtet gennemsnit_ af $S_1^2$ og $S_2^2$.
$$S_P^2=\frac {(n_1-1)S^2_1 + (n_2 - 1) S_2^2}{n_1 + n_2 - 2}\sim \frac {\sigma^2}{n_1 + n_2 - 2}\mathcal X^2(n_1 + n_2 - 2)$$

Nu hvor vi har estimeret den ukendte varians, kan vi opstille en ny test-statistic. _Nu bliver det en Student T fordeling, eftersom vi bruger estimeret varians_.
$$\boxed {T_0:=\frac {(\bar X_1 - \bar X_2)-\Delta_0}{S_P\sqrt{\frac 1 {n_1 + \frac 1 {n_2}}}}\sim t(n_1+n_2-2)}$$
Vi indsætter estimatorer, så: $T_0=t_0$
![[Pasted image 20261106085913.png]]

Vi forkaster $H_0$ for $|t_0|>t(n_1+n_2-2)_{\alpha/2}$.

Vi kan ligesom før opstille et [[Confidence Intervals (CI)]]
$$CI:\quad \left[(\bar X_1 - \bar X_2)\pm t(n_1+n_2-2)_{\alpha/2\right]$$

Eller for $p$-værdi
![[Pasted image 20261106090053.png]]

$$p=2P(t(n_1+n_2-2)>|t_0|)=2(1-P(t(n_1+n_2-2)\leq |t_0|))$$
hvor $P(t(n_1+n_2-2)\leq |t_0|)$ kan findes med `tcdf`.

---
#lecture 