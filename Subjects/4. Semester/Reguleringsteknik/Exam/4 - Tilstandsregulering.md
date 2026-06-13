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

Used to directly control the _states_ of the system by reading them and affecting them accordingly with gains.

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
## Integral Feedback
If an integral term is needed, this can also be done through integral feedback

Considering a state space system of the form
## $$\dot x=Ax+Bu$$ $$y=Cx$$
for which we wish to design a feedback law
## $$u(t)=Fx(t)+F_Ix_I(t)$$
The $I$ denotes an _integrator term_. Thus
## $$x_I(t)=\int_0^ty(\tau)-r(\tau)d\tau$$
Differentiating this yields
## $$\dot x_I(t)=y(t)-r(t)$$
where $y$ is the output and $r$ is the reference
We now have the equations
## $$\dot x=Ax+Bu$$ $$\dot x_I=y-r$$ $$y=Cx$$

Can then be combined into an extended state model
## $$\left[\begin{array}& \dot x \\ \dot x_I\end{array}\right]=\left[\begin{array}& A & 0 \\ C & 0\end{array}\right]\left[\begin{array}& x \\ x_I\end{array}\right] + \left[\begin{array}& B \\ 0\end{array}\right]u+ \left[\begin{array}& 0 \\ -I\end{array}\right]r$$ $$y=\left[\begin{array}& C & 0\end{array}\right] \left[\begin{array}& x \\ x_I\end{array}\right]$$
Referring back to the feedback law from before, this becomes
## $$u=Fx+F_Ix_I=\left[\begin{array}& F & F_I\end{array}\right]\left[\begin{array}& x \\ x_I\end{array}\right]$$

Noticing the form of the extended state space model above, we can notice, that it in itself is a state space model
## $$\dot x_e=A_ex_e+B_eu$$ $$y=C_ex_e$$
for which we have to design a state feedback $u=F_ex_e$, where
## $$F_e=\left[\begin{array}& F & F_I\end{array}\right], \quad x_e=\left[\begin{array}& x \\ x_I\end{array}\right]$$ $$A_e = \left[\begin{array}& A & 0 \\ C & 0\end{array}\right], \quad B_e = \left[\begin{array}& B \\ 0\end{array}\right], \quad C_e = \left[\begin{array}& C & 0\end{array}\right]$$

This yields the following block diagram
![[Pasted image 20260611145138.png]]

Where the black part is the actual system, while the green part is the regulator. The integrator state $x_I$ is a fictive state, that we have added, and thus not something the system actually has.

If the states are unavailable for feedback, they can be estimated by e.g. a full order [[Subjects/4. Semester/Reguleringsteknik/Topics/Observability|Observer]]
## $$\dot{\hat x}=A\hat x+Bu+L(C\hat x-y)$$ $$\hat y=C\hat x$$
Where $L$ is chosen such that $A+LC$ is stable with desirable eigenvalues. (eigenvalues denoting the poles of the system).

**Separation result:** The closed loop poles of such an observer based integral control scheme consist of the eigenvalues of
## $$A_e+B_eF_e\text{ and of }A+LC$$
The block diagram is now
![[Pasted image 20260611153637.png]]

Where the red part is the **observer** and the yellow part is a **copy of the system** (seen in black) also known as the _state estimate_.
Everything that is not black is part of the controller.

# Design af observere


# Referencefølge