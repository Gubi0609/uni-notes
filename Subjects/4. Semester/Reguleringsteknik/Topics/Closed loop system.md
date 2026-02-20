![[Pasted image 20260220083152.png]]
For a system as the above, we input $r(s)$ and our output $y$ into the control system $K(s)$. This effectively means, that we input the _error_ $e=r-y$. This is passed forward to the _System_ $G(s)$. Our output will then be
## $$y(s)=G(s)\cdot K(s)\cdot e(s)$$ $$e(s)=r(s)-y(s)$$ $$y(s)=G(s)\cdot K(s) \cdot (r(s)-y(s)$$ $$(1+G(s)\cdot K(s))\cdot y(s) = G(s)\cdot K(s)\cdot r(s)$$ $$\frac {y(s)}{r(s)}=\frac {G(s)\cdot K(s)}{1+G(s)\cdot K(s)}$$

When our system is stable, it must have the _closed-loop poles_ in the open left half of the imaginary plane (se also [[Open Loop System#Steady-State Value of Time Function|Open Loop System]])

The **loop gain** is defined as $L(s)=G(s)\cdot K(s)$. The closed-loop poles are given by
## $$1+L(s)=0$$
The closed-loop poles then also satisfy
## $$L(s)=-1$$
In polar form, this would be
## $$1\angle{180\deg}\rightarrow 1\angle{\pi}$$
(But we apparently don't use radians in control...)

# Disturbance
![[Pasted image 20260220083457.png]]
We now insert a disturbance $d(s)$. The output $y(s)$ of the system is now
## $$y(s)=\frac {G(s)}{1+G(s)\cdot K(s)}\cdot d(s)+\frac {G(s)\cdot K(s)}{1+ G(s)\cdot K(s)}\cdot r(s)$$
When we _increase_ $K(s)$ we minimize the the disturbance and get closer and closer to the output being $y(s)=r(s)$.

> [!example]- Speed control of an engine
> ![[Pasted image 20260220090419.png]]

> [!example]- Open loop steady state error Vs. closed loop steady state error
> ![[Pasted image 20260220090552.png]]

## Measurement Noise
![[Pasted image 20260220092046.png]]
The output $y_m$ is given by (superposition can be applied for deriving the expression)
## $$y_m(s)=\frac {1}{1+G(s)\cdot K(s)}\cdot v(s)+\frac {G(s)\cdot K(s)}{1+ G(s)\cdot K(s)}\cdot r(s)$$

# Sensitivity Analysis
![[Pasted image 20260220092252.png]]
(same for [[Open Loop System]] but without feedback)

![[Pasted image 20260220092322.png]]
The sensitivity is nominated $S$.

# Linearization
![[Pasted image 20260220092513.png]]

## Linearization model
![[Pasted image 20260220093110.png]]

> [!example]- Linearization
> ![[Pasted image 20260220093656.png]]

