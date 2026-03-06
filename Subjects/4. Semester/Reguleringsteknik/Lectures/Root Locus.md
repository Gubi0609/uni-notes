Is used for describing how the poles of $G(s)$ move around in the $s$-plane when the parameter _K_ changes
![[Pasted image 20260306082020.png]]

The Root Locus can be illustrated in matlab, and it will color coordinate the poles, to show how they will move.
![[Pasted image 20260306083010.png]]


![[Pasted image 20260306091212.png]]

We desicibe
## $$G(s)= \frac {Q(s)}{P(s)}$$
> [!example]- Example of root locus
> ![[Pasted image 20260306091313.png]]
> We want to put it in the standard form, and this is done through the two steps.

# Rule 1
There are $N$ lines (loci) where $N=\max(m,n)$.

> [!example]- Rule 1
> ![[Pasted image 20260306091558.png]]

# Rule 2
A $K$ increases from $0$ to $\infty$, the roots of the characteristic equation move from the poles of $G(s)$ to the zeros of $G(s)$

> [!example]- Rule 2
> ![[Pasted image 20260306091946.png]]

# Rule 3
When roots are complex they occur in conjugate pairs.
- Basically, if we have a pole, it has a "partner" on the other side of the real axis.

> [!example]- Rule 3
> ![[Pasted image 20260306092058.png]]

# Rule 4
The portion of the real axis to the left of an odd number of open loop poles and zeros are part of the loci.

> [!example]- Rule 4
> ![[Pasted image 20260306092218.png]]
> ![[Pasted image 20260306092225.png]]

