We can create an [[Subjects/4. Semester/Reguleringsteknik/Topics/Full Order Observer|Observer]] based control system

![[Pasted image 20260417092003.png]]


> [!help] System:
> $$\dot x = Ax + Bu$$
> $$y = Cx$$

> [!help] Observer:
> $$\dot{\hat x} = A\hat x + B u + L(C\hat x - y)$$
> $$ y = C\hat x$$

> [!help] Feedback:
> $$u=F\hat x$$

The green feedback is in relation to [[L8 - Implementation]].

We then get an error and change in error
![[Pasted image 20260417092130.png]]

# The Separation Principle
![[Pasted image 20260417092244.png]]
![[Pasted image 20260417092249.png]]

Meaning that $F$ and $L$ can be designed _separately_.

> [!example]- Example: Observer Based Control
> ![[Pasted image 20260417092311.png]]
> ![[Pasted image 20260417092322.png]]
> ![[Pasted image 20260417092330.png]]

If we want to dominate the system, then when we place the poles (eigenvalues), we want to place them _further from the imaginary axis_.