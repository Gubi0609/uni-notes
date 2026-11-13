
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
Vi har parvise data $(x_i,Y_i),\quad i=1,..., n$.

Vi laver et _scatter plot_ mellem $x$ og $Y$.
![[Pasted image 20261113082105.png]]

De røde og blå datapunkter har en tydelige lineær sammenhæng. Den grønne er ikke lineær, men vi kan muligvis godt bruge den stadigvæk. Den orange samling har ingen sammenhæng, så der kan vi _ikke lave nogen regression._

## Mål med lineær regression
- Find "bedste" (lineære) sammenhæng mellem $x$ og $Y$
- Estimer modellens parametre
- Model check
- Vurder model fit ($R^2$)

For alt det ovenstående er der **ingen antagelse om fordeling**.

# Foranalyse: Giver det mening at lave en SLR model?
- 1. Lav scatter plot
- 2. Beregn _sample correlationskoefficient_.
	- Teoretisk covarians $\sigma_{xY}=\text{cov}(x,Y) = E[(x-\mu_x)(Y-\mu_Y)]$ 
	- For [[#Introduktion til lineær regression|ovenstående scatter plots]] har det røde plot _positiv_ covariance, blå har _negativ_ og orange har **covarians på cirka 0**.
	- Correnlationskoefficient: $$\varrho_{xY}=\frac {\sigma_{xY}}{\sigma_x\sigma_Y},\quad -1\leq \varrho_{xY}\leq 1$$
	- Sample covarians: $$\hat \sigma_{xY}=s_{xY} = \frac 1 {n-1}\sum_{i=1}^n(x_i-\bar x)(Y_i-\bar Y)$$
		- Sample covarians, har samme fortegn som den teoretiske covarians.

Med sample covarians fundet, kan vi finde _sample correlationskoefficienten_
$$\hat \varrho_{xY}=r_{xY}=\frac {s_{xY}}{s_xs_Y},\quad -1\leq \hat\varrho_{xY}\leq 1$$

> Hvis scatterplot er "OK" og $|r_{xy}|>\text{ca }75-80\%$ kan vi lave lineær regression.
> 	Fjern eventuelle outliers (hvis de kan fjernes)

# Model

Vi vil gerne finde en lineær sammenhæng mellem $x$ og $y$:
$$Y_i=\beta_0+\beta_1x_i+\epsilon_i$$
hvor $\epsilon_i$ er en mulig fejl. $x_i$ er en _predictor variabel_, $Y_i$ er _respons variabel_.
$\beta_0$ og $\beta_1$ er ukendt skæring og hældning.

## Antagelser

Fejlens middel skal være _0_. Det vil sige at linjen skal gå i gennem midten af punkterne
$$E[\epsilon_i]=0$$
Vi antager også at variansen af fejlene er _konstant_, men ukendt
$$V[\epsilon_i]=\sigma^2$$
## Least Squares estimation of regression coefficients

Vi opstiller en _least squares cost fkunktion_, **Sum of Squared Errors**
$$SSE=\sum_{i=1}^n \hat \epsilon_i^2 = \sum_{i=1}^n\left(Y_i-\left(\hat\beta_0+\hat\beta_1x_i\right)\right)^2$$
hvor $\hat \epsilon_i$ er fejlen mellem det estimeret punkt (i følge linjen) $(x_i, \hat Y_i)$ og det målte punkt $(x_i, Y_i)$.

> Vi har ikke $\hat\beta_0$ eller $\hat\beta_1$ endnu, men det er dem vi skal til at finde...

![[Pasted image 20261113084825.png]]

Vores projektion er
$$\hat Y_i=\hat \beta_0 + \hat\beta_1x_i$$

og residuel er
$$\hat \epsilon_i=Y_i-\hat Y_i$$

**Vi vil gerne minimere vores SSE, som derved giver os $\hat\beta_0$ og $\hat\beta_1$.**
Det gør vi ved at sætte gradienten (to variabel differentiering...) lig med 0
$$\nabla SSE=0\Leftrightarrow \left\{\begin{array}{}\frac {\delta SSE}{\delta \hat\beta_0} = 0\\ \frac {\delta SSE}{\delta \hat\beta_1}=0\end{array}\right.$$
$$\frac {\delta SSE}{\delta \hat \beta_0}=-2\sum_{i=1}^n\left(Y_i-(\hat\beta_0+\hat\beta_1x_i)\right)=0$$
$$\sum_{i=1}^n Y_i=n\cdot\hat\beta_0+\hat\beta_1\sum_{i=1}^nx_i$$
$$\bar Y = \hat\beta_0 + \hat\beta_1 \bar x\Leftrightarrow\boxed{\hat \beta_0=\bar Y-\hat\beta_1\bar x}$$


$$\frac {\delta SSE}{\delta \hat\beta_1}=2\sum_{i=1}^n \left(Y_i - (\hat\beta_0+\hat\beta_1x_i)\right)x_i=0$$
$$\sum_{i=1}^n x_iY_i=\hat\beta_0 \sum_{i=1}^n x_i+\hat\beta_1\sum_{i=1}^n x_i^2$$
Vi indsætter fra den ovenstående funktion for $\bar Y$
$$\sum_{i=1}^n x_iY_i=\left(\bar Y - \hat\beta_1\bar x\right)\sum_{i=1}^nx_i+\hat\beta_1\sum_{i=1}^nx_i^2$$
$$\sum_{i=1}^nx_iY_i-\bar Y\sum_{i=1}^n x_i=\hat\beta_1\left(\sum_{i=1}^nx_i^2-\bar x\sum_{i=1}^nx_i\right)$$
$$\boxed{\hat\beta_1=\frac {\sum_{i=1}^nx_iY_i-n\bar x\bar Y}{\sum_{i=1}^nx_i^2-n\bar x^2}=\frac {\sum_{i=1}^n(x_i-\bar x)(Y_i-\bar Y)}{\sum_{i=1}^n(x_i\bar x)^2}}$$

Ved at kombinere disse to ligninger, **kan vi finde $\hat\beta_0$ og $\hat\beta_1$**.
I MATLAB kan vi bare bruge `regress`.

For at kunne sige hvor sikker vi er på vores fundne linje, skal vi også kunne sige hvor _usikker_ vi er på den. Det gør vi via. **varians**.
Vi husker vores [[#Antagelser]]


---
#lecture 