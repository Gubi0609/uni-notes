![[Pasted image 20260220083152.png]]
For a system as the above, we input $r(s)$ and our output $y$ into the control system $K(s)$. This effectively means, that we input the _error_ $e=r-y$. This is passed forward to the _System_ $G(s)$. Our output will then be
## $$y(s)=G(s)\cdot K(s)\cdot e(s)$$ $$e(s)=r(s)-y(s)$$ $$y(s)=G(s)\cdot K(s) \cdot (r(s)-y(s)$$ $$(1+G(s)\cdot K(s))\cdot y(s) = G(s)\cdot K(s)\cdot r(s)$$ $$\frac {y(s)}{r(s)}=\frac {G(s)\cdot K(s)}{1+G(s)\cdot K(s)}$$

# Disturbance
![[Pasted image 20260220083457.png]]
We now insert a disturbance $d(s)$. The output $y(s)$ of the system is now
## $$y(s)=\frac {G(s)}{1+G(s)\cdot K(s)}\cdot d(s)+\frac {G(s)\cdot K(s)}{1+ G(s)\cdot K(s)}\cdot r(s)$$
When we _increase_ $K(s)$ we minimize the the disturbance and get closer and closer to the output being $y(s)=r(s)$.