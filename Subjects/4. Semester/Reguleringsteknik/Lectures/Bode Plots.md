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

