- Betydning af rodkurve
- Anvendelse af rodkurve
- Stabilitet
- System performance

[[L5 - The Root Locus Method]]
- Rodkurvens betydning og opbygning
- Anvendelse til polplacering og controllerdesign
- Stabilitet via rodkurve
- System performance
	- Specifikation af rise time, dæmpning osv. via polplacering på rodkurven
[[L2 - Stability and Performance Analysis]]
- Relation mellem polplacering og dynamik
- Performance specifikation
[[L8 - Implementation]]
- Effekten af at tilføje poler/nulpunkter på rodkurven


# Betydning af rodkurve
The root locus method is used for describing how the poles of $G(s)$ move around in the
$s$-plane, when the parameter $K$ changes.

Useful when we have a _system model_ $G(s)$

![[Pasted image 20260613110156.png]]

By seeing how the poles move, we can determine if our controller should add extra poles or zeros (or both). This is done by determining if changing the gain $K$ will move _all_ poles to the left half plane

![[Pasted image 20260613110601.png]]

This system needs extra zeroes (a $D$-term), because it has positive real poles already. Thus, we need to pull these the left half plane using zeroes (as poles move towards zeroes, when $K$ is increased)


As can be seen from this step response 
![[Pasted image 20260613110809.png]]

the output moves closer to the reference value by adding a $D$-term (which adds a zero).
Both the P-control and the PD-control has a closed-loop pole at $s = -2$. Thus, it is not only the closed loop poles, that describe the behavior of the system.

# Anvendelse af rodkurve
![[Pasted image 20260613111058.png]]
![[Pasted image 20260613111105.png]]
![[Pasted image 20260613111111.png]]



# Stabilitet
- $\sigma > 0$: System is **stable**, since poles are in the _left half plane_
- $\sigma=0$: System is **marginally stable**, since poles are _on the imaginary axis_. This introduces **sustained oscillation**
- $\sigma<0$: System is **unstable**, since poles are in the _right half plane_

**K determines where on the root locus the poles sit**. As K increases from 0 to ∞, poles travel along the branches. Some branches will cross the imaginary axis at some critical gain $K_{critical}$ ​ — below this gain the system is stable, above it the system is unstable (or vice versa depending on the plant). This $K_{critical}$ ties in to the _gain margin_.

Stability is determined by whether the closed-loop poles are in the left half-plane

The root locus shows pole locations for all values of K — stability is directly readable, by noticing the location of the poles at a given K.
# System performance
![[Pasted image 20260612094645.png]]
![[Pasted image 20260612094450.png]]
![[Pasted image 20260612094606.png]]

**You use the performance requirements (ζ, ω_n, σ) to define a desired pole region in the s-plane, then choose K such that the root locus passes through that region.**
## $$a=-\zeta\omega_n\pm\omega_n\sqrt{\zeta^2-1}$$
- If $0<\zeta<1$ the poles of $H(s)$ are complex **(Underdamped case)**
- If $\zeta=1$ then $H(s)$ has a double pole in $s=-\zeta\omega_n$ **(Critically damped case)**
- if $\zeta>1$ then the poles of $H(s)$ are real and distinct **(Overdamped case)**

#### Rise time
## $$t_r=\frac {1.8}{\omega_n}$$

#### Settling time
## $$t_s=\frac {-\log(\alpha/100)}{\omega_n\zeta}$$

#### Peak time
## $$t_p=\frac\pi{\omega_d}$$
#### Overshoot
## $$M_p=e^{-\pi\zeta/\sqrt{1-\zeta^2}}$$