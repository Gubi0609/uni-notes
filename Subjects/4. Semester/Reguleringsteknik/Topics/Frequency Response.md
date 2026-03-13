![[Pasted image 20260313083027.png]]

The output of a time-invariant system will have the same frequency as the sinusoidal input, but possibly with a different amplitude and phase

> [!help] Summary
> The system response subject to the input $u(t)=A\cos(\omega t)$ is
> $$y(t)=\frac A 2 M(\omega)\cos(\omega t+\phi(\omega))$$
> where
> $$M(\omega)=|H(j\omega)|\text{ and } \phi(\omega)=\angle H(j\omega)$$

---

The output of a time-invariant system is given by
![[Pasted image 20260313083139.png]]
where y is the output, u is the input, and h is the impulse response of the system

If we want the frequency response, we are only interested in the sinusoidal input
![[Pasted image 20260313083225.png]]

This can be written using Euler's formula instead
![[Pasted image 20260313083256.png]]


![[Pasted image 20260313083315.png]]
This is basically a _Laplace transform_

$y(t)$ is then given as
![[Pasted image 20260313083704.png]]

Where the complex number $H(j\omega)$ is expressed in polar form as
![[Pasted image 20260313083730.png]]
Where $M(\omega)$ is the magnitude of H and $\phi(\omega)$ is the phase of H.

Then $y(t)$ is
![[Pasted image 20260313083857.png]]

> [!example]- First-Order differential equation
> ![[Pasted image 20260313084305.png]]
> ![[Pasted image 20260313084313.png]]

> [!example]- Second-Order system
> ![[Pasted image 20260313085553.png]]

# Bandwidth
The bandwidth of a closed-loop system $T(s)$ is defined to be the _maximum frequency_ at which the output $y$ of a system will track a sinusoidal input $r$ in a satisfactory manner (output attenuated to $1/\sqrt{2}$ times the input).
Formally, the bandwidth $\omega_{BW}$ of $T(S)$ is the maximal frequency such that
![[Pasted image 20260313085754.png]]

![[Pasted image 20260313085804.png]]

For a second order system, the bandwidth is approximately equal to the natural frequency.