Fourier transform kan laves til laplace transform
## $$X(\omega)=\int^\infty_{-\infty} x(t)*e^{-j\omega t} dt \Rightarrow X(\sigma , \omega) = \int^\infty_{-\infty} [x(t)*e^{-\sigma t}]e^{-j\omega t} dt = \int^\infty_{-\infty} x(t)*e^{-(\sigma+j\omega) t} dt = \int^\infty_{-\infty} x(t)*e^{-st} dt, s = \sigma+j\omega$$
![[Pasted image 20251002082542.png]]

## S domain
s domænet er defineret ud fra $s = \sigma + j\omega$ hvor man har den reelle del ud af x-aksen og den imaginære del op af y-aksen
![[Pasted image 20251002083226.png]]
**Se også [[Z-transform]] for mere info om s-domænet.**


---
#signalprocessing  #laplace