# Kraft
Vi antager, at det elektriske felt i DC motoren er nul, og udregner [[Lorentz kraft|Lorentz kraften]] på en _lille_ ladning $dq$, der er i det lille ledningstykke $ds$ i et magnetisk felt $\mathbf{B}$ som
## $$d\mathbf F=dq\mathbf v\times\mathbf B\quad\text{[N]}$$
**Størrelsen** af kraften, der påvirker en leder med længde $l$ i det magnetiske felt er
## $$F=Bil\sin(\alpha)\quad\text{[N]}$$
hvor $\alpha$ er vinkel imellem lederen og $\mathbf B$ i henhold til strømmens retning.

For en spole med en leder, vil vinklen $\alpha$ altid være $\pm \frac \pi 2$, dermed bliver størrelsen på kraften
## $$F=Bil\quad\text{[N]}$$
# Kraftmoment
[[Impulsmoment og kraftmoment#Kraftmoment|Kraftmomentet]] omkring center-aksen af spolen bliver dermed
## $$\tau=r\times F=2(Bil)\frac d 2\sin(\theta)$$
hvor $\theta$ er vinklen af spolen
![[Pasted image 20260114151545.png]]

Eftersom strømmens retning ændres hver halve omgang (pga kommutatoren), har kraftmomentet samme fortegn for alle værdier af $\theta$.
Hvis mange elementer indsættes i kommutatoren, kan en næsten konstant kraftmoment-profil opnås.
Derved bliver
## $$\tau=Bild=K_\Phi\Phi_i\quad\text{[Nm]}$$
hvor $K_\Phi=Bld$ (alle konstanterne) og $\Phi_i=i$ (variablen, strømmen).

![[Pasted image 20251118125425.png]]

# Elektromotorisk kraft
Den elektromotoriske kraft bestemmes ud fra [[Faradays induktionslov]]
## $$e=-\frac {d\Phi_c}{dt}\quad\text{[V]}$$
hvor $e$ er den elektromotoriske kraft.

Samt udtrykket for [[Biot Savarts lov#Magnetisk fluks i solenoid|fluks i solenoid]]
## $$\Phi(t)=BA\cos(\theta(t))\quad\text{[Wb]}$$
Dermed bliver den elektromotoriske kraft (**back emf**)
## $$e(T)=-\frac d {dt}(Ba\cos(\theta(t))=BA\sin(\theta(t))\omega(t)$$
![[Pasted image 20251118125538.png]]

# Egenskaber
Nu haves udtryk for motorens kraftmoment og spændingen over motoren (givet af den elektromotoriske kraft). Dermed kan følgende diagram anvendes til bestemmelse af motorens dynamik
![[Pasted image 20251118125738.png]]

Vigtigt at bemærke, at $b$ er friktionen.

## $$ \mu_a=R_aI_a+L_a \frac {dI}{dt} + K\omega$$
hvor
## $$ K\omega = emf$$

Vi kan også opstille følgende ligning for dynamikken af en DC motor.
## $$ I_m\dot\omega = kI_a-b\omega=\tau_m-b\omega$$
# Bestemmelse af parametre
Kan være nødvendigt da datablade enten ikke indeholder alle værdier vi skal bruge, eller fordi der kan være stor variation i parametrene for motorer af samme type.

![[Pasted image 20251118131310.png]]

De fire parametre K $R_a$ $\tau_c$ $b$ findes ved at måle spænding, strøm og omdejningshastighed ved to forskellige spændinger.
Af dette får vi
![[Pasted image 20251118131407.png]]

Parametrene kan bestemmes ved brug af mindste kvadraters metode ud fra de fire ligninger fra før.

**Hvis du nu blot kigger på de første målinger (to øverste rækker af venstre matrix), kan du se at som man rykker til højre i første række, passer det med hvad man ganger på parametrene (gående nedad) fra forrige ligninger. (for ubelastet motor) Så er de to første rækker i resultat vektor resultatet for ligningerne fra før.**

## Eksperimentel bestemmelse af $R_a$ og $L_a$
![[Pasted image 20251118132437.png]]

Det ovenstående er et første ordens system med overføringsfunktionen
![[Pasted image 20251118132535.png]]


![[Pasted image 20251118132934.png]]
For tidskonstanterne for elektrisk, mekanisk og termisk energi, vil tidskonstanten være _mindst_ for elektrisk, dernæst mekanisk og til sidst termisk.

Som eksempel:
Man skruer **meget** hurtigt på en radiator (mekanisk). Dette er en _lille_ tidskonstant. Der går dog lige nogle timer inden man kan se at den termiske energi for rummet har ændret sig. Dette er en _stor_ tidskonstant.

## Eksperimentel bestemmelse af inertimomentet $J$
![[Pasted image 20251118133012.png]]


# Gearing
![[Pasted image 20251118130121.png]]
![[Pasted image 20251118130133.png]]

Da der er den fjeder i mellem de to vinkler, er der mulighed for deformation. Det betyder også at der ikke bare er én frihedsgrad, da $\theta_j$ ikke er direkte afhængig af $\theta_m$.
$N_g$ er drivtoget (gearingen). Altså konstanten derfra, som vi ganger på.

---
#physics 