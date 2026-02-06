We work with a transfer function
## $$G(s)=\frac {Q(s)}{P(s)}$$
Where $Q$ and $P$ are polynomials in the variable $s$.
- The roots of $Q(s)$ are called the _zeros_
- The roots of $P(s)$ are called _poles_

We assume that the degree of $P(s)$ is higher than that of $Q(s)$.

To convert from [[Time Domain Models]] we _Laplace transform_ our function.
![[Pasted image 20260206094346.png]]

# [[Time Domain Models#Continuous time state space|State Space Models]] to Transfer Function
![[Pasted image 20260206094433.png]]
When we rearrange, we want to _collect all_ $x(s)$ on one side.

![[Pasted image 20260206094449.png]]
When we invert (in step one of this picture) we assume, that we are not _at the poles_ since the matrix would not be invertable for that position.

> [!example]- 
> ![[Pasted image 20260206094535.png]]
> ![[Pasted image 20260206094545.png]]
> The values for the matrices are obtained from [[Time Domain Models]].
> When we invert in picture 2, we actually also divide by the matrix's determinant.

