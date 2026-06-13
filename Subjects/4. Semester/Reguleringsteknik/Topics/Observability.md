A continuous time system
$$\dot x(t)=Ax(t),\quad y(t)=Cx(t)$$
is said to be obeservable iff $y(t)\equiv 0 \Rightarrow x(t)\equiv 0$.

![[Pasted image 20260417082804.png]]

> [!example]- Condition for Observability for Discrete time system
> ![[Pasted image 20260417082851.png]]
> ![[Pasted image 20260417083022.png]]
> ![[Pasted image 20260417083030.png]]

![[Pasted image 20260417083030.png]]

> [!example]- Example: Series Connection
> ![[Pasted image 20260417083857.png]]
> ![[Pasted image 20260417083908.png]]
> ![[Pasted image 20260417083920.png]]
> ![[Pasted image 20260417083931.png]]

If the solution for observability is along the lines of $x_1=x_2$ we have a _zero-space_, where the two states _needs_ to be equal to each other, so we cannot really change and observe the system.

Just like we have a controlability matrix, we also have an **observability matrix** $\mathcal O$.