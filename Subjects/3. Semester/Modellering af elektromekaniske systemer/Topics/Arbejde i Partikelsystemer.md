Vi har _to koordinatrammer_
1. **L-systemet:** koordinatrammen er fast i forhold til _Jorden_.
2. **C-systemet:** koordinatrammen er fast i forhold til _massemidtpunktet af partikelsystemet_.

# C-systemet
I C-systemet er stedvektor $\mathbf r'$ og hastighedsvektor $\mathbf v'$. Følgende gælder
## $$\sum m_i\mathbf r_i'=0\quad\text{og}\quad\sum m_iv_i'=0$$
## Arbejdssætningen
[[Subjects/3. Semester/Modellering af elektromekaniske systemer/Topics/Arbejde#Arbejdssætningen|Arbejdssætningen]] for den $i$'te partikel giver
## $$\Delta E_{kin,i}=W_{ext,i}+W_{int,i}\quad\text{[J]}$$
hvor $W_{ext,i}$ er de eksterne krafter på partikel $i$, og $W_{int,i}$ er de interne krafter.

For [[Partikelsystemer|partikelsystemet]] gælder således
## $$\Delta E_{kin}=W_{ext}+W_{int}\quad\text{[J]}$$
Hvis partikelsystemet er et _stift legemet_, vil de indbyrdes afstande være konstante, hvilket medfører at $W_{int}=0\text{ J}$. Dermed bliver det
## $$\Delta E_{kin}=W_{ext}\quad\text{[J]}$$

Hvis både interne og eksterne krafter er [[Konservative og ikke-konservative krafter#Konservative krafter|konservative]], gælder
## $$W_{ext}+W_{int}=E_{pot,ext,A}+E_{pot,int,A}-E_{pot,ext,B}-E_{pot,int,B}$$ $$W_{ext}+W_{int}=\Delta E_{pot,ext}+\Delta E_{pot,int}$$
# L-systemet
Hastigheden af partikel $i$ i **L-systemet** kan skrives
## $$\mathbf v_i=\mathbf v_C+\mathbf v_i'$$
Den [[Subjects/3. Semester/Modellering af elektromekaniske systemer/Topics/Kinetisk Energi|kinetiske energi]] af [[Partikelsystemer|partikelsystemet]] udtrykt i L-systemet er
## $$E_{kin}=\sum_i\frac 1 2m_i(\mathbf v_C+\mathbf v_i')^2$$$$E_{kin}=\sum_i\frac 1 2m_i(v_C^2+{v_i'}^2+2\mathbf v_C\cdot\mathbf v_i')$$$$E_{kin}=\frac 1 2 \sum_i m_iv_C^2+\frac 1 2\sum_im_i{v_i'}^2+\mathbf v_C\cdot\sum_im_i\mathbf v_i'$$
Vi kan nu se følgende:
## $$\frac 1 2 \sum_i m_i v_C^2\rightarrow E_{kin,ext}$$$$\frac 1 2 \sum_i m_i {v_i'}^2\rightarrow E_{kin,int}$$$$\mathbf v_C\sum_i m_i \mathbf v_i'=0$$
Det sidste gælder, da vi kan kigge tilbage på egenskaberne for [[Arbejde i Partikelsystemer#C-systemet|C-systemet]].

Endeligt kan det skrives
## $$E_{kin}=\frac 1 2 \sum_i m_iv_C^2+\frac 1 2\sum_im_i{v_i'}^2=E_{kin,ext}+E_{kin,int}$$