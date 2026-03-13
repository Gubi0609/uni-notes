> [!help] Summary
> 1. Rewrite the considered transfer function into Bode form.
> 2. Determine the value of the $K_0(j\omega)^n$ term. Plot the low frequency magnitude asymptote through the point $K_0$ at $\omega = 1$ and with slope of $n\times$ 20/db per decade.
> 3. Complete the composite magnitude asymptotes by extending the low-frequency asymptote until the first frequency break point. Then change the slope according to the behavior at the break point, and continue the procedure for the remaining break points.
> 4. Sketch the approximate magnitude curve by increasing the asymptote value by a factor $\sqrt{2}$ at first-order numerator break and decreasing it by a factor $1/\sqrt{2}$ at denominator break points.
> 5. Plot the low-frequency asymptote of the phase $\phi = n \times 90\deg$.
> 6. Change the phase at the phase points, and correct the phase according to the slope at the phase point.

---

![[Pasted image 20260313091453.png]]

# Advantages of working with bode plots
1. Dynamic compensator design can be based entirely on the Bode plots. (We will do this in the next lecture)
2. Bode plots can be determined experimentally.
3. The Bode plot of a system defined by a series connection is given by the addition of the Bode plots of the individual systems.
4. The use og log scale permits a much wider range of frequencies to be displayed on a single plot than is possible with linear scales.



> [!example]- Bode Form of Transfer Function
> ![[Pasted image 20260313092321.png]]
> In the _Bode form_ we could substitute $s$ with $j\omega$, as that is the actual variable.

# Classes of Terms in Transfer Function
Three classes of terms of the transfer function are analyzed
1. Class 1: $K_0(j\omega)^n$ for $n\in\mathbb{Z}$ 
2. Class 2: $(j\omega\tau +1)^{\pm1}$
3. Class 3: $((j\omega/\omega_n)^2+2\zeta(j\omega/\omega_n)+1)^{\pm1}$

Where $n$ is the number, that $s$ is to the power of.
E.g.
$$G_0(s)=\frac 1 s=s^{-1}\Rightarrow n=-1$$
## Class 1
![[Pasted image 20260313092803.png]]
![[Pasted image 20260313092814.png]]

## Class 2
![[Pasted image 20260313093356.png]]
![[Pasted image 20260313093405.png]]
## Class 3
![[Pasted image 20260313093920.png]]

# Neutral Stability
![[Pasted image 20260313094316.png]]
![[Pasted image 20260313094330.png]]

