
---
**Date:** 2026-09-11

## Preparation

>[!TODO] HOMEWORK
>- [ ] 

> [!DANGER] EXERCISES
> - [ ] 3.1.10, 3.1.11, 3.2.8, 3.3.1, 3.3.7, 3.4.1, 3.5.2, 3.5.4, 3.5.13, 3.6.1, 3.8.2

---
# Relevant documents
[[Agenda lecture 02.pdf]]
[[Lektion 2 slides.pdf]]
[[Solutions lecture 02 v3.pdf]]

# Topics
[[Diskrete stokastiske variable & fordelinger]]

# Notes
For Exercises 3.1.10 to 3.1.12, verify that the following functions are probability mass functions, and determine the requested probabilities.
![[Pasted image 20260911103736.png]]

We must verify, that $f(x)$ is a PMF. For this, it must satisfy
$$f_X(x_i):=P(X=x_i)$$
$$\sum_{x_i\in S} f_X(x_i)=1,\quad 0\leq f_X(x_i)\leq 1$$
$$f(1)=\frac 8 7 \left(\frac 1 2\right)^1=\frac 4 7$$
$$f(2)=\frac 8 7 \left(\frac 1 2\right)^2=\frac 8 {28}=\frac {2}{7}$$
$$f(3)=\frac 8 7\left(\frac 1 2\right)^3=\frac 8 7\frac 1 8=\frac 8 {56}= \frac 1 7$$
$$\sum_{x_i\in S}f_X(x_i)=\frac 4 7+\frac 2 7+\frac 1 7=\frac 7 7=1$$
For the third criteria because the total probability of the variable $X$ having a value inside the domain $x_i = 1, 2, 3$ is equal to one then $f (x_i) = P (X = x_i)$.

- a)
We use CMF
 $$F_X(x_i):=P(X\leq x_i)=\sum_{x_j\leq x_i} P(X=x_j)=\sum_{x_j \leq x_i} f_X(x_j)$$
 $$P(X\leq 1)=\sum_{x_i\leq 1}f_X(1)=\frac 4 7$$
 - b)
We use CMF for the probability of 2 and 3
$$P(X>1)=\sum_{x_i>1}f_X(2)+f_X(3)=\frac 2 7+\frac 1 7=\frac 3 7$$
- c)
Again, CMF
$$P(x_i<X<x_j)=F_X(x_j)-F_X(x_i)-f_X(x_j)$$
$$P(2<X<6)=F_X(6)-F_X(2)-f_X(6)=\sum_{x_i\leq6}f_X(x_i)-\sum_{x_i\leq 2}f_X(x_i)-0=1-\left(\frac 4 7 +\frac 1 7\right)-0=1-\frac 5 7-0=\frac 3 7$$
- d)
$$P(X\leq 1\text{ or } X>1)$$
This is just asking us to verify, that $X$ is within the defined domain (1, 2, 3), which it of course is, so
$$P(X\leq 1\text{ or } X>1)=1$$

![[Pasted image 20260911110406.png]]

Again, we verify, that it is a PMF
$$f(0)=\frac {2\cdot 0+1}{25}=\frac 1 {25}$$
$$f(1)=\frac {2\cdot 1+1}{25}=\frac 3 {25}$$
$$f(2)=\frac {2\cdot 2+1}{25}=\frac 5{25}$$
$$f(3)=\frac {2\cdot 3+1}{25}=\frac 7 {25}$$
$$f(4)=\frac {2\cdot 4+1}{25}=\frac 9 {25}$$
$$\sum_{x_i\in S}f_X(x_i)=\frac 1{25}\frac 3 {25}+\frac 5{25}+\frac 7{25}+\frac 9{25}=\frac {25}{25}$$

- a)
We just check what the probability, that it is 4 is. We have already calculated this
$$P(X=4)=f(4)=\frac 9 {25}$$
- b)
We use CMF
 $$F_X(x_i):=P(X\leq x_i)=\sum_{x_j\leq x_i} P(X=x_j)=\sum_{x_j \leq x_i} f_X(x_j)$$
 $$P(X$$


---
#lecture 