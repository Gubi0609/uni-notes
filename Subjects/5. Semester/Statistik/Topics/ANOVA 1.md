- [[#Model|Model]]
- [[#Hypotese|Hypotese]]
- [[#Notation og sample means|Notation og sample means]]
- [[#SS (sum of squares) decomposition|SS (sum of squares) decomposition]]
	- [[#SS (sum of squares) decomposition#Frihedsgrader ($df$)|Frihedsgrader ($df$)]]
- [[#Variansestimater|Variansestimater]]
- [[#Test statistic|Test statistic]]
	- [[#Test statistic#Interpretation|Interpretation]]
- [[#Test|Test]]
	- [[#Test#$\alpha$|$\alpha$]]
	- [[#Test#$p$-værdi|$p$-værdi]]
- [[#ANOVA tabel|ANOVA tabel]]
- [[#Accept $H_0$|Accept $H_0$]]
- [[#Reject $H_0$|Reject $H_0$]]
- [[#Reject $H_0$#Hvorfor blev $H_0$ forkastet?|Hvorfor blev $H_0$ forkastet?]]

# Sammenligning $a>2$ populationer

## Model
![[Pasted image 20261127082043.png]]
Vi har $a$ _populationer_.
Bredden (??) af populationer er vores _faktorlevel_

For hver populationer har vi punkterne $x_{i1}, ... x_{in}$.
Antallet af de samlede punkter i populationerne er
$$N=\sum_{i=1}^a n_i$$
hvor $n_i$ er det samlede antal punkter i population $i$.

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

$$\sum_{i=1}^a\sum_{j=1}^{n_i}(X_{ij}-\bar X)^2 = \sum_{i=1}^a\sum_{j=1}^{n_i}(X_{ij}-\bar X_i)^2+\sum_{i=1}^a\sum_{j=1}^{n_i}(\bar X_i - \bar X)^2$$
hvor $(X_{ij}-\bar X_i)$ er en _tilfældig variation_ og $(\bar X_i - \bar X)$ er en _systematisk variation_.
Vi genkender, at vi bruger populations wise og overall udregningerne fra før.

Ovenstående udregning kalder vi $SS_{total}$. På højre side af lighedstegnet er det (venstre mod højre) $SS_{within}$ og $SS_{between}$.
Navnene giver lidt sig selv. _Within_ referer til at det er sum of squares _inden for_ populationerne, og _between_ referer til at det er sum of squares _i mellem_ populationerne.

Da $SS_{between}$ ikke har nogle $j$ punkter, kan vi skrive det lidt mere kompakt:
$$SS_{between}=\sum_{i=1}^a n_i(\bar X_i - \bar X)$$
> For nedenstående bruges $SS_{total}$ osv og deres forkortelser frit. Forkortelsen gør bare brug af første bogstav i subscript ($SS_{total}=SS_t$)

### Frihedsgrader ($df$)
Ud fra $SS_{total}$ kan vi skrive $df=N-1$. Da vi først må finde overall sample mean $\bar X$ mister vi en frihedsgrad.

På samme måde kan vi for $S_{within}$ skrive $df=N-a$. På samme måde som før, mister vi $a$ frihedsgrader, da vi skal finde population-wise sample mean først.

For den sidste, $SS_{between}$ kan vi skrive $df=a-1$.

## Variansestimater
Vi kan bruge frihedsgraderne til at finde estimater for variansen

For $SS_{total}$
$$S_T^2:=\frac {SS_{total}} {N-1}=\frac {SS_T} {df_T}=\widehat \sigma_T^2$$
For $SS_{within}$
$$S_W^2:=\frac {SS_W} {N-a} = \frac {SS_W}{df_W}=\widehat \sigma_W^2$$
For $SS_{between}$
$$S_B^2=:=\frac {SS_B}{a-1}=\frac {SS_{B}}{df_B}=\widehat \sigma_B^2$$

## Test statistic
Vi laver nu en test statistic for at sammenligne størrelser af varianser (??)
$$F_0:=\frac {S_B^2}{S_W^2}\sim F(a-1, N-a)$$
Da hver $S$ er chi i anden fordelt, og vi tager brøken mellem dem, er fordelingen af $F_0$ _fischer fordelt_ hvor parametrene er frihedsgraderne af hhv. $SS_B$ og $SS_W$.

### Interpretation
Vi indsætter vores data så
$$F_0=f_0,\quad f_0\in [0,\infty[$$
hvor $f_0$ er en talværdi.

Hvis
$$f_0 \text{ lille}\rightarrow H_0 \text{ is "probably" true}$$
ellers hvis
$$f_0\text{ stor} \rightarrow H_0 \text { is "probably" false}$$
> Grunden til at vi forkaster $H_0$ hvis $f_0$ er stor, er at fordelingen _mellem populationer_ derved er betydeligt større end fordelingen inden i populationer.

## Test
Vi vælger enten et signifikans niveau $\alpha$ eller en $p$-værdi

### $\alpha$
![[Pasted image 20261127085917.png]]

Ud fra vores [[#Hypotese|hypotese]] er det en _et-sidet_ test.

Så har vi altså defineret, hvad vi mener med "stor":
$$f_0>F(a-1, N-1)_\alpha \Rightarrow \text{forkast }H_0$$
### $p$-værdi
![[Pasted image 20261127090142.png]]

p-værdien er så sandsynligheden for at ende ude i halen:
$$p\text{-value}=P(F(a-1,N-1)>f_0)=1-P(F(a-1,N-1)<f_0)$$
Hvor sandsynligheden i sidste udregning kan findes i MATLAB ved `fcdf(f_0, a-1, N-a)`.

Så kan vi ud fra $p$-værdien sige
$$p\text{-value "lille"}\Rightarrow \text{forkast }H_0$$
Vi overlader det så til brugeren at foholde sig til $p$-værdien og ud fra det acceptere eller forkaste $H_0$.

# ANOVA tabel
ANOVA tabellen er en måde at samle al dataen i en let overskuelig tabel.

ANOVA tabellen er opbygget som følgende.

| Variation | $SS$   | $df$  | $S^2$   | $F$               |
| --------- | ------ | ----- | ------- | ----------------- |
| Between   | $SS_B$ | $a-1$ | $S_B^2$ | $F_0=S_B^2/S_W^2$ |
| Within    | $SS_W$ | $N-a$ | $S_W^2$ |                   |
| Total     | $SS_T$ | $N-1$ | $S_T^2$ |                   |

I MATLAB kan man bruge `anova1(X)` hvor `X` er sættet af populationer.
# Accept $H_0$
Vi kan omskrive vores model, da $H_0$ så er bevist, behøver vi ikke $i$ på $\mu_i$ ([[#Hypotese|hypotese]])
$$X_{ij}\sim N(\mu, \sigma^2)$$

Vi kan så også finde $\widehat \mu$ og $\widehat \sigma^2$ ud fra vores forrige udregninger
$$\widehat \mu = \bar X\sim N(\mu, \frac {\sigma^2} N)$$
hvor $\bar X$ er [[#Notation og sample means|over all sample mean]].

$$\widehat \sigma^2 = S_T^2=\frac {SS_T} {N-1}$$
Vi bruger det totale [[#Variansestimater|varians estimat]], da den har flest frihedsgrader.

Vi kan så også opstille et [[Confidence Intervals (CI)|konfidensinterval]].
$$\frac {\bar X - \mu}{\sqrt{\widehat \sigma^2 / N}}\Rightarrow CI:\quad \left[\bar X \pm t(N-1)_{\alpha/2}\sqrt{\frac {\widehat \sigma^2} N}\right]$$

# Reject $H_0$
Da vi ikke kan tro på at vores $\mu_i$ er ens ([[#Hypotese|hypotese]]), er modellen
$$X_{ij}\sim N(\mu_i, \sigma^2)$$

Vi kan så også finde $\widehat \mu_i$ og $\widehat \sigma^2$
$$\widehat \mu_i = \bar X_i \sim N(\mu_i, \frac {\sigma^2} {n_i})\quad i=1,2,...,a$$
hvor $\bar X_i$ er population-wise [[#Notation og sample means|sample mean]].

$$\widehat \sigma^2=S^2_W=\frac {SS_W}{N-a}$$
Vi bruger $SS_W$ da, hvis vi kigger på dens [[#SS (sum of squares) decomposition|udregninger]], kan vi se, at den gør brug af population wise sample mean samt datapunkter i hvert population... tror det er derfor i hvert fald.

## Hvorfor blev $H_0$ forkastet?

For at vide dette, må vi opskrive [[Confidence Intervals (CI)|konfidensintervaler]] for $\mu_i$. (for alle $a$ populationer)
$$\frac {\bar X_i - \mu_i} {\sqrt {\sigma^2 /n_i}}\sim N(0,1)\Rightarrow \frac {\bar X_i - \mu_i} {\sqrt {S_W^2 /n_i}}\sim t(N-a)$$
![[Pasted image 20261127094735.png]]

$$CI:\quad \left[\bar X_i \pm t(N-a)_{\alpha/2}\sqrt {\frac {S_W^2}{n_i}}  \right]$$
![[Pasted image 20261127094936.png]]

Vi holder så øje med hvor konfidensintervallerne ikke overlapper for at finde vores outlier. Hvis $CI$ for $\mu_3$ måske er vores nye metode, kan vi bruge det til at konkludere, om den nye metode er bedre end de gamle.

Vi kan også finde konfidensintervallet for forskellen mellem $\mu_i$ og $\mu_k$ $(\mu_i-\mu_k)$.
$$CI:\quad \left[(\bar X_i - \bar X_k)\pm t(N-a)_{\alpha/2}\sqrt{\widehat \sigma^2 \left(\frac 1 {n_i} + \frac 1 {n_k} \right)} \right]$$

Det på _højre side_ af $\pm$ er **LSD** (**L**east **S**ignificant **D**ifference).

![[Pasted image 20261127095342.png]]



