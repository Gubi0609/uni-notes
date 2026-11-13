
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
[[Simple Linear Regression (SLR)]]

# Notes
![[Pasted image 20261113101217.png]]

- a.
Vi skal bruge formlerne
$$\boxed{\hat\beta_1=\frac {\sum_{i=1}^nx_iY_i-n\bar x\bar Y}{\sum_{i=1}^nx_i^2-n\bar x^2}=\frac {\sum_{i=1}^n(x_i-\bar x)(Y_i-\bar Y)}{\sum_{i=1}^n(x_i-\bar x)^2}=\frac {S_{xY}}{S_{xx}}}$$
og
$$\boxed{\hat \beta_0=\bar Y-\hat\beta_1\bar x}$$

Til dette skal vi bruge mean af $x$ og $y$.
Efter det, starter vi med at finde $\hat  \beta_1$. Ledet $S_{xx}$ kan omskrives til
$$\sum_{i=1}^nx_i^2-n\bar x^2=\sum_{i=1}^nx_i^2-n\left(\frac{\sum x_i}{n}\right)^2=\sum_{i=1}^nx_i^2-\frac {(\sum x_i)^2}{n}$$
$S_{xy}$ skal også omskrives.
Det kan vi gøre lidt på samme måde, ved at gøre brug af hvordan $\bar x$ og $\bar y$ findes.
$$\sum_{i=1}^nx_iy_i-n\bar x\bar y=\sum_{i=1}^nx_iy_i-n\left(\frac {\sum x_i}{n}\frac{\sum y_i}{n}\right)=\sum_{i=1}^nx_iy_i-\frac {\sum x_i\sum y_i} n$$

Disse omskrivelser kan også ses i bogen som ligning [[Applied Statistics and Probability for Engineers, 7th .pdf#page=304|11.10 og 11.11]]

Vi kan så gøre alt dette i matlab og plotte til sidst
```matlab
%% 11.2.1
clear; clc; close all;

sum_x = 6322.28;
sum_x_squared = 162674.18;

sum_y = 4757.90;
sum_y_squared = 107679.27;

sum_xy = 125471.10;

n = 250;

% calculate means
bar_x = sum_x / n;
bar_y = sum_y / n;

% S_xx and S_xy
S_xx = sum_x_squared - (sum_x)^2/n;

S_xy = sum_xy - (sum_x*sum_y)/n;

% calculate hat_beta_1
hat_beta_1 = S_xy/S_xx

% calculate hat_beta_0
hat_beta_0 = bar_y - hat_beta_1*bar_x

% Define hat Y
hat_Y = @(x) hat_beta_1*x + hat_beta_0;

% Plot the linear regression model
fplot(hat_Y, [0, 50])
hold on
xlabel("BMI")
ylabel("Body fat %")
```

![[Pasted image 20261113110635.png]]

```
hat_beta_1 =
    1.8456

hat_beta_0 =
  -27.6429
```

- b.
Vi indsætter simpelthen bare en BMI på 30 i vores $\hat Y$ og observerer resultatet.

```matlab
hat_Y(30)
```

```
ans =
   27.7262
```

- c.
Residual er fejlen mellem observeret resultat og det man får ved lineær regression:
$$\hat \varepsilon_i=Y_i-\hat Y_i$$

Vi udregner det i matlab igen
```matlab
res = 25 - hat_Y(25)
```

```
res =
    6.5020
```

- d.
Det må have været et _underestimat_, siden den aktuelle værdi minus den estimerede værdi er positiv, er den **estimerede værdi altså lavere** end den aktuelle. 

![[Pasted image 20261113101234.png]]

- a.
Til meget af dette, kan vi bruge samme fremgangsmetode som i forrige opgave:
Vi skal bruge formlerne
$$\boxed{\hat\beta_1=\frac {\sum_{i=1}^nx_iY_i-n\bar x\bar Y}{\sum_{i=1}^nx_i^2-n\bar x^2}=\frac {\sum_{i=1}^n(x_i-\bar x)(Y_i-\bar Y)}{\sum_{i=1}^n(x_i-\bar x)^2}=\frac {S_{xY}}{S_{xx}}}$$
og
$$\boxed{\hat \beta_0=\bar Y-\hat\beta_1\bar x}$$

Til dette skal vi bruge mean af $x$ og $y$.
Efter det, starter vi med at finde $\hat  \beta_1$. Ledet $S_{xx}$ kan omskrives til
$$\sum_{i=1}^nx_i^2-n\bar x^2=\sum_{i=1}^nx_i^2-n\left(\frac{\sum x_i}{n}\right)^2=\sum_{i=1}^nx_i^2-\frac {(\sum x_i)^2}{n}$$
$S_{xy}$ skal også omskrives.
Det kan vi gøre lidt på samme måde, ved at gøre brug af hvordan $\bar x$ og $\bar y$ findes.
$$\sum_{i=1}^nx_iy_i-n\bar x\bar y=\sum_{i=1}^nx_iy_i-n\left(\frac {\sum x_i}{n}\frac{\sum y_i}{n}\right)=\sum_{i=1}^nx_iy_i-\frac {\sum x_i\sum y_i} n$$

Disse omskrivelser kan også ses i bogen som ligning [[Applied Statistics and Probability for Engineers, 7th .pdf#page=304|11.10 og 11.11]]

Estimationen af $\sigma^2$ finder vi ved
$$\hat\sigma^2=\frac 1 {n-2} \sum_{i=1}^n \hat\varepsilon_i^2=\frac {SSE}{n-2}$$
SSE findes ved
$$SSE=SST-\hat\beta_1 S_{xY}$$
hvor SST er
$$SST=\sum_{i=1}^n(Y_i-\bar Y)^2=\sum_{i=1}^ny_i^2-n\bar y^2=\sum_{i=1}^ny_i^2-\frac {(\sum y_i)^2}{n}$$

Vi gør alt det her i MATLAB
```matlab
%% 11.2.3
clear; clc; close all;

sum_x = 43;
sum_x_squared = 157.42;

sum_y = 572;
sum_y_squared = 23530;

sum_xy = 1697.80;

n = 14;

% calculate means
bar_x = sum_x / n;
bar_y = sum_y / n;

% S_xx and S_xy
S_xx = sum_x_squared - (sum_x)^2/n;

S_xy = sum_xy - (sum_x*sum_y)/n;

% calculate hat_beta_1
hat_beta_1 = S_xy/S_xx

% calculate hat_beta_0
hat_beta_0 = bar_y - hat_beta_1*bar_x

% Define hat Y
hat_Y = @(x) hat_beta_1*x + hat_beta_0;

% find sigma^2
SST = sum_y_squared - (sum_y)^2/n;
SSE = SST - hat_beta_1*S_xy;

sigma_squared = SSE/(n-2)

fplot(hat_Y, [0, 100])
hold on
xlabel("Compressive strength")
ylabel("Intrinsic permeability")
```

```
hat_beta_1 =
   -2.3298


hat_beta_0 =
   48.0130


sigma_squared =
    1.8436
```

![[Pasted image 20261113113624.png]]

- b.
Det gøres bare i MATLAB
```matlab
hat_Y(4.3)
```

```
37.9948
```

- c.
Bare det samme igen...
```matlab
hat_Y(3.7)
```

```
39.3927
```

- d.
Vi bruger formlen for residual
$$\hat \varepsilon_i=Y_i-\hat Y_i$$

og gør det i matlab
```matlab
res = 46.1 - hat_Y(3.7)
```

```
res =
    6.7073
```

![[Pasted image 20261113101247.png]]

- a.
![[Pasted image 20261113114437.png]]

Jeg vurderer at det godt kan fungere med SLR her, da datapunkterne allerede danner en nogenlunde lineær linje med en hvis spredning.
```matlab
%% 11.2.6
clear; clc; close all;

y = [4.4, 6.6, 9.7, 10.6, 10.8, 10.9, 11.8, 12.1, 14.3, 14.7, 15.0, 17.3, 19.2, 23.1, 27.4, 27.7, 31.8, 39.5]
x = [0.19, 0.15, 0.57, 0.70, 0.67, 0.63, 0.47, 0.70, 0.60, 0.78, 0.81, 0.78, 0.69, 1.3, 1.05, 1.06, 1.74, 1.62]

plot(x, y, "*r")
hold on
xlabel("Roadway area in watershed")
ylabel("Chloride concentration (mg/L)")
hold off
```

- b.
Samme fremgangsmetode som før.

Vi skal bruge formlerne
$$\boxed{\hat\beta_1=\frac {\sum_{i=1}^nx_iY_i-n\bar x\bar Y}{\sum_{i=1}^nx_i^2-n\bar x^2}=\frac {\sum_{i=1}^n(x_i-\bar x)(Y_i-\bar Y)}{\sum_{i=1}^n(x_i-\bar x)^2}=\frac {S_{xY}}{S_{xx}}}$$
og
$$\boxed{\hat \beta_0=\bar Y-\hat\beta_1\bar x}$$

Til dette skal vi bruge mean af $x$ og $y$.
Efter det, starter vi med at finde $\hat  \beta_1$. Ledet $S_{xx}$ kan omskrives til
$$\sum_{i=1}^nx_i^2-n\bar x^2=\sum_{i=1}^nx_i^2-n\left(\frac{\sum x_i}{n}\right)^2=\sum_{i=1}^nx_i^2-\frac {(\sum x_i)^2}{n}$$
$S_{xy}$ skal også omskrives.
Det kan vi gøre lidt på samme måde, ved at gøre brug af hvordan $\bar x$ og $\bar y$ findes.
$$\sum_{i=1}^nx_iy_i-n\bar x\bar y=\sum_{i=1}^nx_iy_i-n\left(\frac {\sum x_i}{n}\frac{\sum y_i}{n}\right)=\sum_{i=1}^nx_iy_i-\frac {\sum x_i\sum y_i} n$$

Disse omskrivelser kan også ses i bogen som ligning [[Applied Statistics and Probability for Engineers, 7th .pdf#page=304|11.10 og 11.11]]

Estimationen af $\sigma^2$ finder vi ved
$$\hat\sigma^2=\frac 1 {n-2} \sum_{i=1}^n \hat\varepsilon_i^2=\frac {SSE}{n-2}$$
SSE findes ved
$$SSE=SST-\hat\beta_1 S_{xY}$$
hvor SST er
$$SST=\sum_{i=1}^n(Y_i-\bar Y)^2=\sum_{i=1}^ny_i^2-n\bar y^2=\sum_{i=1}^ny_i^2-\frac {(\sum y_i)^2}{n}$$

Vi gør alt det her i MATLAB


![[Pasted image 20261113101303.png]]

![[Pasted image 20261113101322.png]]

![[Pasted image 20261113101340.png]]

![[Pasted image 20261113101356.png]]

![[Pasted image 20261113101405.png]]


---
#lecture 