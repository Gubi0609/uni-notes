
# Design process
1. Determine the analog filter's transfer function $𝐻(𝑠)$.
2. Determine the analog filter’s poles and zeros.
3. Convert the **poles** in s-domain to z-domain
4. Determine the coefficients of the digital transfer function. The numerator may be modified to have $𝐻(𝑧 = 1)=1$
5. Implement the transfer function as a **cascade structure**.

With matched z-transform, the **poles** and **zeros** of the prototype filter are transferred directly to the z-domain using the following
![[Pasted image 20251106091738.png]]
![[Pasted image 20251106091756.png]]

# Matched z-transform for 1st order system

A 1st order tranfer function with 1 zero is given by
![[Pasted image 20251106092209.png]]

Where $\sigma _1 = -A_0$ is a real **zero** and $\sigma_2=-B_0$ is a real **pole**
When using matched z-transformation, the zero and the pole can be calculated as
## $$z_1=e^{s_1T}=e^{\sigma_1T}\quad\text{and}z_2=e^{s_2T}=e^{\sigma_2T}$$
![[Pasted image 20251106092443.png]]

A digital 1st order filter based on matched z-transform then has the form
![[Pasted image 20251106092527.png]]

We now consider a 1st order system with no zero
![[Pasted image 20251106092600.png]]

This only has one **pole** and can be converted to the following (z-transform)
![[Pasted image 20251106092626.png]]

where $\sigma_1$ is the pole of H(s) and T is the sampling interval.

## Amplification factor
![[Pasted image 20251106092708.png]]
![[Pasted image 20251106093003.png]]

> [!example]- Eksempel
> ![[Pasted image 20251106093031.png]]
> ![[Pasted image 20251106093041.png]]
> ![[Pasted image 20251106093049.png]]

# Matched z-transform for higher order system
For a higher order system with complex conjugate pole and zero pair, the transfer function can be written after
factorization
![[Pasted image 20251106094712.png]]
Normally, a **cascade structure** is used for the realization when matched z transform method is used.

> [!example]- Eksempel: 2nd order system
> ![[Pasted image 20251106094751.png]]
> ![[Pasted image 20251106094801.png]]
> ![[Pasted image 20251106094810.png]]

## Matlab function
### `Hz=c2d(Hs, Ts, method)`
'`c2d`' stands for _Continuous To Discrete_
![[Pasted image 20251106094911.png]]

> [!example]- Eksempel: Matlab
> ![[Pasted image 20251106094954.png]]



---
#signalprocessing 