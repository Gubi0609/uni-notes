We consider two types of compensators
- **Lead Compensation:** Approximates the PD control
	- Lowers the rise time and decreases the overshoot
- **Lag Compensation:** Approximates the PI control
	- Improves the steady state tracking

Both are given by the transfer function
## $$D(s) = K\frac {s+z}{s+p}$$

- If $z<p$ then $D(s)$ is called a _lead compensation_
- If $z>p$, then $D(s)$ is called a _lag compensation_

# Lead Compensator
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
## $$\omega_{max}=\frac 1 {T\sqrt{\alpha}}=\sqrt{|z||p|}$$
and
## $$\sin\phi_{max}=\frac {1-\alpha}{1+\alpha}$$

![[Pasted image 20260320092332.png]]

## Design procedure
![[Pasted image 20260320092351.png]]
![[Pasted image 20260320092408.png]]

> [!example]-
> ![[Pasted image 20260320092428.png]]
> ![[Pasted image 20260320092438.png]]
> ![[Pasted image 20260320092445.png]]
> ![[Pasted image 20260320092457.png]]
> ![[Pasted image 20260320092505.png]]
> ![[Pasted image 20260320092512.png]]


# Lag Compensator
Is given by
## $$D(s)=K\frac {s+z}{s+p}$$
where $z>p\in\mathbb{R}$ and $\alpha>1$

The transfer function $D(s)$ has a pole followed by a zero, and approximates a PI controller, when used as a feedback controller
![[Pasted image 20260320093539.png]]

**Idea:** Improve the steady-state performance without affecting the other dynamics
![[Pasted image 20260320093617.png]]

## Design procedure
![[Pasted image 20260320093632.png]]

> [!example]-
> ![[Pasted image 20260320093653.png]]
> ![[Pasted image 20260320093704.png]]
> ![[Pasted image 20260320093715.png]]

