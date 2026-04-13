
---
**Date:** 2026-04-13

## Preparation

>[!TODO] HOMEWORK
>- [ ] 

> [!DANGER] EXERCISES
> - [ ] 

---
# Relevant documents


# Topics


# Notes
Krav:
* Motor: RS PRO 238-9715
* Måle Område: 0 – 240 g\*cm
* Udgangs Signal: 0 – 10V (lineært svarende til Torque området)
* Nøjagtighed: ± 1 g\*cm
* Motor Forsyning: op til 12V
* Måle Modstand: 100 mOhm
* Afstand fra Målemodstand til jeres kredsløb: 20-30cm

Systemet skal kunne angive aktuel Torque samt aktivere en over Torque protection sådan at overstiger Torque, 150 g\*cm, så skal en højtaler aktivers.

$$E_{rr}=\frac 1 {240} \cdot 100=0.417\%$$
$$I_{LOAD, min}=0A\quad , \quad I_{LOAD,max}=2.64 A$$
$$f_{sense}=1000 Hz$$
$$R_{SHUNT}=100 m\Omega$$
$$V_{O,max}=10 V$$
$$\Delta V_{SHUNT, max} =0.1\Omega\cdot 2.64A=0.264V$$
$$Gain=\frac {10 V}{0.264 V} = 37.879$$
$$R_2 = {Gain}\cdot{R_1}=37.879 \cdot1000\Omega=37879\Omega=37.879k\Omega$$
$$V_{\textrm{OS}} =\frac{100417\,I_{\textrm{load}} \,R_2 \,R_{11} \,R_{\textrm{shunt}} -100000\,I_{\textrm{load}} \,R_1 \,R_{21} \,R_{\textrm{shunt1}} }{100000\,R_1 \,R_{11} +100000\,R_1 \,R_{21} }$$
Where $R_{11}$, $R_{21}$, and $R_{shunt1}$ denote the tolerance of each corresponding resistor times the resistance ([[low_side_current_sense_circuit_design.pdf#page=4|See tutorial document page 4]]) 
$$C_1=\frac 1 {2\pi\cdot f_{sense}\cdot 10\cdot R_2}=\frac 1 {2\pi\cdot 1000Hz\cdot 10\cdot 37879\Omega}=$$

---
#lecture 