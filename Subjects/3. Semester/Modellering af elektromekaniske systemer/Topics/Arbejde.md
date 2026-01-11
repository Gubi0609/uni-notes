> Arbejde $W$ er energi overført til eller fra et objekt via en kraft, der virker på objektet. Energi der overføres _til_ objektet er positivt arbejde og energi der overføres  _fra_ objektet er negativ energi.

# Opsummering
> [!help] Arbejde
> Arbejde er defineret som
> $$W=\textbf F\cdot\mathbf d\quad\text{[J]}$$
> hvor $\mathbf F$ er kraftvektoren, og $\mathbf d$ er bevægelsesvektoren.

> [!help] Arbejde langs bane
> Arbejdet langs en _kort_ distance på banen er
> $$W=F_Tds\quad\text{[J]}$$
> hvor $F_T$ er kraften _langs_ bevægelsesretningen defineret som
> $$F_T=\mathbf F\cos\phi\quad\text{[N]}$$
> hvor $\phi$ er vinklen mellem kraften $\mathbf F$ og bevægelsesretningen $ds$.
> 
> Arbejde over _hele_ banen
> $$W=\int^B_A\mathbf F\cdot d\mathbf r\quad\text{[J]}$$

> [!help] Arbejdssætningen
> $$W_{AB}=\Delta E_{kin}=E_{kin,B}-E_{kin,A}\quad\text{[J]}$$

> [!help] Varierende kraft
> $$W=\int^{x_f}_{x_i}F(x)dx\quad\text{[J]}$$

> [!help] Arbejde for roterende bevægelse
> Arbejde for _kort_ distance af rotationen
> $$dW=F_Trd\theta=\tau_zd\theta\quad\text{[J]}$$
> 
> Gennemsnitligt arbejde for rotationen
> $$W=\tau(\theta_f-\theta_i)\quad\text{[J]}$$
> 
> Arbejde over _hele_ rotationen
> $$W=\int^{\theta_f}_{\theta_i}\tau(\theta)d\theta\quad\text{[J]}$$

---

En kraft $\mathbf{F}$ gør et **positivt** stykke arbejde, _når den peger i samme retning som bevægelsen af legemet_
Forskydningen kaldes $\mathbf{d}$.
![[Pasted image 20260110132352.png]]

En kraft $\mathbf{F}$ gør et **negativt** stykke arbejde, _når den peger i modsatte retning som bevægelsen af legemet_
Forskydningen kaldes $\mathbf{d}$.
![[Pasted image 20260110132435.png]]

En kraft $\mathbf{F}$ gør et **ikke noget** arbejde, _når den er vinkelret på bevægelsen af legemet_
Forskydningen kaldes $\mathbf{d}$.
![[Pasted image 20260110132530.png]]

# Arbejde
## $$W = \mathbf{F}\cdot\mathbf{d}\quad\text{[J]}$$
## Enhed
Enheden er _Joule_
## $$1 \text{ J}=1\text{ kgm}^2/\text{s}^2=1\text{ Nm}$$
# Arbejde langs bane
Arbejdet som kraften $\mathbf{F}$ udfører på partiklen til tiden $dt$ er
## $$dW=\mathbf{F}\cdot d\mathbf{r}=Fdr\cos{\phi}=F_Tdr=F_Tds\quad \text{[J]}$$
![[Pasted image 20260110132912.png]]

hvor $F_T$ er kraftens komposant langs banekurven, $\phi$ er vinklen mellem banekurven og kraften $\mathbf{F}$.

## Langs hele banen
Arbejdet udført på partiklen, når partiklen bevæger sig fra $A$ til $B$ er
## $$W_{AB}=\int^B_A\mathbf{F}\cdot d\mathbf{r}=\int^B_A(F_xdx+F_ydy+F_zdz)\quad\text{[J]}$$

# Arbejdssætningen
> Kræfternes arbejde på en partikel er lig tilvæksten i partiklens kinetiske energi.

Ovenstående kan omskrives til
## $$W_{AB}=\int^B_AF_T\cdot ds=\int^B_Am\frac {dv} {dt}ds=\int^B_Amvdv=\frac 1 2mv_B^2-\frac 1 2 mv_A^2$$
## $$W_{AB}=\Delta E_{kin}=E_{kin,B}-E_{kin,A}$$
Se [[Subjects/3. Semester/Modellering af elektromekaniske systemer/Topics/Kinetisk Energi|Kinetisk Energi]].

> [!example]- Arbejde udført af tyngdekraften
> Tyngdekraften kan ses [[Gængse kræfter#Tyngdekraften|her]].
> $$W_{g}=\Delta E_{kin,g}$$
> $$\Delta E_{kin,g}=\frac 1 2 mv^2_2 - \frac 1 2 mv^2_1=\frac m 2 \Delta v^2$$
> $$\Delta v^2=dg\cos\theta$$
> hvor $d$ er distancen bevæget, $g$ er tyngdeaccelerationen, og $\theta$ er vinklen mellem $\mathbf{F}_g$ og $\mathbf{d}$.
> $$W_g=mgd\cos\theta$$


# Varierende kraft
Arbejdet udført af en varierende kraft er
## $$W=\int^{x_f}_{x_i}F(x)dx$$
> [!example]- Fjederkraft
> Fjederkraften kan ses [[Gængse kræfter#Fjederkraft|her]].
> $$F_s=-kx$$
> $$W_s=\int^{x_f}_{x_i}F_sdx=-\frac k 2 (x_f^2-x_i^2)$$

# Arbejde udført af [[Impulsmoment og kraftmoment#Kraftmoment|kraftmoment]]
![[Pasted image 20260110185004.png]]

En kraft $\mathbf F$ angriver et legeme i afstanden $r$ fra massemidtpunktet

[[Impulsmoment og kraftmoment#Kraftmoment|Kraftmomentet]] har følgende formel
## $$\tau_z=rF_T$$
Og ud fra formlen for [[Subjects/3. Semester/Modellering af elektromekaniske systemer/Topics/Arbejde#Arbejde langs bane|arbejde langs bane]]
## $$dW=F_Tds$$
kan 
## $$ds=rd\theta$$ $$dW=F_Trd\theta=\tau_zd\theta\quad\text{[J]}$$
udledes.

Det gennemsnitlige arbejde over en cirkulær bane kan skrives
## $$W=\tau(\theta_f-\theta_i)\quad\text{[J]}$$

Hvis kraftmomentet er varierende, kan arbejdes beregnes som
## $$W=\int^{\theta_f}_{\theta_i}\tau(\theta)d\theta\quad\text{[J]}$$
