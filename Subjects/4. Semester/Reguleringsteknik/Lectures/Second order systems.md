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

# Bode plot
The bode plot of a second order system depends on the _damping ratio_ $\zeta$.
![[Pasted image 20260213084726.png]]