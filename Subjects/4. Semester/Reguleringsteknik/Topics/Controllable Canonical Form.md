The single input state space model
## $$\dot x_c=A_cx_c+B_cu,\quad x_c\in\mathbb{R}^n,\quad u\in\mathbb{R}$$
is said to be on **controllable canonical form** if
![[Pasted image 20260611105415.png]]

where $a\in\mathbb{R}^{n\times 1}$, $a^T=\left[\begin{array}& a_1 & a_2 & ... & a_n\end{array}\right]$, $I_{n-1}$ is an $(n-1)\times (n-1)$ identity matrix, and $0_{(n-1)\times 1}$ is an $(n-1)\times 1$ matrix of zeroes.

It can be shown, that
## $$\det(\lambda I-A_c)=\lambda^n-a_1\lambda^{n-1}-...-a_n$$
Where the eigenvalues $\lambda$ are the **poles of the system**.

# Example with $n=3$
For $n=3$ the controllable canonical form becomes
![[Pasted image 20260611110020.png]]

which is controllable
## $$\mathcal C_c=\left[\begin{array}[cccc] & B_c & A_cB_c & ... & A_c^2B_c\end{array}\right]=\left[\begin{array} & 1 & a_1 & a_1^2 + a_2 \\ 0 & 1 & a_1 \\ 0 & 0 & 1\end{array}\right]$$
since $\det(\mathcal C)=1\neq 0$.

# Transformation to Controllable Canonical Form
Given a state space model of a controllable system
## $$\dot x=Ax+Bu, \quad x\in\mathbb{R}^n,\quad u\in\mathbb R$$
we wish to find a basis transformation $x=Tx_c$, such that
## $$\dot x_c=A_cx_c+B_cu, \quad x_c\in\mathbb{R}^n,\quad u\in\mathbb R$$
