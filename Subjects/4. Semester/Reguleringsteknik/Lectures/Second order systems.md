The transfer function of a second order system is
## $$H(s) = \frac {k\omega_n^2}{s^2+2\zeta\omega_ns+\omega_n^2}$$
an is described by the gain $k$ and two paramters $\zeta>0$ and $\omega_n>0$.

The poles will be the roots of the denumerator. The system has _two_ poles which are $s\in \C$ 
## $$a=-\zeta\omega_n\pm\omega_n\sqrt{\zeta^2-1}$$
- If $0<\zeta<1$ the poles of $H(s)$ are complex **(Underdamped case)**
- If $\zeta=1$ then $H(s)$ has a double pole in $s=-\zeta\omega_n$ **(Critically damped case)**
- if $\zeta>1$ then the poles of $H(s)$ are real and distinct **(Overdamped case)**

> [!example]- Underdamped Second Order System
> ![[Pasted image 20260213084608.png]]

# Underdamped second order system
## Impulse Response
The impulse response of the system is 
## $$h(t)=k\frac{\omega_n} {\sqrt{1-\zeta^2}}e^{-\sigma t}\sin(\omega_d t)1(t)$$
![[Pasted image 20260213084904.png]]

## Step reponse
The step response of the system is
## $$y(t)=k\left(1-e^{-\sigma t}\left(\cos(\omega_dt)+\frac \sigma {\omega_d}\sin(\omega_dt)\right)\right)$$
![[Pasted image 20260213085031.png]]

If we want a _good_ system, (e.g. an auto pilot in a car) we would not want it to swing much, so we would need a high damping ratio $\zeta$.

## Bode plot
The bode plot of a second order system depends on the _damping ratio_ $\zeta$.
![[Pasted image 20260213084726.png]]

We can see for the small damping ratio that we have a peak at our resonance frequency. This is not good.

# Critically damped system
## Impulse response
The impulse response of the system is
## $$h(t)=k\omega_n^2te^{-\omega_n t}$$

![[Pasted image 20260213085640.png]]

## Step response
The step response for the system  is
![[Pasted image 20260213085704.png]]

# Overdamped system
## Impulse response
The impulse response of the system is
![[Pasted image 20260213085734.png]]

## Step response
The step response of the system is
![[Pasted image 20260213085752.png]]