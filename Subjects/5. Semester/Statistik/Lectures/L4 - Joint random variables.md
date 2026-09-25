
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

**Kan også overføres til flere dimensioner end bare 2D**

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

Hvis vi har et område $A$ i vores x y-område
![[Pasted image 20260925084218.png|251]]

kan vi finde sandsynligheden for at være i det område som
$$P((X,Y)\in A)=\int\int_{A\subseteq \mathbb R^2}f_{X,Y}(x,y)dxdy$$

### Marginal PDF
Marginal betyder _at man kun kigger på den ene af de stokastiske variable_
$$f_X(x)=\int_{y\in\mathbb R} f_{X,Y}(x,y)dy$$
Det samme kan gøres ved  at integrere over $x$ for at finde $f_Y(y)$.
Der gælder selvfølgelig det samme for denne PDF som for en normal [[Kontinuerte stokastiske variable & fordelinger#Probability *Density* Function, PDF|PDF]].

### Betinget PDF
_Hvad er sandsynligheden for at $y$ har en bestemt værdi, hvis jeg kender $x$ værdien?_
Vi bruger her [[Betinget Sandsynlighed]].
$$P(Y|X)=f_{Y|X}(y|x)=\frac {f_{X,Y}(x,y)}{f_X(x)}$$

Samme den modsatte vej
$$P(X|Y)=f_{X|Y}(x|y)=\frac {f_{X,Y}(x,y)}{f_Y(y)}$$

## Uafhængige X, Y
Uafhængighed er ikke noget man kan bevise, men noget man skal _argumentere for_. Se eventuelt [[Sandsynlighed Basics#**Disjoint events** (disjunkt)|Disjoint events]] for sandsynligheder.

For to uafhængige sæt af stokastiske variable $X$ og $Y$, kan vi kombinere dem.
$$f_{X,Y}(x,y)=f_X(x)f_Y(y)$$

## Momenter for (X,Y)
Nedenstående regler for middelværdi og varians kan overføres mellem $x$ og $y$ ved bare at erstatte variablen.

### Middelværdi
$$\mu_x=E[X]=\int xf_X(x)dx$$
### Varians
$$\sigma_x^2=V[X]=E[(X-\mu_x)^2]=\int (x-\mu_x)^2f_x(x)dx=E[X^2]-\mu_x^2=\int x^2f_X(x)-\mu_x^2 dx$$
Skrives også $\sigma_{xx}$
### Covariance (Covarians)
_Hvordan varierer $X$ og $Y$ sammen **i middel**?_
Gælder når $X$ og $Y$ _ikke_ er uafhængige.

$$\text{Cov}(X,Y)=\sigma_{xy}:=E[(X-\mu_x)(Y-\mu_y)]$$
![[Pasted image 20260925092140.png|247]]

$\text{Cov}(X,Y)>0$: Når $X$ stiger, stiger $Y$ også _in the mean sense_
$\text{Cov}(X,Y)<0$: Når $X$ stiger, falder $Y$ i _in the mean sense_
$\text{Cov}(X,Y)\approx 0$: $X$ og $Y$ har ikke nogen lineær relation (**uncorrelated**)

Covariansen er _unnormed_, hvilket betyder at det **ikke er invariant overfor ændringer i unit/skalering**

### Korrelation
$$\rho_{XY}:=\frac {\sigma_{XY}} {\sigma_x\sigma_y}[]$$
$$-1\leq\rho_{XY}\leq1$$
Hvis $X$ og $Y$ er uafhængige, er der _ingen korrelation_:
$$\rho_{XY}=0$$
## Linear kombinationer af stokastiske variable
Vi har $X_1, X_2, ..., X_n$, $E[X_i]=\mu_i$, $V[X_i]=\sigma_1^2$

Vi definerer et nyt sæt $Y$
$$Y:=c_1X_1+c_2X_2+...+c_nX_n=\sum_{i=1}^nc_iX_i$$
Som har
$$E[Y]=\sum_{i=1}^nc_iE[X_i]$$
$$V[Y]=\sum_{i=1}^nc_i^2V[X_i]+\sum_{i=1}^n\sum_{j\neq i}^nc_ic_j\text{Cov}[X_i,X_j]$$
### Hvis $X_1, ..., X_n$ er _uafhængige_
$$V[Y]=\sum_{i=1}^nc_i^2V[X_i]$$

### Special case: $Y=c_1X_1+c_2X_2$ **IKKE** uafhængig
$$V[Y]=E[(Y-\mu_Y)^2]=c_1^2\sigma_1^2+c_2^2\sigma_2^2+2c_ac_2\text{Cov}(X_1,X_2)$$
Hvis $X_1$ og $X_2$ var uafhængige, ville der ikke være nogen korrelation, så det led ville forsvinde af sig selv.

### Ofte brugt linear kombination (gennemsnit af observationer)
$$\bar X:=\frac 1 n\sum_{i=1}^nX_i$$
med uafhængig $X_i$, $E[X_i]=\mu$, $V[X_i]=\sigma^2$.

$$E[\bar X]=\mu$$
$$V[\bar X]=\frac {\sigma^2}n$$

## Non-linear funktion af stokastisk variabel
Givet 
- $X$ med [[Kontinuerte stokastiske variable & fordelinger#Probability *Density* Function, PDF|PDF]] $f_X(x)$
- Non-linear funktion $y=h(x)$
- Ny stokastisk variable $Y=h(X)$

Så har stokastisk variabel $Y$ [[Kontinuerte stokastiske variable & fordelinger#Probability *Density* Function, PDF|PDF]]
$$f_Y(y)=\left|\frac {dh^{-1}(y)}{dy}\right|f_X(h^{-1}(y))$$
![[Pasted image 20260925100350.png|442]]

Vi kan også finde [[Kontinuerte stokastiske variable & fordelinger#Cumulative Probability Density Function, CDF|CDF]] for $Y$
$$F_Y(y)=P(Y\leq y)=P(h(X)\leq y)=P(X\leq h^{-1}(y))=F_X(h^{-1}(y))$$



---
#lecture 