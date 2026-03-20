Electromechanical systems have saturation on their physical variables.
- The output of any actuator is limited from above and below
- This creates _clipping_
![[Pasted image 20260320084947.png]]

The saturation must be taken into account, when _integral action_ is present in the controller.
![[Pasted image 20260320085057.png]]
- We can see that the output for the system _with saturation_ reaches a higher peak, because the regulator is limited at _1_.

If a setpoint is given to the system, that cannot be reached, then the integrator winds up, and a delay is experienced when changing the setpoint value
- Therefore, it is important to only give a system _reachable references_
![[Pasted image 20260320085315.png]]

We can use _two anti-windup mechanisms_
- **Back-Calculation**
- **Conditional Integration**
Both methods utilize the following signal
![[Pasted image 20260320085434.png]]

# Back-Calculation
This recomputes the integral term when the system input is saturated, as shown below (on a PID regulator)
![[Pasted image 20260320085542.png]]

The value of the integrator output is not changed instantaneously, but it is changed based on the **tracking time constant** $T_t$.

The input of the integrator is given by
## $$ \frac 1 {T_t}e_s+\frac {K_p}{T_i}e$$
where $e_s$ is zero when the system is not saturated.
In steady state, the ouytput of the integrator is constant; therefore its input must be zero
## $$e_s = -\frac {K_pT_t}{T_i}e$$
in steady state
![[Pasted image 20260320085948.png]]

# Conditional Integration
This is also known as _clamping_. It is a bit simpler than back-calculation, and just stops integrating when the system is in saturation
![[Pasted image 20260320090037.png]]

Although it is simple, it still improves the performance of the system
![[Pasted image 20260320090103.png]]

**It is beneficial to use conditional integration in 9/10 cases, as it is simple, yet effective**