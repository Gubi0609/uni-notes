
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

---
#lecture 