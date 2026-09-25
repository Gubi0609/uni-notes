
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
![[Pasted image 20260925102315.png]]

$$f_{X,Y}(x,y):=P(X=x, Y=y)$$
$$0\leq f_{X,Y}(x,y)\leq 1$$
$$\sum_x\sum_y f_{X,Y}(x,y)=1$$

Alle værdier af $f_{XY}(x,y)$ er mellem 0 og 1, så _check_.
$$\sum_x\sum_y f_{X,Y}(x,y)=\frac 1 8+\frac 2 8+ \frac 4 8+\frac 1 8=\frac 8 8 =1$$
_Alle regler er opfyldt._

- a.
Til dette skal vi bruge dens [[Diskrete stokastiske variable & fordelinger#Cumulative probability function, CMF|CMF]].
 $$F_X(x_i):=P(X\leq x_i)=\sum_{x_j\leq x_i} P(X=x_j)=\sum_{x_j \leq x_i} f_X(x_j)$$
 $$P(X<0.5,Y<1.5)=\sum_{x_i<0.5}\sum_{y_i<1.5}f_{XY}(x_i, y_i)=\frac 1 8+\frac 1 4=\frac 3 8$$

- b.
$P(X<0.5)$. Det er det samme svar som i opgave _a_, da vi der også kun gik op til værdier af $x$ som var under $0.5$.

- c.
$$P(Y<1.5)=\sum_{x_i}\sum_{y_i<1.5}f_{XY}(x_i,y_i)=\frac 1 8+\frac 1 4+\frac 1 2=\frac 7 8$$

- d.
$$P(X>0.25,Y<4.5)=\sum_{x_i>0.25}\sum_{y<4.5}f_{XY}(x_i,y_i)=\frac 1 2+\frac 1 8=\frac 5 8$$

- e.
$$f_X(x)=\sum_y f_{X,Y}(x,y)$$
$$\mu_x=E[X]=\sum xf_X(x)dx$$
$$\sigma_x^2=V[X]=\sum x^2f_X(x)-\mu_x^2 dx$$


Da der kun er 1 række af $y$ værdier og 1 række af $x$ værdier, er $f_X(x)=f_Y(y)=f_{XY}(x,y)$.

$$\mu_x=\sum_xx_if_{X}(x_i)=-1\cdot \frac 1 8-0.5\cdot \frac 1 4+0.5\cdot \frac 1 2+1\cdot\frac 1 8=\frac 1 8$$
$$\sigma_x^2=\sum_xx_i^2f_X(x_i)-\mu_x^2=\left((-1)^2\cdot\frac 1 8-\left(\frac 1 8\right)^2\right)+\left((-0.5)^2\cdot\frac 1 4 - \left(\frac 1 8\right)^2\right)+\left(0.5^2\cdot\frac 1 2-\left(\frac 1 8\right)^2\right)+\left(1^2\cdot \frac 1 8-\left(\frac 1 8\right)^2\right)$$
$$\sigma_x^2=\left(\frac 1 8-\frac 1 {16}\right)+\left(0.25\cdot\frac 1 4-\frac 1 {16}\right)+\left(0.25\cdot\frac 1 2-\frac 1 {16}\right)+\left(\frac 1 8-\frac 1 {16}\right)=\frac 1{16}+0+\frac 1{16}+\frac 1{16}=\frac 3 {16}$$

$$\mu_y=\sum_yy_if_{y}(y_i)=-2\cdot\frac 1 8-1\cdot\frac 1 4+1\cdot\frac 1 2+2\cdot\frac 1 8=\frac 3 4$$
$$\sigma_y^2=\sum_yy_i^2f_Y(y_i)-\mu_y^2=$$



![[Pasted image 20260925102325.png]]


![[Pasted image 20260925102342.png]]


![[Pasted image 20260925102356.png]]
![[Pasted image 20260925102407.png]]


![[Pasted image 20260925102427.png]]


![[Pasted image 20260925102449.png]]


![[Pasted image 20260925102504.png]]



---
#lecture 