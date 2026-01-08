> [!help] Fourierrækker opsummeret
> ## $$\text{1.}\quad S_N(x)=\frac{a_0} 2 + \sum^N_{n=1}(a_n \cos(n\pi x/L)+b_n \sin(n\pi x/L)$$
> ## $$\text{2.}\quad S_n(x)= A_0 + \sum^\infty_{n=1} A_n \cos(n\pi x/L - \phi_n)$$
> 
> hvor
> ## $$a_n=\frac 1 L \int^L_{-L} f(x) \cos(n\pi x/L)dx, \quad n\geq 0$$
> ## $$b_n=\frac 1 L \int^L_{-L} f(x) \sin(n\pi x/L)dx, \quad n>0$$
> ## $$A_n=\sqrt{(a_n^2+b_n^2)}$$
> ## $$\phi_n=\tan^{-1}(b_n/a_n)$$


> [!help] Komplekse fourierrækker opsummeret
> ## $$f(x)=\sum^\infty_{n=-\infty} c_n e^{jn\pi x/L}$$
> 
> hvor
> ## $$c_n=\frac 1 2 (a_n-jb_n),\quad \text{for } n>0$$

> Fourierrækker bruges til at aproksimere _periodiske_ funktioner, der har perioden $2L$ 

For ikke-periodiske systemer se enten [[Taylorrækker]] eller 

---
Det kan ses via dette spektrum, at $A_n$ bliver mindre, desto større $n$ bliver. Dette betyder at $A_n$ påvirker signalet mindre og mindre
![[Pasted image 20260108122124.png]]
