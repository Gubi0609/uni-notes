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
## $$\dot x=Ax+By$$ $$\dot x_I=y-r$$ $$y=Cx$$

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
Where $L$ is chosen such that $A+LC$ is stable with desiralbe eigenvalues