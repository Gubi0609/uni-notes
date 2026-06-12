Anti windup is a **MUST** when working with [[Integral Control 1|Integral Control 1]] as accumulation over time can lead to unwanted behavior. Anti windup introduces a saturation point, where the data cannot accumulate anymore.
![[Pasted image 20260611154131.png]]

This is seen by the anti windup blocks on the black and orange entry points (so from $F\hat x$).

To choose how the system behaves while _in saturation_ we can introduce a _saturation matrix_ $M$
![[Pasted image 20260611154252.png]]

Since $M$ finds the difference between $F\hat x$ before saturation control and after saturation control, the difference will be 0, until the system reaches saturation whereupon the unsaturated $F\hat x$ is larger than the saturated $F\hat x$.

![[Pasted image 20260611154420.png]]
While in saturated state, since the output cannot change further, because we have reached $u_{max}$, the system is actually _open loop_. We use the $M$ matrix to try and return the system to closed loop.

# Designing Saturation Gain
Dynamics of a controller during saturation is given by
## $$\dot{\hat x}=A\hat x+LC\hat x+MF\hat x$$
or
## $$\dot{\hat x}=(A+LC+MF)\hat x$$
Determining $M$ can be recognized as an observer gain design problem
## $$\dot{\hat x}=\left(\tilde A + \tilde L\tilde C\right)\hat x$$
with $\tilde A=A+LC$, $\tilde L=M$, and $\tilde C = F$, from which the unknown $\tilde L=M$ can be chosen to assign any desired poles to the saturated controller.