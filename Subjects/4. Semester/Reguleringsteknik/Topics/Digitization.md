Most control systems are sample data systems, i.e., they consist of both _discrete_ and _continuous_ signals
![[Pasted image 20260327092902.png]]

> A **digital controller** both sample and quantize signals. In this course the quantization is omitted.
> Thus, **discrete controllers** are designed.

Two approaches to designing discrete controllers
- **Emulation:** Design continuous controller $K(s)$ and approximate it with $K(z)$ obtained via e.g. _Tustin's method_
- **Discrete design:** Design the 