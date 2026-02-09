
---
**Date:** 2026-02-09

## Preparation

>[!TODO] HOMEWORK
>- [ ]  P. 61-69 + 72-74

> [!DANGER] EXERCISES
> - [ ] 

---
# Relevant documents
[[Lektion 2.pdf]]
[[Forstærker med negativ feedback.pdf]]
[[Opgaver 2.pdf]]
[[Forberedelse 2.pdf]]

# Topics
[[Den Ikke Ideelle Op Amp]]
[[Modkoblet forstærker]]
[[Negativ Feedback Op Amp]]

# Notes
![[Pasted image 20260209094643.png]]

Ovenstående opgave er en samling af alle dagens noter.

Da vi har en [[Modkoblet forstærker#Ikke-inverterende forstærker|ikke-inverterende forstærker]] har vi følgende værdier for $\alpha$ og $\beta$
## $$\alpha = 1\quad \beta=\frac {R_1}{R_1+R_2}=\frac {10k\Omega}{100k\Omega}=\frac {1}{10}$$
og $\alpha/\beta$ bliver
## $$\frac {\alpha}{\beta}=\frac 1{\frac {1}{10}}=10$$
Vi kigger så på formlen for closed loop gain for [[Den Ikke Ideelle Op Amp]].
## $$A_{CL}=\frac {V_o}{V_{in}}=\frac \alpha\beta\cdot \frac {A_{Ol}}{\frac 1\beta+A_{OL}}$$
Fejlen af $A_{CL}$ må ikke overstige 100 ppm.

Dermed
## $$\text{Error}=1-\frac {A_{Ol}}{\frac 1\beta+A_{OL}}$$
100 ppm er $0.0001$. Så
## $$0.0001=1-\frac {A_{OL}}{10+A_{OL}}\Leftrightarrow A_{OL}=99,990$$
# Opgaver
![[Pasted image 20260209101801.png]]

Vi har at gøre med en [[Modkoblet forstærker#Inverterende forstærker|inverterende forstærker]].
## $$\alpha = -\frac {R_2} {R_1 + R_2}\quad \beta = \frac {R_1}{R_2 + R_1}$$
Vi kan starte med at samle nogle af modstandende.

Da den positive indgang af Op Ampen er forbundet til GND, må dens spænding være 0 V.
Eftersom vi gerne vil have en forskel i spændingen på Op Ampen, må indgangsspændingen på den positive indgang også være 0 V.

## 1. Alpha
Vi betragter noden mellem $R_4$ og $V_o$ som GND og vi kan således samle $R_2$, $R_3$ og $R_4$. Set fra $V_{in}$ sidder $R_3$ og $R_4$ parallelt, og denne parallelforbindelse sidder i serie med $R_2$. Dermed bliver den samlede mostand for denne del af kredsløbet
## $$R_f=R_2+\left(\frac 1 {R_3}+\frac 1 {R_4}\right)^{-1}=1000 k\Omega+\left(\frac 1 {1000k\Omega}+\frac 1 {10.2k\Omega}\right)^{-1}=1010.1k\Omega$$

Dermed bliver $\alpha$

## $$\alpha =-\frac {R_f}{R_1+R_f}=-\frac {1010.1k\Omega}{1000k\Omega+1010.1k\Omega}=-\frac {1010.1k\Omega}{2010.1k\Omega}=-\frac {10101}{20101}$$
## 2. Beta
Vi kigger nu fra $V_ o$ i stedet for $V_{in}$. Da kan vi se to spændingsdelere koblet sammen, da vi nu betragter $V_{in}=0 V$ da den positive indgangsspænding er 0 V.

Da kan vi så se (fra $V_0$) at $R_3$ sidder i parallel med $R_1$ og $R_2$. Denne parallelforbindelse sidder i serie med $R_4$.
## $$R_{in}=\left(\frac 1 {R_3}+\frac 1{R_1+R_2}\right)^{-1}=\left(\frac 1 {10.2k\Omega}+\frac 1{1000k\Omega+1000k\Omega}\right)^{-1}=10.15k\Omega$$

Vi har nu to spændingsdelere og da vi gerne vil kende spændingen over $V_{id}$ (som er den samme som den over $R_1$) må vi skulle gange dem sammen.
Den ene spændingsdeler er over $R_4$ og parallelforbindelsen $R_3 ||(R_1+R_2)$ mens den anden spændingsdeler er over $R_1$ og $R_2$.

$\beta$ bliver så
## $$\beta = \frac {R_{in}}{R_{in}+R_4}\cdot\frac{R_1}{R_1+R_2}=$$
## 3. Gain
Da vi antager at forstærkeren er ideel, kan vi bruge formlen for gain fra en [[Modkoblet forstærker]]
## $$A_{CL}=\frac\alpha\beta=\frac {-\frac {10101}{20101}}{\frac {10000}{20101}}=\frac {-10101\cdot 20101}{10000\cdot20101}=-\frac {10101}{10000}\approx -1$$

---
#lecture 