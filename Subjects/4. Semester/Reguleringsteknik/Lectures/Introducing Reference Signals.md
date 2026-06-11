Taking the block diagram
![[Pasted image 20260611161131.png]]

And adding a Reference Signal $N$ and $M$
![[Pasted image 20260611161152.png]]

Gets the following system
## $$\dot x=Ax+B(F\hat x+Nr)$$ $$y=Cx$$
with the **observer**
## $$\dot {\hat x}=A\hat x+BF\hat x+L(C\hat x-y)+Mr$$

Written out in full, this becomes
## $$\left[\begin{array}& \dot x \\ \dot{\hat x} \end{array}\right] = \left[\begin{array}& A & BF \\ -LC & \end{array}\right]$$