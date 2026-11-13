- [[#Introduktion til lineær regression|Introduktion til lineær regression]]
	- [[#Introduktion til lineær regression#Non-linear regression|Non-linear regression]]
	- [[#Introduktion til lineær regression#Mål med lineær regression|Mål med lineær regression]]
- [[#Foranalyse: Giver det mening at lave en SLR model?|Foranalyse: Giver det mening at lave en SLR model?]]
- [[#Model|Model]]
	- [[#Model#Antagelser|Antagelser]]
	- [[#Model#Least Squares estimation of regression coefficients|Least Squares estimation of regression coefficients]]
	- [[#Model#Estimation af $\sigma^2$|Estimation af $\sigma^2$]]
	- [[#Model#Model check|Model check]]
	- [[#Model#Mål for model fit $R^2$|Mål for model fit $R^2$]]


# Introduktion til lineær regression
Vi har parvise data $(x_i,Y_i),\quad i=1,..., n$.

Vi laver et _scatter plot_ mellem $x$ og $Y$.
![[Pasted image 20261113082105.png]]

De røde og blå datapunkter har en tydelige lineær sammenhæng. Den grønne er ikke lineær, men vi kan muligvis godt bruge den stadigvæk. Den orange samling har ingen sammenhæng, så der kan vi _ikke lave nogen regression._

At vi har lineær regression betyder _IKKE_ at modellen er lineær i $x_i$, men at den er lineær _i regressions koefficenterne_ $\beta_0$ og $\beta_1$.
E.g. modellen $Y_i=\beta_0+\beta_1 x_i^2+\varepsilon_i$ er ikke lineær i $x_i$.
- Vi kan definere $z_i:=x_i^2$ og omskrive til $Y_i=\beta_0+\beta_1z_i+\varepsilon_i$.
- Så kan lineær regression teknikken bruges på datasættet $(z_i, Y_i)$ og producerer i dette eksempel den bedst passende parabel til $(x_i^2, Y_i)$.

## Non-linear regression
Nogen (men ikke alle) regressions modeller som _ikke er lineære i regressions koefficienterne_ kan omskrives til en _lineær model ved at omskrive variablene_.

E.g. Modellen $Y_i=\beta_0 e^{\beta_1x_i}$. Kan omskrives:
$$\log Y_i=\log \beta_0 + \beta_1 x_i\rightarrow Y_i^* = \beta_0^*+\beta_1^*x_i$$
![[Pasted image 20261113100652.png|370]]

Vi kan så lave SLR på $(Y_i^*, x_i)=(\log Y_i, x_i)$.
$$\hat\beta_0^*,\quad \hat \beta_1^*\rightarrow \left\{\begin{array}{}\hat\beta_0 = e\hat\beta_0^* \\ \hat\beta_1=\hat\beta_1^*\end{array}\right.$$
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

> Hvis scatterplot er "OK" og $|r_{xy}|\gtrapprox 75-80\%$ kan vi lave lineær regression.
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
$$SSE=\sum_{i=1}^n \hat \varepsilon_i^2 = \sum_{i=1}^n\left(Y_i-\left(\hat\beta_0+\hat\beta_1x_i\right)\right)^2$$
hvor $\hat \varepsilon_i$ er fejlen mellem det estimeret punkt (i følge linjen) $(x_i, \hat Y_i)$ og det målte punkt $(x_i, Y_i)$.

> Vi har ikke $\hat\beta_0$ eller $\hat\beta_1$ endnu, men det er dem vi skal til at finde...

![[Pasted image 20261113084825.png]]

Vores projektion er
$$\hat Y_i=\hat \beta_0 + \hat\beta_1x_i$$

og residuel er
$$\hat \varepsilon_i=Y_i-\hat Y_i$$

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
$$\boxed{\hat\beta_1=\frac {\sum_{i=1}^nx_iY_i-n\bar x\bar Y}{\sum_{i=1}^nx_i^2-n\bar x^2}=\frac {\sum_{i=1}^n(x_i-\bar x)(Y_i-\bar Y)}{\sum_{i=1}^n(x_i-\bar x)^2}=\frac {S_{xY}}{S_{xx}}}$$

Ved at kombinere disse to ligninger, **kan vi finde $\hat\beta_0$ og $\hat\beta_1$**.
I MATLAB kan vi bare bruge `regress`.

Man skal give funktionen i MATLAB en $Y$ søjle vektor og en matrix, der indeholder en søjle vektor med 1 taller og en søjle vektor med $x$ værdierner.
$$\left[\begin{array}{}Y_1\\Y_2\\...\\Y_n\end{array}\right]=\left[\begin{array}{}1 & x_1\\1 & x_2\\ ...&...\\1 & x_n\end{array}\right]\left[\begin{array}{}\beta_0\\ \beta_1\end{array}\right]$$

`regress(Y', [ones(size(x')) x'])`. **MATLAB giver ikke en fejlmeldning hvis man glemmer det, men svaret bliver forkert.**

## Estimation af $\sigma^2$
For at kunne sige hvor sikker vi er på vores fundne linje, skal vi også kunne sige hvor _usikker_ vi er på den. Det gør vi via. **varians**.
Vi husker vores [[#Antagelser|antagelser]].
$$V[\varepsilon_i]:=E[(\varepsilon_i-E[\varepsilon_i])^2]=E[\varepsilon_i^2]$$
$$\hat\sigma^2=\frac 1 {n-2} \sum_{i=1}^n \hat\varepsilon_i^2=\frac {SSE}{n-2}$$

## Model check
Vi laver et _residual plot_ for både $i$ og $Y_i$ (**de er ikke rent faktisk ens, jeg har bare været doven da jeg tegnede dem**)

![[Pasted image 20261113093837.png|449]]![[Pasted image 20261113093924.png|458]]

Vi kigger efter _uafhængighed_ og _konstant varians_.
Det skal gerne være lidt **kaotisk**. Altså ikke alle de små til venstre, eller andre mønstre der nu måtte være.

## Mål for model fit $R^2$

$R^2$ hedder egentlig _coefficient of determination_, men alle kalder det bare $R^2$.

Vi kan lave **Sum of Squares Decomposition**
$$\sum_{i=1}^n(Y_i-\bar Y)^2=\sum_{i=1}^n(Y_i-\hat Y_i)^2+\sum_{i=1}^n(\hat Y_i-\bar Y)^2$$
For lige at give navne til ligningens dele (fra venstre til højre): $SS_{TOTAL}=SST$, $SS_{ERROR}=SSE$, $SS_{REGRESS}=SSR$.

Vi kan så finde $R^2$
$$R^2=\frac {SSR}{SST}=\frac {\sum_{i=1}^n(\hat Y_i-\bar Y)^2}{\sum_{i=1}^n(Y_i-\bar Y)^2} = 1- \frac {SSE}{SST}=1-\frac {\sum_{i=1}^n(Y_i-\hat Y_i)^2}{\sum_{i=1}^n(Y_i-\bar Y)^2},\quad 0\leq R^2\leq 1$$

Vi har et _godt fit_ hvis $R^2\gtrapprox 0.8$.

![[Pasted image 20261113095102.png|350]]![[Pasted image 20261113095138.png|350]]
