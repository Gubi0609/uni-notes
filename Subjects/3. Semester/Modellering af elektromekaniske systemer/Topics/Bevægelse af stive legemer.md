[[Partikelsystemer#Massemidtpunktssætningen|Massemidtpunktssætningen]] bruges til at finde massemidtpunktets bevægelse
## $$M\mathbf a_C=\mathbf F_{net}=\sum \mathbf F_{ext}$$
[[Impulsmoment og kraftmoment#Impulsmomentsætningen|Impulsmomentsætningen]] i $z$-retningen kan benyttes til beskrivelse af roterende bevægelse i planen
## $$\frac {dL_z} {dt}=\tau_z\quad \text{[Nm]}$$
hvor $L_z$ er impulsmomentet og $\tau_z$ er kraftmomentet

Vi benytter dog ofte massemidtpunktet $C$ som referencepunkt
## $$\frac {dL_{C,z}} {dt}=\tau_{C,z}\quad \text{[Nm]}$$
# Inertimoment
Inertimomentet i z-aksens retning er defineret som
## $$I_z=\sum_im_iR_i^2=\int R^2dm=\int R^2\rho dV$$
hvor $R_i$ er radius ud til den givne partikel fra rotations aksen, $\rho$ er densiteten af objektet.

> [!example]- Eksempel på udledning af intertimoment
> ![[Pasted image 20260110160936.png]]
> ![[Pasted image 20260110160944.png]]

# Impulsmoment
Vi har allerede ligninger for [[Impulsmoment og kraftmoment|impulsmomentet]], men vi kan nu også beskrive det ud fra [[Bevægelse af stive legemer#Inertimoment|inertimomentet]]
## $$L_z=I_z\omega$$
Hvor $I_z$ er inertimomentet om en linje gennem punktet parallel med rotationsaksen

eller
## $$L_z=I_{C,z}\omega+(\mathbf r_C\times\mathbf P)_z$$
hvor $\mathbf P$ er systemets samlede impuls

# Rotationel dynamik
Den rotationelle dynamik for et stift legeme er så
## $$I_z \dot \omega=\tau_z\quad\text{eller}\quad I_{C,z}\dot\omega=\tau_{C,z}$$
> [!example]- Eksempel: Bevægelse af stift legeme
> ![[Pasted image 20260110161458.png]]
> ![[Pasted image 20260110161511.png]]

# Steiners sætning
> [!note] Steiners sætning
> Lad $\mathbf z_C$ være en akse, der går i gennem massemidtpunktet og $\mathbf z$ være parallel med $\mathbf z_C$. Så er inertimomentet om $z$-aksen
> $$I_z=I_C+Ml^2$$
> hvor $M$ er massen af legemet, $l$ er afstanden mellem $\mathbf z$ og $\mathbf z_C$, og $I_C$ er inertimomentet om $\mathbf z_C$-aksen $\text{[kgm}^2\text{]}$.

> [!example]- Udledning af Steiners sætning
> ![[Pasted image 20260110184033.png]]
> Betragt et legeme, der roterer omkring $z$-aksen og _ikke_ $z_C$-aksen. Legemets [[Subjects/3. Semester/Modellering af elektromekaniske systemer/Topics/Kinetisk Energi|kinetiske energi]] bliver så
> $$E_{kin}=\frac 1 2 I_z\omega^2$$
> hvor $I_x$ er inertimomentet om $z$-aksen.
> 
> [[Partikelsystemer#Massemidpunktet|Massemidtpunktets]] fart er
> $$v_C=l\omega$$
> hvor $l$ er længden mellem $z$ og $z_C$.
> 
> Den kinetiske energi kan derfor også skrives
> $$E_{kin}=\frac 1 2 M(l\omega)^2+\frac 1 2I_C\omega^2$$
> (Se [[Subjects/3. Semester/Modellering af elektromekaniske systemer/Topics/Kinetisk Energi#Roterende og translatorisk bevægelse|Kinetisk Energi for roterende og translatoriske bevægelser]])
> 
> Fra
> $$E_{kin}=\frac 1 2 I_z \omega^2=\frac 1 2 M(l\omega)^2+\frac 1 2 I_C\omega^2$$
> konkluderes det at
> $$I_z=I_C+Ml^2$$
> hvilket er Steiners sætning.

---
#physics #kinematics