
# Discrete time system
A linear discrete-time system
## $$x_{k+1}=\Phi x_k$$
where $x_k\in\R$ and $\Phi\in\R^{n\times n}$ is _asymptotically stable_ if
![[Pasted image 20260213094444.png]]

The system is asymptotically stable if and only if all eigenvalues have magnitude smaller than one (they are within the unit circle (think back to [[Subjects/3. Semester/Signalbehandling/Signalbehandling|Signalbehandling]])).

## Derivation of Stability Condition
![[Pasted image 20260213094611.png]]
Since we have $\Lambda^k$ it would grow to a _very large number_ for eigenvalues larger than 1. Thus we must have eigenvalues $0<\Lambda<1$ to have something stable.

# Continuous time system
A lineay continuous time system described by the state equation
## $$\dot x=Ax$$
is asymptotically stable if and only if all eigenvalues have _negative real part_

## Derivation of Stability Condition
![[Pasted image 20260213095207.png]]

# $s$-plane Vs $z$-plane
![[Pasted image 20260213095235.png]]

`zgrid` can be used in matlab for this illustration. (I think...)