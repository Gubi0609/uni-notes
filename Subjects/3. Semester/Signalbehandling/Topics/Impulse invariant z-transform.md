The analog impulse response can be achieved by using inverse Laplace transform of analog filter 𝐻𝐻 𝑠𝑠 .
![[Pasted image 20251106101801.png]]

Then we can sample this analog impulse response with a sampling interval T. T is also used as a scaling factor
![[Pasted image 20251106101840.png]]

![[Pasted image 20251106101851.png]]

Given a Nth order filter
![[Pasted image 20251106101949.png]]

We use partial fraction solution
![[Pasted image 20251106102007.png]]

where $s_i$ is the analog filter's pole.


## General Example
We have the transfer function
## $$H(s)=\sum^N_{i=1} \frac {k_i}{s-s_i} $$
We then use inverse Laplace transform
## $$h(t) = \mathcal{L}^{-1}[H(s)]=\sum^N_{i=1}k_ie^{s_it}$$
The impulse response of the digital filter then becomes
## $$h(n)=h(nT)=\sum^N_{i=1}k_ie^{s_inT}$$

Lastly we z-transform h(n)
![[Pasted image 20251106102502.png]]

> [!example]-
> ![[Pasted image 20251106102528.png]]
> **Efter at have taget partial fraction decomposition, mangler der et 'j' i den første nævner ved '3554.6'**

# Matlab code example

![[Pasted image 20251106103137.png]]


---
#signalprocessing 