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
## $$u(t)=K_pe(t)+K_i\int_{t_0}^{t}e(\tau)\, d\tau+K_d\frac {de(t)}{dt}\rightarrow K(s)=K_p\left(1+\frac 1 {sT_i}+sT_d\right)$$
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
lectromechanical systems have saturation on their physical variables.
- The output of any actuator is limited from above and below
- This creates _clipping_
![[Pasted image 20260320084947.png]]

The saturation must be taken into account, when _integral action_ is present in the controller.
![[Pasted image 20260320085057.png]]
- We can see that the output for the system _with saturation_ reaches a higher peak, because the regulator is limited at _1_.
We can use _two anti-windup mechanisms_
- **Back-Calculation**
- **Conditional Integration**
Both methods utilize the following signal
![[Pasted image 20260320085434.png]]

## Back-Calculation
This recomputes the integral term when the system input is saturated, as shown below (on a PID regulator)
![[Pasted image 20260320085542.png]]

The value of the integrator output is not changed instantaneously, but it is changed based on the **tracking time constant** $T_t$.

The input of the integrator is given by
## $$ \frac 1 {T_t}e_s+\frac {K_p}{T_i}e$$
where $e_s$ is zero when the system is not saturated.

Evidence of improved performance
![[Pasted image 20260612142904.png]]

## Conditional Integration
This is also known as _clamping_. It is a bit simpler than back-calculation, and just stops integrating when the system is in saturation
![[Pasted image 20260320090037.png]]

Although it is simple, it still improves the performance of the system
![[Pasted image 20260320090103.png]]

**It is beneficial to use conditional integration in 9/10 cases, as it is simple, yet effective**

# Referencefølge og stationær fejl

The DC gain of the closed loop system is given by the _Final Value Theorem_ ([[Subjects/4. Semester/Reguleringsteknik/Topics/Steady State Tracking|Steady State Tracking]])
## $$\frac {G(0)K_p}{1+G(0)K_p}$$
And the steady state error $e_{ss}$ is then given as (_for constant reference_ $r(s)=r$)
## $$e_{ss}=\left(1-\frac {G(0)K_p}{1+G(0)K_p}\right)r=\frac {1} {1+G(0)K_p}r$$
**From this we can see that $K_p$ should be large to decrease the steady state error. Since this is infeasible, steady state error cannot be eliminated solely by proportional gain.**

> Assuming that a closed loop system reaches steady state. Then the integral action removes the _steady state error_.

> [!example] Proof of removing steady state error
> Assume that there is a steady state error with $u=u_0$ and $e_0$. Then
> $$u_0=K_pe_0+K_ie_0t$$
> Which is a contradiction except if $e_0=0$ or $K_i=0$. This hints, that the error $e_0$ must be 0.

Referencefølge simply means: **how well does the system output y(t) follow the reference signal r(t)?**

In a closed-loop system, the goal is that y tracks r as closely as possible. The measure of how well it does so is the **steady-state error**:
## $$e_{ss}=\lim_{⁡t\rightarrow\infty}(r(t)-y(t))$$
If $e_{ss} = 0$, the system tracks the reference perfectly in steady state. If $e_{ss} \neq 0$, there is a permanent offset between what you asked for and what you got.

A higher order system has better reference follow
![[Pasted image 20260612145606.png]]

If 0, the steady state error is 0, if $\infty$ the steady state error grows without bound. The finite numbers mean, that there is a steady state error of that size.
The system type references how many integrator terms there are in the controller. So a P/PD controller would be type 0, PI/PID controller would be type 1, and a PID + PID controller combination would be type 2

**Can also be seen from poles in origo, as $1/s$ is the integrator, and has a pole in origo.**

#### What this means practically:

**Type 0** — no integrators in the loop. A pure P-controller with a plant that has no integrator. Can never track a step perfectly (there is always a residual error $\frac{1}{1+K_p}$), and completely fails on ramps.

**Type 1** — one integrator in the loop. This is what you get with a PI or PID controller, or a plant that already contains an integrator (e.g. a motor where you control velocity by commanding acceleration). Tracks step references perfectly ($e_{ss} = 0$), has a finite error on ramps.

**Type 2** — two integrators. Tracks both steps and ramps perfectly, finite error on parabolic references. Rare in practice as it is harder to stabilise.

**Adding an integrator to the controller raises the system type by one**. A Type 0 plant with a PI controller becomes a Type 1 system, which now tracks step references with zero steady-state error. This is the formal justification for why integral action eliminates steady-state error

#### The constants $K_p$​,$K_v$,$K_a$​
These are called position, velocity and acceleration error constants respectively. They are properties of the open-loop transfer function evaluated at specific limits, and they set the size of the residual error when the system cannot track perfectly.