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

![[Pasted image 20260610151258.png]]
![[Pasted image 20260610151609.png]]


The integral term is useful instead of using feedforward, as feedforward requires a perfect, known system model and no disturbance, while the integral term can operate even under those conditions.

It can also be implemented with noise reduction on the derivative term
## $$T_{ue}(s)=K_p\left(N-\frac N {1+sT_d/N}\right)=K_p\frac {sT_d}{1+sT_d/N}$$
![[Pasted image 20260610150811.png]]

Where $N$ is a filter constant, typically between $2$ to $20$.
This is done, as noise will massively affect the change in error, as its tilt is rather steep compared to actual data

We can also implement the integral term with automatic reset
## $$T_{ue}=K_p\frac {1+sT_i}{sT_i}=K_p+\frac {K_p}{sT_i}$$
![[Pasted image 20260610145447.png]]

By wiring it as such, the integral term directly affects the controller output $u$, approaching steady state.


## Zeigler-Nichols tuning based on step response
The considered system is assumed to have the transfer function
## $$\frac {y(s)}{u(s)}=\frac A {\tau s+1}e^{-st_d}$$
where $t_d=L$ is the time delay of a first order system (the $L$ will be used later on), $A$ is the top of the step response (amplitude) and $\tau$ is the time from when the tilt of the step response hits $y=0$ to the time it hits $y=A$
![[Pasted image 20260610152912.png]]

By using the Zeigler-Nichols tuning method, a closed loop system is obtained that has a decay ratio of ~$0.25$ (damping ratio $\zeta \approx 0.21$)
![[Pasted image 20260610153038.png]]
![[Pasted image 20260610153139.png]]

## Zeigler-Nichols tuning - The Ultimate Sensitivity method
An alternative to studying the step response is to connect a P-controller to the system, and increase the gain $K_p$ until the output oscillates.
![[Pasted image 20260610153549.png]]

The value of $K_p$ when the output oscillates with a constant amplitude is called the **ultimate gain** $K_u$. The period of oscillation $P_u$ is called the **ultimate period**.
![[Pasted image 20260610153733.png]]


# Stabilitet

Stability of closed loop system
![[Pasted image 20260612135554.png]]


Disturbance rejection of closed loop system (where $d(s)$ is the disturbance)
![[Pasted image 20260612135705.png]]

It can be seen, that by increasing $K(s)$, the output $y(s)=r(s)$.


# Anti windup



# Referencefølge og stationær fejl

The DC gain of the closed loop system is given by the _Final Value Theorem_ ([[Subjects/4. Semester/Reguleringsteknik/Topics/Steady State Tracking|Steady State Tracking]])
## $$\frac {G(0)K_p}{1+G(0)K_p}$$
And the steady state error $e_{ss}$ is then given as (_for constant reference_ $r(s)=r$)
## $$e_{ss}=\left(1-\frac {G(0)K_p}{1+G(0)K_p}\right)r=\frac {1} {1+G(0)K_p}r$$
**From this we can see that $K_p$ should be large to decrease the steady state error.**

> Assuming that a closed loop system reaches steady state. Then the integral action removes the _steady state error_.

> [!example] Proof of removing steady state error
> Assume that there is a steady state error with $u=u_0$ and $e_0$. Then
> $$u_0=K_pe_0+K_ie_0t$$
> Which is a contradiction except if $e_0=0$ or $K_i=0$. This hints, that the error $e_0$ must be 0.
