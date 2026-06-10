A feedback controller is defined as
![[Pasted image 20260610135349.png]]

Which has the closed loop transfer function
## $$T_{CL}(s)=\frac {y(s)}{r(s)}= \frac {G(s)K(s)}{1+G(s)K(s)}$$
where $K(s)$ is the controller and $G(s)$ is the system model (plant). $r(s)$ is the reference, $y(s)$ is the output and $e(s)$ is the error between the reference and output. (Since there is feedback, the output doubles as the input via the feedback).

# Proportional Feedback Controller
A proportional feedback controller has the control law
## $$u(t)=K_pe(t)$$
where $K_P\in\mathbb{R}$ is the proportional gain.

The controller applies a control signal to the system, which depends linearly on the error.
![[Pasted image 20260610135805.png]]

The closed loop transfer function for this is then
## $$T_{CL}(s)=\frac {G(s)K_p}{1+G(s)K_p}$$

## Steady State Error
The DC gain of the closed loop system is given by the _Final Value Theorem_ ([[Subjects/4. Semester/Reguleringsteknik/Topics/Steady State Tracking|Steady State Tracking]])
## $$\frac {G(0)K_p}{1+G(0)K_p}$$
And the steady state error $e_{ss}$ is then given as (_for constant reference_ $r(s)=r$)
## $$e_{ss}=\left(1-\frac {G(0)K_p}{1+G(0)K_p}\right)r=\frac {1} {1+G(0)K_p}r$$
**From this we can see that $K_p$ should be large to decrease the steady state error.**

> [!example]- Proportional Feedback Control: Example
> ![[Pasted image 20260610143731.png]]
> ![[Pasted image 20260610143743.png]]
> We can see that a higher gain leads to a quicker rise time, but the settling time gets substantially worse. It is therefore not always better to choose a high gain. 
> We can also see that the input required increases for higher gains. If we have hardware constrictions, this is not good either.
> 
> ![[Pasted image 20260610143908.png]]
> We can see, that the poles approach the imaginary axis, as $K_p$ increases. _When the poles lie on the imaginary axis, the system has constant oscillation_.

## Proportional Control with Feedforward
We can eliminate the steady state error seen in the above example by introducing feedforward to the proportional controller. **This only works, if a perfect system model is known, and no disturbances are introduced to the system**.
## $$u(t)=K_pe(t)+u_{ff}$$
where the term $u_ff$ is called **reset**. The feedforward is chosen according to the DC gain of the system
## $$u(t)=K_pe(t)+\frac 1 {G(0)}r(t)$$
*The feedforward eliminates the steady state error if the dynamics of the system is perfectly known.*

> [!example]- Proportional Control with Feedforward: Example
> ![[Pasted image 20260610144527.png]]
> The poles of the system are not affected, as the feedforward only affects the numerator of the transfer function, and the poles are dependent on the denominator.

# Proportional-Integral Feedback Control
The control law of a proportional-integral feedback controller is
## $$u=K_pe+K_i\int_{t_0}^te(\tau)d\tau$$
As can be seen from the equation, the _integral_ term of the controller introduces an **integral gain** proportional to the integral of the error $e$.
![[Pasted image 20260610144802.png]]

**The integral action negates the use of a feedforward term, thus replacing it. This is useful when the perfect system model isn't known, and disturbances may be introduced.**

> Assuming that a closed loop system reaches steady state. Then the integral action removes the _steady state error_.

> [!example] Proof of removing steady state error
> Assume that there is a steady state error with $u=u_0$ and $e_0$. Then
> $$u_0=K_pe_0+K_ie_0t$$
> Which is a contradiction except if $e_0=0$ or $K_i=0$. 