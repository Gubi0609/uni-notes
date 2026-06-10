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