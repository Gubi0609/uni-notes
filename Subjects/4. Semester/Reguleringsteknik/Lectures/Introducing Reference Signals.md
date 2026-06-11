Taking the block diagram
![[Pasted image 20260611161131.png]]

And adding a Reference Signal $N$ and $M$
![[Pasted image 20260611161152.png]]

Gets the following system
## $$\dot x=Ax+B(F\hat x+Nr)$$ $$y=Cx$$
with the **observer**
## $$\dot {\hat x}=A\hat x+BF\hat x+L(C\hat x-y)+Mr$$

Written out in full, this becomes
## $$\left[\begin{array}& \dot x \\ \dot{\hat x} \end{array}\right] = \left[\begin{array}& A & BF \\ -LC & A+BF+LC \end{array}\right]\left[\begin{array}&  x \\ {\hat x} \end{array}\right]+\left[\begin{array}& BN \\ M \end{array}\right]r$$ $$y = \left[\begin{array}& C & 0 \end{array}\right]\left[\begin{array}& x \\ {\hat x} \end{array}\right]$$

# Zeros of a State Space Model
A square system (same number of inputs as outputs) with a state space model o the form
## $$\dot x=Ax+Bu$$$$y=Cx+Du$$
has a zero with value $z\in\mathbb{C}$ only if
## $$\det\left(\left[\begin{array}& A-zI & B \\ C & D\end{array}\right]\right)=0$$
## Zeroes of Closed Loop System
For a closed loop system this expands to
## $$\det\left(\left[\begin{array}& A_{CL}-zI & B_{CL} \\ C_{CL} & D_{CL}\end{array}\right]\right)=0$$$$\det\left(\left[\begin{array}& A-zI & BF & BN \\ -LC & A+BF+LC-zI & M \\ C & 0 & 0\end{array}\right]\right)=0$$ $$\det\left(\left[\begin{array}& A-zI & BF-BNN^{-1}F & BN \\ -LC & A+BF+LC-zI & M \\ C & 0 & 0\end{array}\right]\right)=0$$