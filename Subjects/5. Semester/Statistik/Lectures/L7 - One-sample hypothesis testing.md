
---
**Date:** 2026-10-23

## Preparation

>[!TODO] HOMEWORK
>- [ ] 

> [!DANGER] EXERCISES
> - [ ] 9.2.2, 9.2.3, 9.2.4, 9.2.6a, 9.2.7, 9.3.1, 9.3.7, 9.4.1, 9.4.3, 9.5.2

---

# Relevant documents
[[Agenda lecture 07.pdf]]
[[Lektion 7 slides.pdf]]
[[Solutions lecture 07 v3.pdf]]

# Topics


# Notes
![[Pasted image 20261023102927.png]]

Signifikans niveau: $\alpha$
$H_0:\quad \mu=5$
$H_1:\quad \mu<5$

Ud fra vores hypoteser, kan vi opstille områderne

$$C:\quad z_0 < z_\alpha \Rightarrow \text{forkast }H_0$$
$$A:\quad z_0= z_\alpha \Rightarrow \text{accepter }H_0$$
Hvor
$$z_\alpha\rightarrow \text{norminv}(\alpha)$$

Dette kan vi gøre da $\sigma^2$ er _kendt_, hvilket betyder at $Z_0$ følger normalfordelingen. Derfor kan vi løse problemet ved at bruge _standard normal fordelingen_. Ud fra hypotesen kan vi se at det er en _lower one-sided test_ altså kan vi opstille de områder vi har gjort ovenfor.

```matlab
>> norminv(0.01)

ans =

   -2.3263

>> norminv(0.05)

ans =

   -1.6449

>> norminv(0.10)

ans =

   -1.2816
```


![[Pasted image 20261023102942.png]]

- a.
Fra [[Kontinuerte stokastiske variable & fordelinger#Central Limit Theorem|Central Limit Theorem (CLT)]] ved vi at for et stort antal sampels $n$, kan gennemsnittet $\bar X$ approximeres som normalfordelt
$$\bar X\sim N\left(\mu, \frac {\sigma^2} n\right)$$
Hvilket betyder at vi kan finde vores standard afvigelse $s$ fra SE mean (_Standard Error mean_ eller _Standard Deviation of the mean_)
$$\text{SE mean}=\frac s {\sqrt N}\Rightarrow s=\text {SE mean}\cdot \sqrt N=0.7495$$

Vi har ukendt varians, så vi kan bruge [[Hypotese test (1 population)#Case 2 Normalfordelt data, ukendt $ sigma 2$|Case 2: Ukendt Varians]] til at opstille vores test statistic
$$T_0:=\frac {\bar X-\mu_0}{s/\sqrt n}=-0.4684$$
Vi har en _upper-tailed one sided test_ da $H_1:\quad \mu>20$.
Så kan vi få p-værdien ved (se [[Lektion 7 slides.pdf#page=6|slides]])
$$p=(1-P(t(n-1)\leq t_0))$$
$P(t(n-1)\leq t_0)$ kan fås ved `tcdf(t_0, n-1)`.
Så er p-værdien
$$p=0.6747$$
Så har vi altså de manglende parametre:
SE Mean: $0.7495$
Z: $T_0=-0.4684$
P: $0.6747$

```matlab
%% 9.2.3
N = 10;
Mean = 19.889;
SEMean = 0.237;
mu0 = 20;

% Assumed standard deviation
s = SEMean * sqrt(N) % 0.7495

% Test statistic: Unknown variance (Case 2)
T_0 = (Mean - mu0)/(s/sqrt(N)) % -0.4684

% p-value
p = 1 - tcdf(T_0, N-1) % 0.6747
```


- b.
Det er en _et-sidet_ test da hypoteserne er
$H_0: \quad \mu=20$
$H_1: \quad \mu>20$

$H_1$ er den afgørende faktor. Hvis $H_1:\quad \mu \neq 20$ ville det være en to-sidet.

- c.
Vi kan bruge [[Confidence Intervals (CI)#Case 2 Normalfordeling, $ sigma 2$ ukendt|CI, Case 2: Normalfordeling, varians ukendt]].
$$CI: \quad \left[\bar X \pm t(n-1)_{\alpha/2}\cdot \frac S {\sqrt n}\right]$$
Hvor $t(n-1)_{\alpha/2}$ findes med `tinv(1 - alpha/2, n-1)`.

Via Matlab får vi så
$$CI:\quad \left[19.3529,\quad 20.4251\right]$$

```matlab
% Fortsættelse af matlab-blokken ovenover
% c

alpha = 0.05; % 95% confidence level

% Find t(n-1)_alpha/2
t_alpha_2 = tinv(1-alpha/2, N - 1) % 2.2622
t_alpha_2_neg = -t_alpha_2 % -2.2622

C_low = Mean - t_alpha_2 * s/sqrt(N) % 19.3529
C_up = Mean + t_alpha_2 * s/sqrt(N) % 20.4251
```

- d.
Hvis $H_1:\quad \mu \neq 20$ har vi istedet en to-sidet test.
Da kan p-værdien beregnes som

$$p=2P(t(n-1)>|t_0|)=2(1-P(t(n-1)\leq |t_0|))$$
$P(t(n-1)\leq |t_0|)$ kan fås ved `tcdf(|t_0|, n-1)`.
Så bliver p-værdien
$$p=0.6507$$
```matlab
% Fortsættelse af matlab-blokken ovenover
% d

p_two_sided = 2*(1-tcdf(abs(T_0), N-1)) % 0.6507
```


![[Pasted image 20261023102955.png]]

Da vi har $H_0:\quad \mu = 10$ og $H_1:\quad \mu > 10$ har vi en _one-sided, upper tailed_ test.
- Varians er kendt

Ud fra alt dette kan vi bruge [[Hypotese test (1 population)#1-sidet test|p-værdi for 1-sidet test]].
$$p=P(Z>z_0)\rightarrow p=1-P(Z\leq z_0)=1-\Phi(z_0)$$
Vi kan finde $\Phi(z_0)$ i MATLAB ved at bruge `normcdf(z_0)`.

Alle opgaverne løses så i matlab

```matlab
%% 9.2.4
clc; clear; close all;

z0_1 = 2.05;
z0_2 = -1.84;
z0_3 = 0.4;

p1 = 1 - normcdf(z0_1) % 0.0202
p2 = 1 - normcdf(z0_2) % 0.9671
p3 = 1 - normcdf(z0_3) % 0.3446
```


![[Pasted image 20261023103006.png]]

Siden $H_0:\quad \mu=3$ og $H_1:\quad \mu\neq 3$ er det en _to-sidet_ test.
Varians $\sigma=0.9$ er kendt.
Vi ved også at dataen er normal fordelt.
Vi ved også at $\alpha = 0.05$.

Derfor kan vi bruge [[Hypotese test (1 population)#Test statistic|Case 1: Kendt varians, Test statistic]]
$$Z_0:=\frac {\bar X - \mu} {\sigma/\sqrt n}=^{H_0} \frac {\bar X - \mu_0} {\sigma /\sqrt n}\sim N(0,1)$$
Vi vil også finde $z_{\alpha/2}$



![[Pasted image 20261023103014.png]]

![[Pasted image 20261023103028.png]]

![[Pasted image 20261023103048.png]]
![[Pasted image 20261023103059.png]]

![[Pasted image 20261023103112.png]]

![[Pasted image 20261023103124.png]]
![[Pasted image 20261023103136.png]]

![[Pasted image 20261023103157.png]]

---
#lecture 