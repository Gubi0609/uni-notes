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

