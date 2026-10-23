
---
**Date:** YYYY-MM-DD

## Preparation

>[!TODO] HOMEWORK
>- [ ] 

> [!DANGER] EXERCISES
> - [ ] 

---

# Relevant documents
[[Agenda lecture 07.pdf]]
[[Lektion 7 slides.pdf]]
[[Solutions lecture 07 v3.pdf]]

# Topics


# Notes

# Hypotese test (1 population)

## Case 1: Normalfordelt data
Vi har $X \sim N(\mu, \sigma^2)$.
Vi vil gerne teste for middelværdien $\mu$
- $\sigma^2$ er ukendt

Model: $x_1, ..., x_n$, uafhængige. Kommer fra en normalfordeling $X_i\sim N(\mu,\sigma^2)$
- Observation: $x_1, ..., x_n$ (data)

Vi opstiller en _nul-hypotese_ $H_0$.
$$H_0:\quad \mu = \mu_0$$
Vi gætter på at middelværdien har en specificeret værdi på $\mu_0$.
Hvis $H_0$ ikke gælder, må man tro på en _alternativ hypotese_ $H_1$
$$H_1: \quad \mu \neq \mu_0$$
Dette er **to-sidet**. ==Jeg tro at det er fordi det enten er ligmed eller ikke-ligmed==.

### 1-sidet
Vi opstiller en nul-hypotese
$$H_0:\quad \mu \leq \mu_0$$

Og til dette en alternativ hypotese
$$H_1:\quad \mu > \mu_0$$

**Formålet** med disse hypoteswer er at tage vores _data_ og lave en _test_ som fører til en _konklusion_.
Ud fra testen kan vi konkludere om enten $H_0$ (_ikke signifikant_) eller $H_1$ (_signifikant_) gælder.
- Hvis $H_1$ gælder forkaster vi $H_0$ og må så ændre vores antagelser om systemet. Derfor er det signifikant, da vores antagelser så ikke gælder længere.

### Estimat, $\hat \mu$
Estimatet $\hat \mu$ skrives
$$\hat \mu = \bar X = \frac 1 n \sum_{i=1}^n x_i \sim N\left(\mu, \frac {\sigma^2} n\right)$$
Vi vil gerne opstille det som en standard normalfordeling, da PDF'en så er nemmere at tegne. Vi opstiller derfor en test statistic
#### Test statistic
$$Z_0:=\frac {\bar X - \mu} {\sigma/\sqrt n}=^{H_0} \frac {\bar X - \mu_0} {\sigma /\sqrt n}\sim N(0,1)$$
Dataen bliver så $Z_0 = z_0$.
Hvis $Z_0$ er et lille tal, altså at forskellen mellem $\bar X$ og $\mu_0$ er lille, tror vi på $H_0$. Hvis forskellen derimod er stor, forkaster vi $H_0$ og tror i stedet på $H_1$.

Vi har til dette et _accept område_ $A$ og et _kritisk område_ $C$.
Til dette gælder
- $z_0 \in A\rightarrow$ vi _accepterer_ $H_0$.
- $z_0 \in C \rightarrow$ vi _forkaster_ $H_0$.

#### To sidet kritisk område
![[Pasted image 20261023083726.png|467]]

#### Et sidet kritisk område
![[Pasted image 20261023083929.png|464]]

Som vi kan se, kan accept området ligge forskelligt an på hvad $H_0$ er.
Der er lidt fejl på tegningen... Det skulle selvfølgelig være
$$H_0:\quad \mu\leq \mu_0$$
og omvendt for den nederste.


### Fejl typer

|                | $H_0$ sand   | $H_0$ falsk  |
| -------------- | ------------ | ------------ |
| Accepter $H_0$ | _Ingen fejl_ | Type 2 fejl  |
| Forkast $H_0$  | Type 1 fejl  | _Ingen fejl_ |

Type 1 fejl er den **mest alvorlige**, fordi vi da laver et _forkert stærkt udsagn_.

For at sørge for at vores fejl ikke er for stor, laver vi et **signifikansniveau** $\alpha$.
$\alpha$ er typisk $1\%$, $5\%$, eller $10\%$. Den mest normale er $5\%$.
$$\alpha :=\text{max acceptable }P(\text{Type 1 error})$$

På den her måde laver vi højest $\alpha$ procent af gangene en Type 1 fejl.
## Fra signifikansniveau til accept og kritisk område

### To-sidet test
![[Pasted image 20261023085427.png|694]]

For de typiske værdier af $\alpha$ (1%, 5%, 10%), er $z_{\alpha/2}:
$$\alpha = 1\% \rightarrow z_{\alpha/2}=2.58$$
$$\alpha = 5\% \rightarrow z_{\alpha/2}=1.96$$
$$\alpha = 10\% \rightarrow z_{\alpha/2}=1.65$$

Ud fra ovenstående tegning af vores _test statistic PDF_ kan vi sige
$$C:\quad |z_0|>z_{\alpha/2}\Rightarrow \text{forkast }H_0$$
$$A:\quad |z_0|\leq z_{\alpha/2}\Rightarrow \text{accepter }H_0$$

### Et-sidet test
![[Pasted image 20261023090030.png|703]]

Ud fra vores _test statistic PDF_ ovenover, kan vi sige
$$C:\quad z_0 > z_\alpha \Rightarrow \text{forkast }H_0$$
$$A:\quad z_0\leq z_\alpha \Rightarrow \text{accepter }H_0$$

Vi kan også tegne en omvendt PDF (bare spejlvend den) hvor der så gælder
$$C:\quad z_0 < -z_\alpha \Rightarrow \text{forkast }H_0$$
$$A:\quad z_0\geq -z_\alpha \Rightarrow \text{accepter }H_0$$
Der skal vi også omvende formlen for $z_\alpha$ fra tegningen:
$$z_{1-\alpha}=-z_\alpha\rightarrow \text{norminv}(\alpha)$$
### Type 2 fejl
Hvis vi istedet for at kigge på type 1 fejl, vil kigge på type 2 fejl bruger vi $\beta$
$$\beta=\beta(\mu)=P(z_0\in A|H_0 \text{ falsk})$$
Det er vigtigt her at sige, at dette _ikke_ giver et tal, men er en _funktion af den sande_ $\mu$.

### Power
Nogle gange bruger vi en _power_
$$\gamma = \gamma(\mu)=1-\beta(\mu)=P(z_0\in C |H_0 \text{ falsk})$$
Ligesom $\beta$ er dette _ikke et tal_ men en funktion af den sande $\mu$.


## P-værdi (alternativ til en valgt $\alpha$)

### 2-sidet
Beregn $z_0$
![[Pasted image 20261023093827.png|509]]

$$p/2=P(Z>|z_0|)\rightarrow p=2(1-P(Z\leq |z_0|))=2(1-\Phi(|z_0|))$$
Hvis $p$ er _lille_ **forkaster** vi $H_0$.
Hvis $p$ er _stor_ **accepterer** vi $H_0$.

Eksemperl: $p=3\%$
- $\alpha = 5\% \Rightarrow \text{forkast }H_0$
- $\alpha = 1\% \Rightarrow \text{accepter }H_0$

> p-værdien er _sandsynligheden_ for at en værdi af _test statistic_ (af dataen) er **mindst lige så sjælden som den beregnede** for dataen, _**givet at $H_0$ er sand**_.

### 1-sidet test
$$H_0:\quad \mu\leq \mu_0$$
$$H_1:\quad \mu >\mu_0$$
Fra test statistic PDF
$$p=P(Z>z_0)\rightarrow p=1-P(Z\leq z_0)=1-\Phi(z_0)$$

For omvendt, er det det samme bare uden $1-$.


## Case 2: Normalfordelt data, ukendt $\mu$
Vi har normalfordelt data $X\sim N(\mu,\sigma^2)$.
- Vi _tester_ for $\mu$ som er ukendt
- $\sigma^2$ er også ukendt.

### Test statistic
$$Z_0=\frac {\bar X-\mu_0}{\sigma/\sqrt n}\sim N(0,1)$$



---
#lecture 