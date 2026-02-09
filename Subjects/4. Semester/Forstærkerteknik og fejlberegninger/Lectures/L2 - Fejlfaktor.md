
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
## $$\alpha = \frac {R_2} {R_1 + R_2}\quad \beta = \frac {R_1}{R_2 + R_1}$$
Vi kan starte med at samle nogle af modstandende.

Da den positive indgang af Op Ampen er forbundet til GND, må dens spænding være 0 V.
Eftersom vi gerne vil have en forskel i spændingen på Op Ampen, må indgangsspændingen på den positive indgang også være 0 V.

Derfor kan noden mellem $R_1$ og $R_2$ betragtes som $R_2$'s GND og vi kan således samle $R_2$, $R_3$ og $R_4$. Set fra $R_4$ sidder $R_2$ og $R_3$ parallelt, og denne parallelforbindelse sidder i serie med $R_4$. Dermed bliver den samlede mostand for denne del af kredsløbet
## $$R_f=R_4+(\frac 1 $$

## 1.



---
#lecture 