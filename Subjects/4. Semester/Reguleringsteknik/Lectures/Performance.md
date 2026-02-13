Performance of a system can be specified in both time and frequency domain

### Time domain
- Rise time
- Setting time
- Overshoot

This entails the stability of the dynamical system
## $$\dot x=Ax+Bu \quad \quad y=Cx$$
And can be determined from the _eigenvalues_ of A.

### Frequency domain
![[Pasted image 20260213082430.png]]


This entails the stability of the transfer function
## $$G(s)=\frac {Q(s)}{P(s)}$$
where the poles of $G(s)$ describes the stability.
- If the _real part_ of the poles (the roots of $P(s)$) is _negative_ the system is stabel. The imaginary part has no say in the stability.