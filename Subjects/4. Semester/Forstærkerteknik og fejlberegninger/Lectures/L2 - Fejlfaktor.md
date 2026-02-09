
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
## $$0.0001=1-\frac {A_{OL}}{10+A_{OL}}\Leftrightarrow$$

---
#lecture 