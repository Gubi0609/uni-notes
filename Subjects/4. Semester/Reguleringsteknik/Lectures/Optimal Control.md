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
Then the optimal state feedback law is given by
## $$u=Fx\text{ where }F=-R^{-1}B^TP$$
