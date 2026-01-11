Tilføjes en dæmpning til en [[Simpel harmonisk svingning|simpel harmonisk svingning]], kaldes det en **dæmpet simpel harmonisk svingning**.

Sådan en ligning er sammensat af [[Gængse kræfter#Fjederkraft|en fjederkraft]] og [[Gængse kræfter#Dæmpningskraft|en dæmpningskraft]].
## $$m\ddot x=-kx-b\dot x$$
Vi kan sammensætte nogle af variablerne, og skrive
## $$\ddot x+\gamma\dot x+\omega_0^2x=0$$
hvor $\gamma=b/m$ og $\omega_0^2=k/m$.

Denne ligning, har rødderne
## $$R=-\frac \gamma 2 \pm j\sqrt{\omega_0^2-\frac {\gamma^2}4}$$
hvor
## $$\omega_d=\sqrt{\omega_0^2-\frac {\gamma^2}4}$$
Der findes **tre** løsninger for rødderne
1. **Dæmpet svingning:** Når $\omega_0^2>\gamma^2/4\rightarrow \omega_d\in\mathbb{R}_+$  ([[2. ordens systemer#Underdæmpet|underdæmpet]])
2. **Aperiodisk grænsetilfælde:** Når $\omega_0^2=\gamma^2/4\rightarrow \omega_d=0$ ([[2. ordens systemer|kritisk dæmpet]])
3. **Aperiodisk svingning:** Når $\omega_0^2<\gamma^2/4\rightarrow\omega_d\in\mathbb{C}$ ([[2. ordens systemer|overdæmpet]])

# Dæmpet svingning
Løsningen til differentialligningen
## $$\ddot x+\gamma\dot x+\omega_0^2x=0$$
når $\omega_0^2>\gamma^2/4$ er
## $$x(t)=Ae^{R_{\text{real}}t}\cos(R_{\text{imag}}t+\phi)=Ae^{-\gamma t/2}\cos(\omega_dt+\phi)$$
![[Pasted image 20260111123651.png]]

hvor $Ae^{-\gamma t/2}$ bestemmer dæmpningen.

# Aperiodisk tilfælde
Løsningen til differentialligningen
## $$\ddot x+\gamma\dot x+\omega_0^2x=0$$
når $\omega_0^2=\gamma^2/4$ er
## $$x(t)=Ae^{R_{\text{real}}t}+Be^{R_{\text{real}}t}=Ae^{-\gamma t/2}+Be^{-\gamma t/2}$$
