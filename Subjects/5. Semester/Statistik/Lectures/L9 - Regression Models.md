
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
[[Simple Linear Regression (SLR)]]

# Notes
![[Pasted image 20261113101217.png]]

- a.
Vi skal bruge formlerne
$$\boxed{\hat\beta_1=\frac {\sum_{i=1}^nx_iY_i-n\bar x\bar Y}{\sum_{i=1}^nx_i^2-n\bar x^2}=\frac {\sum_{i=1}^n(x_i-\bar x)(Y_i-\bar Y)}{\sum_{i=1}^n(x_i-\bar x)^2}=\frac {S_{xY}}{S_{xx}}}$$
og
$$\boxed{\hat \beta_0=\bar Y-\hat\beta_1\bar x}$$

Til dette skal vi bruge mean af $x$ og $y$.
Efter det, starter vi med at finde $\hat  \beta_1$. Ledet $S_{xx}$ kan omskrives til
$$\sum_{i=1}^nx_i^2-\bar x^2=\bar x^2\sum_{i=1}^nx_i^2$$

![[Pasted image 20261113101234.png]]

![[Pasted image 20261113101247.png]]

![[Pasted image 20261113101303.png]]

![[Pasted image 20261113101322.png]]

![[Pasted image 20261113101340.png]]

![[Pasted image 20261113101356.png]]

![[Pasted image 20261113101405.png]]


---
#lecture 