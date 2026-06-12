- Regulatorens virkemåde
- Stabilitet
- Anti-windup
- Referencefølge og stationær fejl

[[L3 - Introduction to Control]]
- Åben og lukket sløjfe regulering
- Stabilitet i feedback
- Stationær fejl (steady state tracking)
- Sensitivitetanalyse
- Linearisering og cascade control
 [[L4 - Design of PID Controllers]]
- Regulatorens virkemåde (P, PI, PD, PID)
- Referencefølge og stationær fejl
- Tuning af PID (Zeigler-Nichols bl.a.)
 [[L2 - Stability and Performance Analysis]]
 - Stabilitet
 [[L7 - Dynamic Compensators and Stability Margins]]
 - Anti windup (back-calculation og conditional integration)
 - Steady-State tracking med type 0/1/2 systemer
 - Lead og lag kompensation
[[L11 - Optimal Control]]
- Fortsættelse af anti-windup i forbindelse med tilstandregulering.


# Regulatorens virkemåde (PID)
Has three terms,P, I, D
## $$u(t)=K_pe(t)+K_i\int_{t_0}^{t_0}e(\tau)\, d\tau+K_d\frac {de(t)}{dt}\rightarrow K(s)=K_p\left(1+\frac 1 {sT_i}+sT_d\right)$$
where $K_p$ is the proportional gain, $K_i$ is the integral gain, $K_d$ is the derivative gain.
If we instead want it in the frequency domain, we still use the proportional gain, but now with the integral time constant (how far to look _back_) and the derivative time constant (how far to look _forward_).


It can also be implemented with noise reduction on the derivative term
## $$T_{ue}(s)=K_p\left(N-\frac N {1+sT_d/N}\right)=K_p\frac {sT_d}{1+sT_d/N}$$
![[Pasted image 20260610150811.png]]

This is done, as noise will massively affect the 

# Stabilitet

Stability of closed loop system
![[Pasted image 20260612135554.png]]


Disturbance rejection of closed loop system (where $d(s)$ is the disturbance)
![[Pasted image 20260612135705.png]]

It can be seen, that by increasing $K(s)$, the output $y(s)=r(s)$.

# Anti windup

# Referencefølge og stationær fejl