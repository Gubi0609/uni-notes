
---
**Date:** 2026-11-27

## Preparation

>[!TODO] HOMEWORK
>- [ ] 

> [!DANGER] EXERCISES
> - [ ] 

---
# Relevant documents
[[Agenda lecture 11.pdf]]
[[Lektion 11 slides.pdf]]
[[Solutions lecture 11 v2.pdf]]

# Topics


# Notes

# ANOVA 1

# Sammenligning $a>2$ populationer

## Model
![[Pasted image 20261127082043.png]]
Vi har $a$ _populationer_.
Bredden (??) af populationer er vores _faktorlevel_

For hver populationer har vi punkterne $x_{i1}, ... x_{in}$.
Antallet af de samlede punkter i populationerne er
$$N=\sum_{i=1}^a n_i$$

Fordelingen er
$$X_{ij}\sim N(\mu_i, \sigma^2)$$
Hvor $X_{ij}$ er _faktorevel_, $j$ er observations nummer (tror jeg...), og $\sigma^2$ er en fælles ukendt.

## Hypotese
$$H_0:\quad \text{alle }\mu_i=\mu$$
$$H_1:\quad \text{mindst }2\text{ } \mu_i \text{ forskellige}$$
eller
$$\mu_i=\mu+\tau_i$$
hvor $\mu$ er et fælles led og $\tau_i$ er en _faktoreffekt_.
Ud fra dette kan vi omskrive hypoteserne
$$H_0: \quad \text{alle } t_i=0\rightarrow \quad \forall t_i=0$$
$$H_1:\quad \text{mindst en }t_i \neq 0\rightarrow\quad \exists t_i\neq 0$$

## Notation og sample means

| Faktor | obs      | \# obs | sample mean |
| ------ | -------- | ------ | ----------- |
| $i=1$  | $x_{1j}$ | $n_1$  | $\bar x_1$  |
| $i=2$  | $x_{2j}$ | $n_2$  | $\bar x_2$  |
| $...$  | $...$    | $...$  | $...$       |
| $i=a$  | $x_{aj}$ | $n_a£  | $\bar x_a$  |

Population-wise:
$$\bar X_i=\frac 1 {n_i} \sum_{j=1}^{n_i} X_{ij}$$
Overall:
$$\bar X = \frac 1 N \sum_{i=1}^a \sum_{j=1}^{n_i}X_{ij}$$

## SS (sum of squares) decomposition
Tilsvarende til $R^2$ hvor godt en linje fitter til puntker...

$$\sum_{i=1}^a\sum_{j=1}^{n_i}(X_{ij}-\bar X)^2 = \sum_{i=1}^a\sum_{j=1}^{n_i}(X_{ij}-\bar X_i)^2+(\bar X_i - \bar X)^2$$
hvor $(X_{ij}-\bar X_i)$ er en _tilfældig variation_ og $(\bar X_i - \bar X)$ er en _systematisk variation_.
Vi genkender, at vi bruger populations wise og overall udregningerne fra før.




---
#lecture 