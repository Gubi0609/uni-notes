Most control systems are sample data systems, i.e., they consist of both _discrete_ and _continuous_ signals
![[Pasted image 20260327092902.png]]

> A **digital controller** both sample and quantize signals. In this course the quantization is omitted.
> Thus, **discrete controllers** are designed.

Two approaches to designing discrete controllers
- **Emulation:** Design continuous controller $K(s)$ and approximate it with $K(z)$ obtained via e.g. _Tustin's method_
- **Discrete design:** Design the discrete controller directly without computing $K(s)$.

The sampling frequency used for the discrete controller should be about _20 times the closed-loop bandwidth_. Otherwise, special care should be taken in the design of the discrete controller.

# Emulation
We consider the PID-controller in the $s$-domain
![[Pasted image 20260327093401.png]]

and its equivalent in the time-domain
![[Pasted image 20260327093438.png]]

Each of the terms in the PID controller is computed for discrete times in the following
![[Pasted image 20260327093507.png]]
where 
- $T$ is the _sampling time_
- $f$ is the _sampling frequency_

![[Pasted image 20260327093646.png]]


If we combine the three terms $u_P$, $u_I$, and $u_D$, that we just calculated we get
![[Pasted image 20260327094233.png]]

We notice that the terms in the controller _depends on the sampling time_ $T$. Thus, it needs to be known and constant for implementing the PID controller with constant gains.

To analyze the system, the I-term and D-term are $z$-transformed
![[Pasted image 20260327094730.png]]

We notice, that when we $z$-transform $y(k+1)$, we get
## $$y(k+1)\rightarrow z\cdot y(z)$$

Thus we have the following expression for the controller in the $z$-domain
![[Pasted image 20260327094752.png]]

We note, that the PID controller in the $s$-domain is
![[Pasted image 20260327094832.png]]

And given in the $z$-domain as
![[Pasted image 20260327094847.png]]

This means, that the discrete controller is obtained by replacing $s$ with
## $$\frac {2(z-1)}{T(z+1)}$$
This is called the _trapezoidal rule_ or _Tustin's method_.


In conclusion, a discrete equivalent of a controller $K(s)$ is
## $$K_d(z)=K\left(\frac {2(z-1)}{T(z+1)}\right)$$

This is in MATLAB `c2d`.

> [!example]- Example of PID Controller
> ![[Pasted image 20260327095241.png]]
> ![[Pasted image 20260327095253.png]]
> ![[Pasted image 20260327095302.png]]
> We can see that with a larger sampling time, the overshoot is actually _larger_ than for the continuous graph.

## Compensation for Sampling Effects
A signal sampled with zero-order hold is in average delayed by $T/2$ where $T$ is the sampling time
![[Pasted image 20260327095851.png]]

It is appropriate to include this delay in the model when designing a controller by emulation.

To incorporate the delay caused by zero-order hold in the design, the coninuous controller should be designed for the system $\tilde G(s)$  where $G_d(s)$ models the delay $T/s$
![[Pasted image 20260327100030.png]]

![[Pasted image 20260327100039.png]]
![[Pasted image 20260327100047.png]]

We can see, that the continuous with delay is much closer to the discrete.

## Design Procedure
![[Pasted image 20260327100142.png]]

# Numerical Integration Methods
The following integration rules are commonly used
![[Pasted image 20260327100229.png]]

Can approximate discrete transfer functions by substituting $s$ by the following expressions
![[Pasted image 20260327100317.png]]

To get the transfer function from a discrete transfer function, the variable $z$ is replaced by the following expressions
![[Pasted image 20260327100349.png]]


The left half-plane is mapped to different regions of the $z$-plane (shaded area) dependent on the numeric approximation method
![[Pasted image 20260327100432.png]]

**Discretization of a stable system using the forward rectangular rule may lead to an unstable discrete system.**

# Discrete design
![[Pasted image 20260327100533.png]]

## Design procedure
![[Pasted image 20260327100557.png]]

> [!example]-
> ![[Pasted image 20260327100652.png]]
> ![[Pasted image 20260327100701.png]]
> Since the poles are never within the unit-circle (dotted lined), the system can never be stable
> 
> ![[Pasted image 20260327100709.png]]

