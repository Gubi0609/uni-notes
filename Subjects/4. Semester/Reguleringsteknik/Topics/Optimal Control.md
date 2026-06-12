We consider a linear control system of the form
## $$\dot x=Ax+Bu,\quad x(0)=x_0$$ $$y=Cx$$
A control law for such a system is said to be _optimal_ if it minimizes the cost functional
## $$\mathcal J=\int_0^\infty x^tQx+u^TRu \,dt$$
where $Q=Q^T$ is a positive semi-definite matrix and $R=R^T$ is a positive definite matrix.

# The Algebraic Riccati Equation (ARE)
An _Algebraic Riccati Equation_ is a second order matrix equation in an indeterminate $P=P^T\in\mathbb R^{n\times n}$ of the form
## $$A^TP+PA-PBR^{-1}B^TP+Q=0$$
where $A\in\mathbb{R}^{n\times n}$, $B\in\mathbb R^{n\times m}$ are matrices, $R=R^T\in\mathbb{m\times m}$ is a positive definite matrix, and $Q=Q^T\in\mathbb{R}^{n\times n}$ is a positive semi-definite matrix.

$P$ is called a _stabilizing solution_ to the ARE, if it satisfies the equation, and further satisfies the eigenvalues of $A-BR^{-1}B^TP$ are in the open left half plane.

# Optimal State Feedback Control
Consider a linear system of the form
## $$\dot x=Ax+Bu,\quad x(0)=x_0$$ $$y=Cx$$
Let $P$ be a stabilizing solution to the ARE
## $$A^TP+PA-PBR^{-1}B^TP+Q=0$$
Then the _optimal state feedback law_ is given by
## $$u=Fx\text{ where }F=-R^{-1}B^TP$$
## Output Variance Minimization
Introducing $y=Cx$ into a cost functional of the type
## $$\mathcal J=\int_0^\infty \rho y^Ry+u^Tu\, dt,\quad \rho\in\mathbb R$$
this can be written as an _optimal control problem_
## $$\mathcal J=\int_0^\infty \rho y^Ty+u^Tu\, dt$$ $$=\int_0^\infty px^TC^TCx+u^tu\, dt$$ $$=\int_0^\infty x^TQx+u^TRu\, dt,\quad Q=\rho C^TC,\quad R=I$$
## Tuning using Brysons Rule
Alternatively use a cost functional of the type
## $$\mathcal J=\int_0^\infty x^TQx+u^TRu\, dt$$
where $Q$ and $R$ are diagonal matrices.
With this can be written as an optimal control problem where
## $$Q_{ii}=\frac 1 {\text{maximum acceptable value of }x_i^2}$$ $$R_{jj}=\frac 1 {\text{maximum acceptable value of }u_j^2}$$
# Optimal State Estimation
Given the system
## $$\dot x=Ax+Bu+Gw$$ $$y=Cx+Du+v$$
with _unbiased process noise_ $w$ and _measurement noise_ $v$ with covariances
## $$\xi\{ww^T\}=Q,\quad \xi\{vv^T\}=R$$
then an optimal state estimator is given by
## $$\dot{\hat x}=A\hat x+Bu+L(C\hat x-y)$$
where
## $$L=-PC^TR^{-1}$$
and $P$ is a stabilising solution to the ARE
## $$A^TP+PA-PBR^{-1}B^TP+Q=0$$

> [!example]-
> ![[Pasted image 20260611160924.png]]
> ![[Pasted image 20260611160931.png]]
> ![[Pasted image 20260611160938.png]]
> We can see that there is a slight overswing compared to pole placement, but the rise time is quicker.

