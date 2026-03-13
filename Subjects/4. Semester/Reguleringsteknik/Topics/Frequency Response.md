![[Pasted image 20260313083027.png]]

The output of a time-invariant system will have the same frequency as the sinusoidal input, but possibly with a different amplitude and phase

The sy

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

