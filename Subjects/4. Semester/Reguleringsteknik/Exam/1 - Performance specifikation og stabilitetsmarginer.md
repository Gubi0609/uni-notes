- Stabilitet
- Relation mellem polplacering og system dynamik
- Ændring af dynamik ved indsættelse af pol eller nulpunkt
- Betydning og bestemmelse af fasemargin, forstærkningsmargin samt vektormargin

[[L2 - Stability and Performance Analysis]]
- Stabilitet
- Polplacering og systemdynamik
- Performance specifikation
- Relation mellem polplacering og transientrespons
- Nulpunkter i state-space modeller
[[L6 - Nyquist Stability Criterion]]
- Frekvensrespons
- Bode plots
- Nyquist stabilitetkriteriet
- Fasemargin
- Forstærkningsmargin
- Vektormargin
[[L8 - Implementation]]
- Virkningen af at tilføje poler eller nulpunkter

# Stabilitet
![[Pasted image 20260612094450.png]]

![[Pasted image 20260612094645.png]]

![[Pasted image 20260612094730.png]]

![[Pasted image 20260612094755.png]]

Poler af transfer function $G(s)$ i stedet for kun state space model.

When a system is asymptotically stable, it returns to equilibrium

Marginally stable means the system has a bounded but non-decaying oscillation

Unstable means that the controller isn't controlling properly.

Formler for overshoot, settling time, peak time og så videre.

> A value p is a pole of G(s) if and only if p is an eigenvalue of A

This is the formal justification for why stability is determined by the eigenvalues of A. The poles of the transfer function G(s) = C(sI − A)⁻¹B + D blow up exactly when det(sI − A) = 0, which is the characteristic equation for the eigenvalues of A. It is a small point but ties your stability notes and your pole-placement notes together cleanly.
# Relation mellem polplacering og system dynamik
![[Pasted image 20260612094450.png]]
![[Pasted image 20260612094606.png]]
## $$a=-\zeta\omega_n\pm\omega_n\sqrt{\zeta^2-1}$$
- If $0<\zeta<1$ the poles of $H(s)$ are complex **(Underdamped case)**
- If $\zeta=1$ then $H(s)$ has a double pole in $s=-\zeta\omega_n$ **(Critically damped case)**
- if $\zeta>1$ then the poles of $H(s)$ are real and distinct **(Overdamped case)**
# Ændring af dynamik ved indsættelse af pol eller nulpunkt
![[Pasted image 20260612100737.png]]
![[Pasted image 20260612100750.png]]

Zeros is the numerator of $G(s)$, poles are the denominator

combining multiple systems through multiplying (cascade implementation of higher order systems) combines their individual bode plots.

Zeros in the right half plane give **rise to non-minimum phase behavior**
![[Pasted image 20260612105948.png]]
![[Pasted image 20260612105956.png]]

Normally zeros _lift_ the phase (blue line), but if they are in the right half plane, the phase actually _drops_ (red line).
We can also see, that a right half plane zero introduces _reverse swing_, which is just like overswing, but in the wrong direction

We can also look at higher order systems
![[Pasted image 20260612110219.png]]
![[Pasted image 20260612110226.png]]

To solve the problem of the blue line (reverse swing) we would need to analyze the system, and try to move the zeros, so that they are _not complex conjugates_.

Performance of zeroes:
![[Pasted image 20260612110322.png]]

If we move the zero further from the origin, we can _reduce the overshoot_. (the further into the left half plane, the less overshoot).


In regards to poles:
- Poles should be in the left-half plane. If they are not, the system is not stable
- Poles should be placed to fulfill system requirements (see illustration [[1 - Performance specifikation og stabilitetsmarginer#Relation mellem polplacering og system dynamik|above]])
# Betydning og bestemmelse af fasemargin, forstærkningsmargin samt vektormargin

The **gain margin** is the factor by which the gain can be _raised_ before a system becomes unstable

For a _neutrally stable_ system
## $$|L(j\omega)|=1\text{ and } \angle L(j\omega)=180^\circ$$



where $L(s)=K(s)G(s)$
![[Pasted image 20260612131647.png]]

Can be found from bode plot
- Find the value of $\omega$ where $\angle K(j\omega)G(j\omega)=-180^\circ$, and denote it by $\omega_{GM}$. The gain margin in dB is given by
## $$GM=-|K(j\omega_{GM})G(j\omega_{GM})|$$




The **phase margin** is the amount by which the phase can be raised before a system becomes unstable (exceeds $-180^\circ$)
(Se neutralt stabilt system ovenover)

Can be found from bode plot
- Find the value of $\omega$ where $|K(j\omega)G(j\omega)|=0\text{ db}$ and denote it by $\omega_c$ (**Called the crossover frequency**). The phase margin is then given by
## $$PM=\angle K(j\omega_c)G(j\omega_c)+180^\circ$$

![[Pasted image 20260612132220.png]]


Kan også findes ud fra Nyquist plot, hvor de bestemmes ud fra hvor tæt de er på $-1$
![[Pasted image 20260612132300.png]]


The phase and gain marhins determine stability when only _one of them is changed_.
This is the motivation for looking at the **vector margin**, which gives the shortest distance between the Nyquist plot and -1
![[Pasted image 20260612132909.png]]

This is related to the _maximum sensitivity_
## $$\text{Vector margin}=\frac 1 {M_s}$$
 where $M_s=\max_\omega|S(j\omega)|$ and $S(s)=1/(1+K_0G_0)$ is the sensitivity function ([[Subjects/4. Semester/Reguleringsteknik/PDFs/Lecture 3 - Introduction to Control.pdf#page=44|Lecture 3 - Introduction to Control]])
==Dette står dog ikke direkte i slides for vektor margin, så vær påpasselig med at bruge det til eksamen==.

The vector margin then captures robustness against simultaneous changes in both gain and phase, which the individual margins cannot.