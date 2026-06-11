> If a model of the system plant is not available, then the controller should be tuned by only studying the input-output behavior of the system

# Zeigler-Nichols
Zeigler and Nichols have two methods for tuning PID controllers without explicit use of a plant model

## Zeigler-Nichols tuning based on step response
The considered system is assumed to have the transfer function
## $$\frac {y(s)}{u(s)}=\frac A {\tau s+1}e^{-st_d}$$
where $t_d=L$ is the time delay of a first order system (the $L$ will be used later on), $A$ is the top of the step response (amplitude) and $\tau$ is the time from when the tilt of the step response hits $y=0$ to the time it hits $y=A$
![[Pasted image 20260610152912.png]]

By using the Zeigler-Nichols tuning methid, a closed loop system is obtained that has a decay ratio of ~$0.25$ (damping ratio $\zeta \approx 0.21$)
![[Pasted image 20260610153038.png]]

### Parameters
The parameters for the PID controller
## $$u(s)=K_p\left(1+\frac 1 {sT_i} + T_ds\right)e(s)$$
are given by
![[Pasted image 20260610153139.png]]

Where $R=A/\tau$.

> [!example]- Zeigler-Nichols tuning: Example
> ![[Pasted image 20260610153215.png]]
> ![[Pasted image 20260610153225.png]]
> ![[Pasted image 20260610153236.png]]
> ![[Pasted image 20260610153249.png]]
> As can be seen, by fine-tuning the result a bit, a much more clean system is achieved.

## Zeigler-Nichols tuning - The Ultimate Sensitivity method
An alternative to studying the step response is to connect a P-controller to the system, and increase the gain $K_p$ until the output oscillates.
![[Pasted image 20260610153549.png]]

The value of $K_p$ when the output oscillates with a constant amplitude is called the **ultimate gain** $K_u$. The period of oscillation $P_u$ is called the **ultimate period**.

### Parameters
The parameters for the PID controller
## $$u(s)=K_p\left(1+\frac 1 {sT_i} + T_ds\right)e(s)$$
are given by
![[Pasted image 20260610153733.png]]

> [!example]- Zeigler-Nichols Tuning (USM): Example
> ![[Pasted image 20260610153806.png]]
> ![[Pasted image 20260610153815.png]]
> As with [[Tuning PID controller#Zeigler-Nichols tuning based on step response|Zeigler-Nichols tuning based on step response]], the result needs fine tuning.

