With a [[Frequency Domain Models#Time Domain Models Continuous time state space State Space Models to Transfer Function|transfer function]]
## $$G(s)=C(sI-A)^{-1}B+D$$
we have 
## $$G(s)\rightarrow infty\text{ for }s\rightarrow p\quad \Rightarrow\quad \det(pI-A)=0$$
Hence, $p$ is a pole for $G(S)\quad \Rightarrow\quad p$  is an eigenvalue for $A$.

> [!example]- Example - Mass-Spring-Damper
> ![[Pasted image 20260213093018.png]]
> Notice that the poles are easily found from the last form of the determinant, since we want it to equal 0. This only leaves $-1$ and $-2$ as options.
> ![[Pasted image 20260213093028.png]]
> ![[Pasted image 20260213093040.png]]
> ![[Pasted image 20260213093048.png]]
> We must choose the easiest way to calculate the determinant. We notice that the right column is 0, 1, 0, meaning that we can rule out two of the sub-determinants (since they would be multiplied by 0). Then we calculate the sub-determinant for 1 and multiply by $-1$, since the order is +, -, +, ...

