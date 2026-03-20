We consider two types of compensators
- **Lead Compensation:** Approximates the PD control
	- Lowers the rise time and decreases the overshoot
- **Lag Compensation:** Approximates the PI control
	- Improves the steady state tracking

Both are given by the transfer function
## $$D(s) = K\frac {s+z}{s+p}$$

- If $z<p$ then $D(s)$ is called a _lead compensation_
- If $z>p$, then $D(s)$ is called a _lag compensation_

# Lead compensator
Is given by
## $$D(s) = K\frac {s+z}{s+p}$$
where $z<p\in\mathbb{R}$
![[Pasted image 20260320092004.png]]

The bode plot for a lead compensator is
![[Pasted image 20260320092118.png]]

## Parameters
A lead compensation is given by
## $$D(s)=\frac {Ts+1}{\alpha Ts+1}\text{ where }\alpha<1$$

and $1/\alpha$ is called the _lead ratio_

We have
## $$\omega_{max}=\frac 1 {T\s}