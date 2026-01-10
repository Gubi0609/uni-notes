Givet som
## $$E_{kin}=\frac 1 2 mv^2\quad \text{[J]}$$
Enheden er [[Subjects/3. Semester/Modellering af elektromekaniske systemer/Topics/Arbejde#Enhed|Joule]].
Vi antager at $v$ er betydeligt mindre end lysets hastighed.

# Partikelsystem
Den kinetiske energi for et partikelsystem i [[Arbejde i Partikelsystemer#L-systemet|L-systemet]] kan udtrykkes som
## $$E_{kin}=\sum_i\frac 1 2m_i(\mathbf v_C+\mathbf v_i')^2$$$$E_{kin}=\sum_i\frac 1 2m_i(v_C^2+{v_i'}^2+2\mathbf v_C\cdot\mathbf v_i')$$$$E_{kin}=\frac 1 2 \sum_i m_iv_C^2+\frac 1 2\sum_im_i{v_i'}^2+\mathbf v_C\cdot\sum_im_i\mathbf v_i'$$
Vi kan nu se følgende:
## $$\frac 1 2 \sum_i m_i v_C^2\rightarrow E_{kin,ext}$$$$\frac 1 2 \sum_i m_i {v_i'}^2\rightarrow E_{kin,int}$$$$\mathbf v_C\sum_i m_i \mathbf v_i'=0$$
Det sidste gælder, da vi kan kigge tilbage på egenskaberne for [[Arbejde i Partikelsystemer#C-systemet|C-systemet]].

Endeligt kan det skrives
## $$E_{kin}=\frac 1 2 \sum_i m_iv_C^2+\frac 1 2\sum_im_i{v_i'}^2=E_{kin,ext}+E_{kin,int}$$

# Roterende systemer
Vi kan kigge på $E_{kin,int}$ fra før
## $$E_{kin}=\frac 1 2 \sum_im_iv_i^2 \quad\text{[J]}$$
Hvis vi har en [[Plan bevægelse#Rotationel hastighed|roterende bevægelse]], bliver hastigheden i stedet skrevet
## $$E_{kin}=\frac 1 2 \sum_im_ir_i^2\omega^2 \quad\text{[J]}$$
hvor $\omega$ er vinkelhastigheden og $r_i$ er radius fra omdrejningsakse til partikel $i$.
Vi kan lave endnu en omskrivning, så vi i stedet bruger [[Bevægelse af stive legemer#Inertimoment|inertimomentet]].
## $$\sum_im_ir_i^2\rightarrow I_z$$$$E_{kin}=\frac 1 2I_z\omega^2$$
# Roterende og translatorisk bevægelse
Vi kan igen tage udgangspunkt i
## $$E_{kin}=E_{kin,ext}+E_{kin.int}$$
for blandet bevægelse

Den interne kinetiske energi bliver til den rotationelle del.
## $$E_{kin,int}=\frac 1 2 I_C\omega^2$$
Den eksterne kinetiske energi bliver således til den translatoriske del
## $$E_{kin,ext}=\frac 1 2\sum_im_iv_C^2$$