
---
**Date:** 2026-09-25

## Preparation

>[!TODO] HOMEWORK
>- [ ] 

> [!DANGER] EXERCISES
> - [ ] 5.1.2, 5.1.9, 5.4.1, 5.4.7, 5.6.1, 5.6.9, 5.7.3

---
# Relevant documents
[[Agenda lecture 04.pdf]]
[[Lektion 4 slides.pdf]]
[[Solutions lecture 04 v3.pdf]]

# Topics


# Notes

# Simultane stokastiske variable
Vi har et stokastisk udfald $a_1$ i sample space $S$ som vi mapper til en $x$ og $y$ værdi
$$(x,u):S\rightarrow \mathbb R^2$$

![[Pasted image 20260925082115.png|590]]

## Diskret (x, y)
Vi har en [[Diskrete stokastiske variable & fordelinger#Probability mass function, PMF|simultan PMF]]
$$f_{X,Y}(x,y):=P(X=x, Y=y)$$
$$0\leq f_{X,Y}(x,y)\leq 1$$
$$\sum_x\sum_y f_{X,Y}(x,y)=1$$

| $f_{X,Y}(x,y)$ | $X=x_1$ | $X=x_2$      | ... | $X=x_n$ |
| -------------- | ------- | ------------ | --- | ------- |
| $Y=y_1$        | ...     | $P(x_2,y_1)$ | ... | ...     |
| $Y=y_2$        | ...     | ...          | ... | ...     |
| ...            | ...     | ...          | ... | ...     |
| $Y=y_n$        | ...     | ...          | ... | ...     |

### Marginal PMF
Marginal betyder _at man kun kigger på den ene af de stokastiske variable_
$$f_X(x)=\sum_y f_{X,Y}(x,y)$$
Ved at summere over $y$ fjerner vi dens indflydelse på resultatet. Vi kan summere over $x$ for at finde $f_Y(y)$.

### Betinget PMF
_Hvad er sandsynligheden for at $y$ har en bestemt værdi, hvis jeg kender $x$ værdien?_
Vi bruger her [[Betinget Sandsynlighed]].
$$P(Y|X)=f_{Y|X}(y|x)=\frac {f_{X,Y}(x,y)}{f_X(x)}$$

Samme den modsatte vej
$$P(X|Y)=f_{X|Y}(x|y)=\frac {f_{X,Y}(x,y)}{f_Y(y)}$$
## Kontinuert (x,y)
Vi har en [[Kontinuerte stokastiske variable & fordelinger#Probability *Density* Function, PDF|simultan PDF]].
$$f_{X,Y}(x,y)\geq 0$$
$$\int\int_{\mathbb R^2} f_{X,Y}(x,y)=1$$



---
#lecture 