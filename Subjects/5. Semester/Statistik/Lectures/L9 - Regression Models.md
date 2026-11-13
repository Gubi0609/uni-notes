
---
**Date:** 2026-11-13

## Preparation

>[!TODO] HOMEWORK
>- [ ] 

> [!DANGER] EXERCISES
> - [ ] 11.2.1, 11.2.3, 11.2.6, 11.2.10, 11.7.3, 11.7.5, 11.9.1, 11.9.2

---
# Relevant documents
[[Agenda lecture 09.pdf]]
[[Lektion 9 slides.pdf]]
[[Solutions lecture 09 v3.pdf]]

# Topics


# Notes

# Simple Linear Regression

# Introduktion til lineær regression
Vi har parvise data $(x_i,y_i),\quad i=1,..., n$.

Vi laver et _scatter plot_ mellem $x$ og $y$.
![[Pasted image 20261113082105.png]]

De røde og blå datapunkter har en tydelige lineær sammenhæng. Den grønne er ikke lineær, men vi kan muligvis godt bruge den stadigvæk. Den orange samling har ingen sammenhæng, så der kan vi _ikke lave nogen regression._

## Mål med lineær regression
- Find "bedste" (lineære) sammenhæng mellem $x$ og $y$
- Estimer modellens parametre
- Model check
- Vurder model fit ($R^2$)

For alt det ovenstående er der **ingen antagelse om fordeling**.

# Foranalyse: Giver det mening at lave en SLR model?
- 1. Lav scatter plot
- 2. Beregn _sample correlationskoefficient_.
	- Teoretisk covarians $\sigma_{xy}=\text{cov}(x,y) = E[(X-\mu_x)(Y-\mu_y)]$ 
	- For [[#Introduktion til lineær regression|ovenstående scatter plots]] har det røde plot _positiv_ covariance, blå har _negativ_ og orange har **covarians på cirka 0**.
	- Correnlationskoefficient: $$\varrho_{xy}=\frac {\sigma_{xy}}{\sigma_x\sigma_y},\quad -1\leq \varrho_{xy}\leq 1$$
	- Sample covarians: $$\hat \sigma_{xy}=s_{xy} = \frac 1 {n-1}\sum_{i=1}^n(x_i-\bar x)(y_i-\bar y)$$
		- Sample covarians, har samme fortegn som den teoretiske covarians.

Med sample covarians fundet, kan vi omskrive correlationskoefficienten
$$\hat \varrho_{xy}=r_{xy}=

---
#lecture 