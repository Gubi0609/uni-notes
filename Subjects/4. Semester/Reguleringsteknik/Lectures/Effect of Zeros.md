A general transfer function
![[Pasted image 20260327082954.png]]

Can be written
## $$G(s)=G_1(s)G_2(s)$$

where
![[Pasted image 20260327083015.png]]
The signal $u_2(s)$ is a _preconditioned version_ of $u(s)$ only affected by the system poles.

![[Pasted image 20260327083655.png]]

> [!example]- Impulse response of different systems
> ![[Pasted image 20260327084701.png]]
> $a=1$
> For system 1, it simply has an impulse response of $y(t)=1-e^{-t}$
> For system 2, we can split it up into two systems, one that contains the poles, and one that contains the zeros
> - Subsystem 1: $1/(s+1)$. The impulse response for this is the same as the above
> - Subsystem 2: $s$. $s$ in the time domain, is equal to taking the time derivative, so that will be the time derivative of subsystem 1. Thus: $e^{-t}$
> For system 3, since $a=1$, the numerator and denominator is the same, so $G_3(s)=1$.


# Non minimum phase
Zeros in the right half-plane give rise to non-minimum phase behavior.

We can take some examples of this
![[Pasted image 20260327085130.png]]

Generally speaking, zeros _lifts_ the phase, but if they are in the right half-plane, they contribute with a _phase drop_

Step responses:
![[Pasted image 20260327085144.png]]

We can see that we have _reverse swing_ for the red system above. Essentially it is the same as overshoot, but we shoot in the wrong direction.

## Higher order zeros
Higher-order zeros can also occur in transfer functions.
We consider
![[Pasted image 20260327085648.png]]

Thus we have the bode plot