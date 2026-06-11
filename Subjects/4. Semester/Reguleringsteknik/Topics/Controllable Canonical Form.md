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
where $A_c=T^{-1}AT$ and $B_c=T^{-1}B$ is in controllable canonical form. We can solve for $T^{-1}$ by rewriting these equations as
## $$A_cT^{-1}=T^{-1}A\text{ and }B_c=T^{-1}B$$
going back to the example with $n=3$, we can write the rows of $T^{-1}$ as
## $$T^{-1}=\left[\begin{array} & s_1\\ s_2 \\ s_3\end{array}\right], \quad s_1,s_2,s_3\in\mathbb R^{1\times n}$$
then we can rewrite the transformation equations from earlier as
## $$\left[\begin{array}& a_1 & a_2 & a_3 \\ 1 & 0 & 0 \\ 0 & 1 & 0\end{array}\right]\left[\begin{array}& s_1 \\ s_2 \\ s_3\end{array}\right] = \left[\begin{array}& s_1 \\ s_2 \\ s_3\end{array}\right]A,\quad \left[\begin{array}& s_1 \\ s_2 \\ s_3\end{array}\right]B=\left[\begin{array}& 1 \\ 0 \\ 0\end{array}\right]$$
Noticing, that row 2 of the first matrix equals $s_2A$ and the same for row 3, and also noticing the results of equation 2, yields
## $$\left\{\begin{array}& s_1=s_2A\\s_2=s_3A\end{array}\right\}, \quad \left\{\begin{array}& s_1B=1 \\ s_2B=0 \\ s_3B=0 \end{array}\right\}$$
By combingin