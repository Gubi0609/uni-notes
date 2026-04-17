For a system (seen in black) we can design an observer, if the system is [[Subjects/4. Semester/Reguleringsteknik/Topics/Observability|Observabel]]. The observer can be seen in red and yellow, where the red part is responsible for the $L$ of the observer.

![[Pasted image 20260417085014.png]]

> [!help] System:
> $$\dot x = Ax + Bu$$
> $$y = Cx$$

> [!help] Observer:
> $$\dot{\hat x} = A\hat x + B u + L(C\hat x - y)$$
> $$ y = C\hat x$$

**Notice, that _IDEALLY_ the A, B, and C matrices are the same for System and Observer. In reality, there may be a small error on the system, that thus requires adjusting of the matrices**

The error $e$ is
$$e=\hat x - x$$
Combining the equations, we get the equation for change in error
![[Pasted image 20260417085347.png]]

We notice, that both the output $y$ and input $u$ are not included in this expression. We already _know_ $u$, since that is the input, we input to the system ourself.

![[Pasted image 20260417085834.png]]

If the eigenvalues of the matrix $A+LC$ are 0, then the error $e$ converges towards 0.