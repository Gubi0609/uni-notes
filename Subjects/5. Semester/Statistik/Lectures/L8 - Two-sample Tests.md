
---
**Date:** 2026-11-06

## Preparation

>[!TODO] HOMEWORK
>- [ ] 

> [!DANGER] EXERCISES
> - [ ] 10.1.1 a+b, 10.2.2 a+b, 10.2.6, 10.2.11 a+b+c, 10.4.1, 10.4.3

---
# Relevant documents
[[Agenda lecture 08.pdf]]
[[Lektion 8 slides.pdf]]
[[Solutions lecture 08 v2.pdf]]

# Topics


# Notes
![[Pasted image 20261106101031.png]]

- a.
Vi får givet nul hypotesen $H_0: \quad \mu_1 = \mu_2 \Leftrightarrow \mu_1 - \mu_2 = \Delta_0, \quad \Delta_0 = 0$. Derfor kan vi bruge [[Hypotese test (2 populationer)#Case 1 Non-paired test (forskel i middelværdier) med _kendt_ varians|Non-paired test med kendt varians]] da vi også får givet variansen.

Vi starter med at ville estimere $\mu_1$ og $\mu_2$. Samtidigt finder vi også forskellen i gennemsnittende $\bar x_1$ og $\bar x_2$.
Til dette bruger vi følgende ligninger:

$$\hat\mu_1=\bar X_1 = \frac 1 n \sum_{i=1}^{n_1} x_{1i}\sim N(\mu_1, \sigma_1^2)$$
$$\hat\mu_2=\bar X_2 = \frac 1 n \sum_{i=1}^{n_2} x_{2i}\sim N(\mu_2, \sigma_2^2)$$
$$(\bar x_1-\bar x_2)\sim N(\mu_1-\mu_2, \frac {\sigma_1^2} {n_1} + \frac {\sigma_2^2} {n_2})$$

Dernæst opstiller vi vores test statistic og indsætter $H_0$ for at få $z_0$:



![[Pasted image 20261106101050.png]]



![[Pasted image 20261106101100.png]]
![[Pasted image 20261106101114.png]]



![[Pasted image 20261106101209.png]]



![[Pasted image 20261106101225.png]]



![[Pasted image 20261106101240.png]]



---
#lecture 