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

Thus we have the 
