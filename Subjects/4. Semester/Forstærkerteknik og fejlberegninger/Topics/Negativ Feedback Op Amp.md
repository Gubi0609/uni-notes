Dette er en [[Modkoblet forstærker|modkoblet forstærker]].
# Effekt af negativ feedback
![[Pasted image 20260209085441.png]]

Formlen i rød kan forlænges til _hvis det er en [[Den ideelle Op Amp|ideel Op Amp]]_.
## $$A_{CL}=\frac {V_o}{V_{in}}=\frac\alpha\beta\cdot K_f=\frac\alpha\beta=1+\frac{R_2}{R_1}$$

For [[Den ideelle Op Amp]] har vi
## $$A_{OL}\rightarrow\infty\quad R_{in}\rightarrow\infty\quad R_o\rightarrow 0\Omega$$
For [[Den Ikke Ideelle Op Amp]] gælder
## $$A_{OL}\neq \infty\quad R_{in}\neq\infty\quad R_o\neq 0\Omega$$
# Forstærkning af negativ feedback
![[Pasted image 20260209092852.png]]

Da bliver $A_f$ for dette
## $$A_f = \frac {x_o}{x_s}=\frac A {1+\beta\cdot A}=\frac 1\beta\cdot\frac 1{1+\frac 1{\beta\cdot A}}\rightarrow \frac 1\beta|_{\beta A\rightarrow\infty}$$
Her betragtes $\alpha$ (se [[Modkoblet forstærker]]) som værende $\alpha=1$ idet $x_s$ betragtes som indgangssignal.
- **A** er *Åben*sløjfeforstærknigne ($A_{OL}$]).
- **A_f** ($A_f$) er *Lukket*sløjeforstærkning ($A_{CL}$).
- $\beta A$ er *Sløjfe*forstærknigen (${\beta A}_{OL}$)
![[Pasted image 20260209093425.png]]

$\beta$ er typisk bestemt af _passive_ komponenter (e.g. **R**, **C** etc.,)

# Feedback typer
![[Pasted image 20260209093526.png]]

> [!example]- Eksempler på feedback typer
> ![[Pasted image 20260209093550.png]]

