![[Pasted image 20260220084053.png]]
For an open loop system as the above, we want to chose $D(s)$ so that our output $y(s)$ is as close to the input $r(s)$ as possible. For this to be true, we must choose $D(s)$ as follows
![[Pasted image 20260220084151.png]]

# Steady-State Value of Time Function
![[Pasted image 20260220084252.png]]

## Final Value Theorem
If all poles of $sY(S)$ are in the _open left half_ of the $s$-plane then
## $$\lim_{t\rightarrow \infty}y(t)=\lim_{s\rightarrow 0}sY(s)$$
This is called the **Final Value Theorem**, which determines the constant value that the impulse response of a stable system converges to.

The reason that we now have $sY(s)$ instead of $Y(s)$, is that we have integrated $Y(s)$.
- E.g. if our input is an impulse-response, we want to go to a step-response. This is done by integration.

The Final Value Theorem can also be used to determine the **DC gain** of a system (i.e. the output when a step input is applied to the system)
## $$\lim_{s\rightarrow\infty}sG(s)\frac 1 s =\lim_{s\rightarrow 0}G(s)$$

# Disturbance
![[Pasted image 20260220085634.png]]
## $$y(s)=G(s)d(s)+G(s)D(s)r(s)$$
This is not very good, as we can not minimize the disturbance. Thus we instead use [[Closed loop system]]