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


# Anvendelse af rodkurve


# Stabilitet


# System performance
![[Pasted image 20260612094645.png]]
![[Pasted image 20260612094450.png]]
![[Pasted image 20260612094606.png]]

## $$a=-\zeta\omega_n\pm\omega_n\sqrt{\zeta^2-1}$$
- If $0<\zeta<1$ the poles of $H(s)$ are complex **(Underdamped case)**
- If $\zeta=1$ then $H(s)$ has a double pole in $s=-\zeta\omega_n$ **(Critically damped case)**
- if $\zeta>1$ then the poles of $H(s)$ are real and distinct **(Overdamped case)**