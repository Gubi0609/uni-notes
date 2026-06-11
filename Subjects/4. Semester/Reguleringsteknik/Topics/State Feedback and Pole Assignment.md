> [!help] Algorithm for Pole Assignment
> 1. Choose desired closed loop polynomial $$\det(\lambda I-(A+BF))=\lambda^n-a_{CL,1}\lambda^{n-1}-...-a_{CL,n}$$
> 2. Determine $T$ such that $A_c=T^{-1}AT$ and $B_c=T^{-1}B$ are in controllable canonical form.
> 3. Determine open loop polynomial  $$


---
For a state space model
## $$\dot x=Ax+Bu$$
a _state feedback_ is a feedback of the form
## $$u=Fx$$
Combining these equations, we obtain
## $$\dot x=Ax+BFx=(A+BF)x$$
Thus, the result of a state feedback is a system with a modified system matrix, and thus with _modified poles_.

For a _single input_ system in [[Subjects/4. Semester/Reguleringsteknik/Topics/Controllable Canonical Form#Transformation to Controllable Canonical Form|Companion form]], a state feedback takes a particular simple form
![[Pasted image 20260611120042.png]]

Applying the feedback $u=Fx$ with
## $$F_c=\left[\begin{array}& f_1 & f_2 & f_3\end{array}\right]$$
we then obtain
![[Pasted image 20260611120147.png]]

Notice, that the feedback matrix only affects the top row of $A_c$.

The characteristic polynomial has then been changed from (see [[Subjects/4. Semester/Reguleringsteknik/Topics/Controllable Canonical Form|Controllable Canonical Form]])
## $$\det(\lambda I-A_c)=\lambda^n-a_1\lambda^{n-1}-...-a_n$$
to
## $$\det(\lambda I-(A_c+B_cF_c))=\lambda^n-(a_1+f_1)\lambda^{n-1}-...-(a_n+f_n)$$
We can then, by choosing $f_1,...,f_n$ appropriately obtain _any closed loop pole configuration_.
This is known as **pole assignment**.