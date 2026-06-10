> If a model of the system plant is not available, then the controller should be tuned by only studying the input-output behavior of the system

# Zeigler-Nichols
Zeigler and Nichols have two methods for tuning PID controllers without explicit use of a plant model

## Zeigler-Nichols tuning based on step response
The considered system is assumed to have the transfer function
## $$\frac {y(s)}{u(s)}=\frac A {\tau s+1}e^{-st_d}$$
where $t_d=L$ is the time delay of a first order system (the $L$ will be used later on), $A$ is the top of the step response (amplitude) and $\tau$ is the time from when the tilt of the step response hits $y=0$ to the time it hits $y=A$
![[Pasted image 20260610152912.png]]



## Zeigler-Nichols tuning - The Ultimate Sensitivity method