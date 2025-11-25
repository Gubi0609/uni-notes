
# Kinematik
![[Pasted image 20251125133028.png]]

Vi definerer først DH-parametrene for robotten
![[Pasted image 20251125133101.png]]

Og ud fra DH notation, bliver hver koordinats transformation givet ved
![[Pasted image 20251125133134.png]]

Hvor $c_i$ og $s_i$ står for hhv. $\cos(\theta_i)$ og $\sin(\theta_i)$.


Massemidtpunktet for Link 1 i ramme 0 er
![[Pasted image 20251125133252.png]]
![[Pasted image 20251125133640.png]]

Vi ender med at bruge $l_{cl1}$ som er længden til massemidtpunktet (se illustration).

For massemidtpunktet for Link 2 i ramme 0 er proceduren ret meget det samme
![[Pasted image 20251125133801.png]]

![[Pasted image 20251125134348.png]]
![[Pasted image 20251125134400.png]]
**Det er vigtigt at bemærke, at vi stadig kun går ud til massemidtpunktet**.

![[Pasted image 20251125134718.png]]
![[Pasted image 20251125134827.png]]

# Potentiel energi
![[Pasted image 20251125135023.png]]
![[Pasted image 20251125135032.png]]

![[Pasted image 20251125135051.png]]
![[Pasted image 20251125135103.png]]

# Kinetisk energi
![[Pasted image 20251125135149.png]]

![[Pasted image 20251125135200.png]]
Vi finder $\dot{\textbf{p}_i}$ ved at kigge på jakobianten for det givne led således:

## $$\dot{\textbf{p}_{li}} = J_{pi}\dot{\textbf{q}}$$

![[Pasted image 20251125135213.png]]


![[Pasted image 20251125135223.png]]

![[Pasted image 20251125135233.png]]

![[Pasted image 20251125135904.png]]


# Dynamik
![[Pasted image 20251125135919.png]]

Det udtryk bliver til
## $$B(q)\ddot q+C(q,\dot q)+g(q)=\tau$$
## $$\ddot q = B^{-1}(q)(\tau-C(q,\dot q)\dot q-g(q))$$
Hvor $B(q)$ er matricen for kinetisk energi.


Hvis en ikke-konservativ kraft (eg. friktionskraft) skal tilføjes, tilføjes de på højre side af lighedstegnet fra før. Altså fx  $=\tau_1 + \text{ikke-konservativ kraft}$

Hvis en konservativ kraft (eg. fjederkraft) skal tilføjes, tilføjes de i $\mathscr{L}$. Mere specifikt i $E_{pot}$.