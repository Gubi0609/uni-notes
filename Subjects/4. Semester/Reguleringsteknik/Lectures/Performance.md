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

If we have a frequency of 0 (s=0), we get the _DC_-gain of the system.

# Specifications
![[Pasted image 20260213085824.png]]

The rise time is the time that it takes to rise from $10\%$ to $90\%$ of the setpoint value.
The settling time is how long it takes to settle at our the setpoint value (no swinging).

Peak time is not used in describing the performance. 
## Rise time
