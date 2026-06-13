- Stabilitet
- Tilstandstilbagekobling
- Design af observere
- Referencefølge

[[L1 - Introduction to Linear Time-Invariant Systems]]
- State space modeller (kontinuert og diskret)
- Transferfunktioner
- Laplace/z-transform
- Diskretisering
- Fundament for al tildstandsreguelring
[[L2 - Stability and Performance Analysis]]
- Stabilitet
[[L7 - Dynamic Compensators and Stability Margins]]
- Stabilitet
[[L9 - State Feedback]]
- Styrbarhed
- Kontrollerbar kanonisk form
- Tilstandstilbagekobling og polplacering
- Stabilitet
[[L11 - Optimal Control]]
- Referencefølge via integral control og reference signals
- Zero assignment
- LQR optimal control
- Anti windup
[[L10 - Observer Design]]
- Observerbarhed
- Fuldt ordens observer (Luenberger)
- Polplacering for observere
- Observer-baseret regulering
- Separationsprincippet
- Integralregulering med observer
[[L12 - The Kalman Filter]]
- Referencefølge (afslutning fra L11)
- Zero assignment (afslutning)
- Kalman filter som stokastisk observer

# Stabilitet
Uses state space model
![[Pasted image 20260206085202.png]]
![[Pasted image 20260206085226.png]]

Poles of continuous
![[Pasted image 20260613120936.png]]

Zeroes for continuous
![[Pasted image 20260613120951.png]]


Stability
![[Pasted image 20260613121039.png]]

Since the continuous system is in the $s$-plane, the eigenvalues correspond to the $s$-plane poles. Thus they need to have  a negative real part to be stable

The discrete time system is in the $z$-plane, thus the eigenvalues correspond to the $z$-plane poles. This means, that the eigenvalues' magnitude will need to be less than one, for them to lie within the unit circle
![[Pasted image 20260613121214.png]]

We just stick to $s$-plane (continuous time) for ease.

# Tilstandstilbagekobling

Used to directly control the _states_ of the system by reading them and affecting them accordingly with 

![[Pasted image 20260613122906.png]]

For a state space model
## $$\dot x=Ax+Bu$$
a _state feedback_ is a feedback of the form
## $$u=Fx$$
Combining these equations, we obtain
## $$\dot x=Ax+BFx=(A+BF)x$$
Thus, the result of a state feedback is a system with a modified system matrix, and thus with _modified poles_.


## $$s_3 = \left[\begin{array}& 0 & 0 & 1\end{array}\right]\mathcal C^{-1},\quad s_2=s_3A, \quad s_1=s_2A$$
## $$\mathcal{C} = \left[\begin{array}[cccc] & B & AB & ... & A^{n-1}B\end{array}\right]$$
An either continuous or discrete time system is controllable **iff**
## $$\text{rank}\left[\begin{array}[cccc] & B & AB & ... & A^{n-1}B\end{array}\right]=n$$
or if the number of inputs $m=1$, this reduces to
## $$\det\left(\left[\begin{array}[cccc] & B & AB & ... & A^{n-1}B\end{array}\right]\right)\neq 0$$

# Design af observere


# Referencefølge