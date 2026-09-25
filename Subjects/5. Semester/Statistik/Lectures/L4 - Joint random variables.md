
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





---
#lecture 