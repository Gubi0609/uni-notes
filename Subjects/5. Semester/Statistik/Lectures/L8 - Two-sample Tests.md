
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

## Recept
- Model + model check
- $H_0$, $H_1$
- Estimatere de størrelser der indgår i hypoteserne
- Definer test-statistic og fordeling
- Data + $H_0$ $\rightarrow$ TS-værdi
- _Enten_ vælg $\alpha$ og find A og C områder
- _Eller_ beregn p-værdi

## Case 1: Non-paired test (forskel i middelværdier) med _kendt_ varians
Vi har normalfordelt data:
- $X_{1i}\sim N(\mu_i, \sigma_1^2)$, $i=1,...,n_1$
- $X_{2i} \sim N(\mu_2,\sigma_2^2)$, $i=1,...,n_2$

Vi tjekker om modellen er sandsynlig ved model-check

### Hypoteser
$$H_0:\quad \mu_1-\mu_2=\Delta_0$$
hvor $\Delta_0$ er den postulerede størrelse. _$\Delta_0$ er ofte ligmed 0_.
$$H_1:\quad \mu_1-\mu_2\neq \Delta_0$$
Vi kan se ud fra $H_1$ at dette er en _to-sidet test_, da vi bruger $\neq$.

### Estimatorer
Vi estimerer $\mu_1$
$$\hat\mu_1=\bar X_1 = \frac 1 n \sum_{i=1}^{n_1} x_{1i}\sim N(\mu_1, \sigma_1^2)$$
og $\mu_2$
$$\hat\mu_2=\bar X_2 = \frac 1 n \sum_{i=1}^{n_2} x_{2i}\sim N(\mu_2, \sigma_2^2)$$

Vi kan så også finde forskellen i de to normalfordelinger
$$(\bar x_1-\bar x_2)\sim N(\mu_1-\mu_2, \frac {\sigma_1^2} {n_1} + \frac {\sigma_2^2} {n_2})$$
### Test statistic
Vi kan så definere test-statistic
$$Z_0:= \frac {(\bar x_1 - \bar x_2)-(\mu_1-\mu_2)}{\sqrt{\frac {\sigma_1^2}{n_1}+\frac {\sigma_2^2}{n_2}}}=^{H_0}\frac {(\bar x_1 - \bar x_2)-\Delta_0}{\sqrt{\frac {\sigma_1^2}{n_1}+\frac {\sigma_2^2}{n_2}}}\sim N(0,1)$$

### Indsæt data og $H_0$
Vi indsættet estimatorer og $H_0$: $Z_0=z_0$

![[Pasted image 20261106083340.png]]

Vi forkaster $H_0$ for $|z_0|>_{\alpha/2}$.

Eller for $p$-værdi
![[Pasted image 20261106083553.png]]

$$p=2P(Z>|z_0|)=2(1-P(Z<|z_0|))$$
Hvor $P(Z<|z_0|)$ kan findes med `normcdf(|z_0|)`.




---
#lecture 