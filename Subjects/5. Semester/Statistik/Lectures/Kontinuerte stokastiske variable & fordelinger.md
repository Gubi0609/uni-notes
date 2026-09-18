
> [!help] Central Limit Theorem
> Bruges til at kunne lave en hvilken som helst fordeling om til _normal fordeling_.
> Se [[#Central Limit Theorem]]

> [!help] Case 1: [[#Case 1 Uniform fordeling|Uniform fordeling]]
> $$X\sim U(a,b)\quad a,b\in \mathbb R$$
> 
> **PDF**
> $$f_X(x)=\left\{\begin{array} &  \frac 1 {b-a} & a\leq x \leq b \\ 0 & ellers \end{array}\right.$$
> 
> **CDF**
> Bare integrer PDF
> 
> **Middelværdi**
> $$\mu_X=E[X]=\frac {a+b}2$$
> 
> **Varians**
> $$\sigma^2=V[X]=\frac {(b-a)^2}{12}$$

> [!help] Case 2: [[#Case 2 Normal (Gaussian) fordeling|Normal fordeling]]
> $$X\sim N(\mu, \sigma^2)$$
> 
> **PDF**
> $$f_X(x)=\frac 1 {\sqrt{2\pi}\cdot\sigma}e^{-\frac 1 2(\frac {x-\mu} {\sigma})^2}$$
> 
> **Standard Normal Fordeling**
> $$Z\sim N(\mu=0, \sigma^2=1)$$
> $$P(a\leq X\leq b)=P(\frac {a-\mu}\sigma \leq \frac {X-\mu}\sigma\leq \frac {b-\mu}\sigma)=F_Z\left(\frac {b-\mu}{\sigma}\right)-F_Z\left(\frac {a-\mu}\sigma\right)$$
> 
> **Lineær Kombination**
> $$Y=\sum_{i=1}^n a_iX_i=a_1X_1+...+a_nX_n\sim N\left(\sum_{i=1}^n a_i\mu_i=\mu_y, \sum_{i=1}^n a_i^2\sigma_i^2=\sigma_y^2\right)$$

> [!help] Case 3: [[#Case 3 Eksponentiel fordeling|Eksponentiel fordeling]]
> $$X\sim \text{Exp}(\lambda)$$
> 
> **CDF**
> $$F_T(t)=P(T\leq t)=1-e^{-\lambda t}$$
> 
> **PDF**
> $$f_T(t)=\frac {dF_T(t)}{dt}=\lambda e^{-\lambda t}$$
> 
> **Middelværdi**
> $$\mu=E[T]=\frac 1 \lambda$$
> **Varians**
> $$\sigma^2=V[T]=\frac 1 {\lambda^2}$$

> [!help] Case 4: [[#Case 4 Binomial fordeling|Binomial fordeling]]
> $$X\sim \text{Bin}(n, p)$$
hvor $np>>1$ og $np(1-p)>> 1$.
$$Z=\frac {X-np} {\sqrt{np(1-np)}}\sim N(0,1)$$

> [!help] Case 5: [[#Case 4 Poisson fordeling|Pois]]

---
Ligesom [[Diskrete stokastiske variable & fordelinger]] har vi et sample space $S$ og et sæt af stokastiske variable $X$.
$$X: S\rightarrow I\subseteq \mathbb R$$

# Probability *Density* Function, PDF
På dansk kunne man kalde det en sandsynligheds-*tætheds* funktion

Skrevet $f_X(x)$ ligesom [[Diskrete stokastiske variable & fordelinger#Probability mass function, PMF|PMF]].
![[Pasted image 20260918082149.png|284]]

$$f_X(x):=\frac {P(X\in[x,x+dx])}{dx}$$
![[Pasted image 20260918082328.png|309]]
$$P(a\leq X\leq b)=\int_a^b f_X(x)dx$$

$f_X(x)$ er _likelihood_.

Der gælder
$$\int_{-\infty}^\infty f_X(x)dx=1\quad [P(s)=1]$$
$$f_X(x)\geq 0$$

Da vi bruger integraler her, gælder der også
$$P(X=x)=0$$
Da arealet for et specifikt x-punkt er 0.

# Cumulative Probability Density Function, CDF
På dansk: fordelingsfunktion

Skrevet $F_X(x)$.
$$F_X(x):=F(X\leq x)=\int_{-\infty}^xf_X(u)du$$
![[Pasted image 20260918083233.png|323]]

_Svagt monoton_, stiger langsomt. Starter i 0, og stiger til 1.

Vi kan finde $f_X(x)$ fra $F_X(x)$
$$f_X(x)=\frac {dF_X(x)}{dx}\geq 0$$

$$\lim_{x\rightarrow -\infty}F_X(x)=0$$
$$\lim_{x\rightarrow \infty}F_X(x)=1$$
Det ovenover skriver bare, at den starter i 0 og slutter i 1.

$$P(a\leq X\leq b)=\int_a^b f_X(x)dx=F_X(b)-F_X(a)$$
I modsætning til [[Diskrete stokastiske variable & fordelinger#Cumulative probability function, CMF|CMF]] behøver vi ikke fire forskellige udgaver af ovenstående formel. Noget med Dirac Delta, som vi ikke bruger. Anyways, det virker bare!

# Middelværdi (Mean) af X
Skrevet $\mu_X$

$$\mu_X=E[X]=\int_{-\infty}^\infty x\cdot f_X(x)$$
Hvor $E[X]$ er _forventet værdi_ eller _expectancy_
![[Pasted image 20260918084209.png|369]]

Man kan også tænke på middelværdien som _tyngdepunkt_. Hvis vi have en længere hale, ville tyngdepunktet blive påvirket meget af den, og altså rykke sig længere langs den.

$$E[h(x)]=\int_{-\infty}^\infty h(x)\cdot f_X(x)dx$$
hvor $h(x)$ er en tilfældig funktion af $x$.

# Varians (Variance) af X
Bruges til at beskrive spredningen(ikke helt sikker på, at det er det rigtige ord at bruge), da flere kan have samme [[#Middelværdi (Mean) af X|middelværdi]] men anderledes varians
![[Pasted image 20260918084723.png]]

$$\sigma^2=V[X]:=E[(X-\mu_X)^2]=E[X^2]-\mu_X^2 =\int_{-\infty}^\infty (x-\mu_X)^2\cdot f_X(x) dx\geq 0$$

Hvis vi i stedet for $X^2$ bruger $X^3$ hedder det _skewness_, men det bruger vi ikke rigtig.
## Standardafvigelse
$$\sigma_X=+\sqrt{\sigma_X^2}$$
Har samme enhed som $X$.

# Case 1: Uniform fordeling
_Continuos uniform distribution_
Betyder at alle udfald er lige sandsynlige
$$X\sim U(a,b)\quad a,b\in \mathbb R$$

I matlab, skrives `x=a+b*rand`. `rand` generer et tilfældigt tal mellem 0 og 1.

## PDF
![[Pasted image 20260918085853.png|366]]
Arealet under grafen er 1. Dette er i henhold til [[#Probability *Density* Function, PDF|PDF]].

$$f_X(x)=\left\{\begin{array} &  \frac 1 {b-a} & a\leq x \leq b \\ 0 & ellers \end{array}\right.$$

## CMF
![[Pasted image 20260918090124.png|357]]

## Middelværdi
Middelværdien ligger nødvendigvis i midten, da alle udfald i mellem a og b er lige sandsynlige
$$\mu_X=E[X]=\frac {a+b}2$$
## Varians
$$\sigma^2=V[X]=\frac {(b-a)^2}{12}$$
Kommer af den generelle formel for [[#Varians (Variance) af X|Varians]], men vi gider ikke udlede det.

# Case 2: Normal (Gaussian) fordeling
$$X\sim N(\mu, \sigma^2)$$
Her bruger vi [[#Middelværdi (Mean) af X|middelværdien]] og [[#Varians (Variance) af X|variansen]] direkte som parametre.

> Lineære kombinationer af normalfordelinger giver nye normal fordelinger med summeret middelværdier og summeret varians fra lineær kombinations komponenter. $X_1, ..., X_n$ uafhængige $X_i \sim N(\mu_i, \sigma^2_i)$
> $$Y=\sum_{i=1}^n a_iX_i=a_1X_1+...+a_nX_n\sim N\left(\sum_{i=1}^n a_i\mu_i=\mu_y, \sum_{i=1}^n a_i^2\sigma_i^2=\sigma_y^2\right)$$
## PDF
$$f_X(x)=\frac 1 {\sqrt{2\pi}\cdot\sigma}e^{-\frac 1 2(\frac {x-\mu} {\sigma})^2}$$
![[Pasted image 20260918093345.png|317]]

$$\mu\pm3\sigma :99.7\%$$
Ovenstående betyder at 99.7% af alle udfald ligger indenfor det beskrevne område.

## Standard Normal Fordeling
Skrevet $Z$
$$Z\sim N(\mu=0, \sigma^2=1)$$
Den er normal fordelt, men har en middelværdi på 0 og en varians på 1.

[[#Probability *Density* Function, PDF|PDF]] skrives også $f_Z(z)=\phi(z)$ (kaldet _normpdf_) og [[#Cumulative Probability Density Function, CDF|CDF]] skrives $F_Z(z)=\Phi(z)$ (kaldet _normcdf_)

## Standardisering
Vi normerer en normal fordeling til at blive til en standard normal fordeling
$$X\sim N(\mu,\sigma^2)\Rightarrow Z=\frac {X-\mu}{\sigma}\sim N(0,1)$$

Vi kan så finde sandsynligheden for at være mellem a og b ved bruge standardisering.
$$P(a\leq X\leq b)=P(\frac {a-\mu}\sigma \leq \frac {X-\mu}\sigma\leq \frac {b-\mu}\sigma)=F_Z\left(\frac {b-\mu}{\sigma}\right)-F_Z\left(\frac {a-\mu}\sigma\right)$$

# Central Limit Theorem
På dansk: Central grænseværdi sætning
Vi har $x_1, x_2, ..., x_n$ som er _uafhængige_ og kommer fra _samme fordeling_
$$E[X]=\mu$$
$$V[X]=\sigma^2$$

Skal _ikke_ være normalfordel

$$\bar X=\frac 1 n \sum_{i=1}^n X_i\rightarrow^{n\rightarrow \infty} \bar X\sim N(\mu, \frac {\sigma^2}n)$$
$\bar X$ er _gennemsnittet_ af $X$.

Vi kan tage enhver form for fordeling, og tilpasse det [[#Normal (Gaussian) fordeling]].

Kan også bruges i sammenhæng med [[#Normal (Gaussian) fordeling|lineær kombination]].
$$\bar X=\frac 1 n \sum_{i=1}^nX_i\sim N\left(\sum_{i=1}^n\frac 1 n\mu,\sum_{i=1}^n\left(\frac 1 n\right)^2\sigma^2\right)\sim N\left(\mu, \frac {\sigma^2}n\right)$$

# Case 3: Eksponentiel fordeling
$$X\sim \text{Exp}(\lambda)$$
Hvor $\lambda$ er _ankomst intensitet_. (Bruges i sammenhæng med [[Diskrete stokastiske variable & fordelinger#Case 4 Poisson fordeling|Poisson fordeling]], der tæller ankomster). Lambda har enheden $s^{-1}$.
Eksponentiel fordeling tæller _ventetid_.

Vi har variablen $T$ som er _ventetid til næste ankomst_.
$$P(T>t)=P(\text{0 ankomster i }[0,t])=e^{-\lambda t}$$

## CDF
$$F_T(t)=P(T\leq t)=1-e^{-\lambda t}$$
![[Pasted image 20260918100541.png|330]]
## PDF
$$f_T(t)=\frac {dF_T(t)}{dt}=\lambda e^{-\lambda t}$$
![[Pasted image 20260918100515.png|350]]

## Middelværdi
$$\mu=E[T]=\frac 1 \lambda$$
## Varians
$$\sigma^2=V[T]=\frac 1 {\lambda^2}$$

# Case 4: Binomial fordeling
$$X\sim \text{Bin}(n, p)$$
hvor $np>>1$ og $np(1-p)>> 1$.
$$Z=\frac {X-np} {\sqrt{np(1-np)}}\sim N(0,1)$$
# Case 4: Poisson fordeling
$$X\sim\text{Poisson}(\lambda)$$
$$Z=\frac {X-\lambda}{\sqrt{\lambda}}\sim N(0,1)$$
