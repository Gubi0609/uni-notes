
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
$$\hat\mu_1=\bar x_1 = \frac 1 n \sum_{i=1}^{n_1}


---
#lecture 