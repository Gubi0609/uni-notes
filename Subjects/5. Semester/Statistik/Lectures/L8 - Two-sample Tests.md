
---
**Date:** 2026-11-06

## Preparation

>[!TODO] HOMEWORK
>- [ ] 

> [!DANGER] EXERCISES
> - [ ] 10.1.1 a+b, 10.2.2 a+b, 10.2.6, 10.2.11 a+b+c, 10.4.1, 10.4.3

---
# Relevant documents
[[Agenda lecture 08.pdf]]
[[Lektion 8 slides.pdf]]
[[Solutions lecture 08 v2.pdf]]

# Topics


# Notes
![[Pasted image 20261106101031.png]]

- a.
Vi får givet nul hypotesen $H_0: \quad \mu_1 = \mu_2 \Leftrightarrow \mu_1 - \mu_2 = \Delta_0, \quad \Delta_0 = 0$. Derfor kan vi bruge [[Hypotese test (2 populationer)#Case 1 Non-paired test (forskel i middelværdier) med _kendt_ varians|Non-paired test med kendt varians]] da vi også får givet variansen.

Vi starter med at ville estimere $\mu_1$ og $\mu_2$. Samtidigt finder vi også forskellen i gennemsnittende $\bar x_1$ og $\bar x_2$.
Til dette bruger vi følgende ligninger:

$$\hat\mu_1=\bar X_1 = \frac 1 n \sum_{i=1}^{n_1} x_{1i}\sim N(\mu_1, \sigma_1^2)$$
$$\hat\mu_2=\bar X_2 = \frac 1 n \sum_{i=1}^{n_2} x_{2i}\sim N(\mu_2, \sigma_2^2)$$
$$(\bar x_1-\bar x_2)\sim N(\mu_1-\mu_2, \frac {\sigma_1^2} {n_1} + \frac {\sigma_2^2} {n_2})$$

Dernæst opstiller vi vores test statistic og indsætter $H_0$ for at få $z_0$:
$$Z_0:= \frac {(\bar X_1 - \bar X_2)-(\mu_1-\mu_2)}{\sqrt{\frac {\sigma_1^2}{n_1}+\frac {\sigma_2^2}{n_2}}}=^{H_0}\frac {(\bar X_1 - \bar X_2)-\Delta_0}{\sqrt{\frac {\sigma_1^2}{n_1}+\frac {\sigma_2^2}{n_2}}}\sim N(0,1)$$

Og til sidst kan vi finde $p-værdien$:
$$p=2P(Z>|z_0|)=2(1-P(Z<|z_0|))$$

Alt dette blev gjort i MATLAB:
```matlab
%% 10.1.1
clear; clc; close all;

sigma1 = 10;
sigma2 = 5;

n1 = 10;
n2 = 15;

bar_x1 = 4.7;
bar_x2 = 7.8;

alpha = 0.05;

delta0 = 0;

% Estimate mu1 and mu2
hat_mu1 = bar_x1;
hat_mu2 = bar_x2;

% Diff in normal distributions
diff_x1_x2 = bar_x1 - bar_x2;

% Test statistic
Z0 = (diff_x1_x2 - delta0)/(sqrt(sigma1^2/n1 + sigma2^2/n2));

% p-value
p = 2*(1-normcdf(abs(Z0)))
```

Med resultatet
$$p=0.3641$$

Da $p>>\alpha$ kan vi _acceptere $H_0$_ ([[Hypotese test (1 population)#P-værdi (alternativ til en valgt $ alpha$)|p-værdi]])

- b.
Hvis vi ville gøre det med et confidens interval i stedet kunne vi bruger formlen:
$$CI:\quad \left[(\bar X_1 - \bar X_2)\pm z_{\alpha/2}\sqrt{\frac {\sigma_1^2}{n_1} + \frac {\sigma_2^2}{n_2}}\right]$$

og tjekke om $\Delta_0 = 0$ falder inden for dette område.

```matlab
% Confidence Interval
z_alpha2 = norminv(1 - alpha/2);
CI_low = diff_x1_x2 - z_alpha2*sqrt(sigma1^2/n1 + sigma2^2/n2);
CI_up = diff_x1_x2 + z_alpha2*sqrt(sigma1^2/n1 + sigma2^2/n2);

CI = [CI_low, CI_up]
```

$\Delta_0=0$
$CI:\quad \left[-9.7946, 3.5946\right]$

Eftersom $\Delta_0$ ligger i $CI$ kan vi acceptere $H_0$.

![[Pasted image 20261106101050.png]]

- a.
Vi får givet nul hypotesen $H_0: \quad \mu_1 = \mu_2 \Leftrightarrow \mu_1 - \mu_2 = \Delta_0, \quad \Delta_0 = 0$. Eftersom $\sigma_1^2 =\sigma_2^2$ er ukendt, kan vi bruge [[Hypotese test (2 populationer)#Case 2 Non-paired test (forskel i middelværdi) med _ukendt men ens_ varians|Non-paired med ukendt varians]].

Vi kender allerede estimaterne $s_1^2$ og $s_2^2$, så vi kan starte med at poole dem for at finde $S_P^2$ og 
derefter $S_P=\sqrt {S_P^2}$.
$$S_P^2=\frac {(n_1-1)S^2_1 + (n_2 - 1) S_2^2}{n_1 + n_2 - 2}\sim \frac {\sigma^2}{n_1 + n_2 - 2}\mathcal X^2(n_1 + n_2 - 2)$$

Vi kan bruge dette til at finde vores test statistic, som er en _student t fordeling_
$${T_0:=\frac {(\bar X_1 - \bar X_2)-\Delta_0}{S_P\sqrt{\frac 1 {n_1} + \frac 1 {n_2}}}\sim t(n_1+n_2-2)}$$
Til sidst kan vi finde p-værdien
$$p=2P(t(n_1+n_2-2)>|t_0|)=2(1-P(t(n_1+n_2-2)\leq |t_0|))$$

Gjort i MATLAB får vi
```matlab
%% 10.2.2
clear; clc; close all;

n1 = 15;
n2 = 15;

bar_x1 = 4.7;
bar_x2 = 7.8;

s1_2 = 4;
s2_2 = 6.25;

alpha = 0.05;
delta0 = 0;

% Pool s
SP_2 = ((n1-1)*s1_2 + (n2 - 1)*s2_2)/(n1 + n2 - 2);
SP = sqrt(SP_2);

% Student T distribution
T0 = (bar_x1 - bar_x2 - delta0)/(SP*sqrt(1/n1+1/n2));

% p-value
p = 2*(1- tcdf(abs(T0), n1 + n2 - 2))
```

hvor $p=8.1775\cdot 10^{-4}$.

Eftersom $p<<\alpha$ kan vi _forkaste_ $H_0$. ([[Hypotese test (1 population)#P-værdi (alternativ til en valgt $ alpha$)|p-værdi]])

- b.
Vi kan opstille CI
$$CI:\quad \left[(\bar X_1 - \bar X_2)\pm t(n_1+n_2-2)_{\alpha/2} S_P\sqrt{\frac 1 {n_1} + \frac 1 {n_2}}\right]$$
Og tjekke om $\Delta_0 = 0$ ligger i intervallet.
```matlab
% Confidence Interval
t_alpha2 = tinv(1-alpha/2, n1 + n2 - 2);
CI_low = bar_x1 - bar_x2 - t_alpha2*SP*sqrt(1/n1 + 1/n2);
CI_up = bar_x1 - bar_x2 + t_alpha2*SP*sqrt(1/n1 + 1/n2);

CI = [CI_low, CI_up]
```

$CI: \left[-4.7933, -1.4067\right]$

Eftersom $\Delta_0 \notin CI$ kan vi _forkaste_ $H_0$.


![[Pasted image 20261106101100.png]]
![[Pasted image 20261106101114.png]]

- a.
Vi opstiller hypoteserne
$$H_0:\quad \mu_1-\mu_2 <0,\quad H_1:\quad \mu_1 - \mu_2\leq \Delta_0,\quad \Delta_0 <0$$

![[Pasted image 20261106101209.png]]



![[Pasted image 20261106101225.png]]



![[Pasted image 20261106101240.png]]



---
#lecture 