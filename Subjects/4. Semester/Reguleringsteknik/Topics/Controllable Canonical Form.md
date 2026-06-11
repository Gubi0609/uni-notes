The single input state space model
## $$\dot x_c=A_cx_c+B_cu,\quad x_c\in\mathbb{R}^n,\quad u\in\mathbb{R}$$
is said to be on **controllable canonical form** if
![[Pasted image 20260611105415.png]]

where $a\in\mathbb{R}^{n\times 1}$, $a^T=\left[\begin{array}& a_1 & a_2 & ... & a_n\end{array}\right]$, $I_{n-1}$ is an $(n-1)\times (n-1)$ identity matrix, and $0_{(n-1)\times 1}$ is an $(n-1)\times 1$ matrix of zeroes.

It can be shown, that
## $$\det(\lambda I-A_c)=\lambda^n-a_1\lambda^{n-1}-...-a_n$$
Where the eigenvalues $\lambda$ are