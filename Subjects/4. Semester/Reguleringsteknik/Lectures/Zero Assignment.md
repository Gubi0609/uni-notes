If $\tilde M$ is an _observer gain_ such that the characteristic polynomial of the matrix $A_{za}+\tilde MC_{za}$ is
## $$\det\left(sI-\left(A_{za} + \tilde MC_{za} \right) \right)=(s-z_1)...(s-z_n)$$
with $A_{za}=A+BF+LC$ and $C_{za}=-F$, then the numbers $z_1,...,z_n$ are all zeroes of the closed loop transfer function from $r$ to $y$.

# Algorithm for Zero Assignment
1. Design $\tilde M$ assigning zeroes close to the cut-off frequency of the Bode plot, such that the horizontal part is extended.
2. Compute $N$ such that the DC-value of the transfer function from $r$ to $y$ is unity  
## $$N=-\left(C_{CL}A_{CL}^{-1}\tilde B_{CL}\right)^{-1}$$
where
## $$A_{CL}=\left[\begin{array}& A & BF \\ -LC & A+BF+LC\end{array}\right], \quad \tilde B_{CL}=\left[\begin{array}& B \\ \tilde M\end{array}\right]$$
3. Compute $M=MN^{-1}N=\tilde MN$.