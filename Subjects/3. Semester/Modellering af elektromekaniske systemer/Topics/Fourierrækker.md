
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
> ## $$\text{3.}\quad f(x)=\sum^\infty_{n=-\infty} c_n e^{jn\pi x/L}$$
> 
> hvor
> ## $$c_n=\frac 1 2 (a_n-jb_n),\quad \text{for } n>0$$
> ## $$\arg(c_n) = -\tan^{-1}(b_n/a_n)=-\phi_n$$
> hvor $\arg(c_n)$ er argumentet af $c_n$ 

> Fourierrækker bruges til at aproksimere _periodiske_ funktioner, der har perioden $2L$ 

For ikke-periodiske systemer se enten [[Taylorrækker]] eller [[Fouriertransformation]].

---
Det kan ses via dette spektrum, at $A_n$ bliver mindre, desto større $n$ bliver. Dette betyder at $A_n$ påvirker signalet mindre og mindre
![[Pasted image 20260108122124.png]]

> [!example]- Fourierrække af trekant-funktion
> ![[Pasted image 20260108123202.png]]
> ![[Pasted image 20260108123215.png]]
> Vi kan se, at desto større $N$, desto nærmere den originale funktion er vi