
![[Pasted image 20251106091511.png]]
![[Pasted image 20251106091522.png]]

# Design of digital IIR filter
An IIR filter is designed by following the procedure
1. The filter's specifications are drawn up (analog filter) (This is in the s-domain)
2. Convert the analog filter to digital filter: z-domain transfer function is made
3. Choose a realization structure
4. Implement the design through program or hardware

## Transformation from analog prototype filter
![[Pasted image 20251106085715.png]]

We transform from **s-domain** to **z-domain**
In this process we transfer the **poles** and **zeros** from the s-plane to the z-plane. This will give a similar filter response
![[Pasted image 20251106091430.png]]

# Realization
![[Pasted image 20251106103105.png]]



---
#signalprocessing #filter