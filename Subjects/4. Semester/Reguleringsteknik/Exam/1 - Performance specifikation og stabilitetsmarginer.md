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

3 dampning cases (det står i dine noter for lecture 2)
# Ændring af dynamik ved indsættelse af pol eller nulpunkt
![[Pasted image 20260612100737.png]]
![[Pasted image 20260612100750.png]]



# Betydning og bestemmelse af fasemargin, forstærkningsmargin samt vektormargin