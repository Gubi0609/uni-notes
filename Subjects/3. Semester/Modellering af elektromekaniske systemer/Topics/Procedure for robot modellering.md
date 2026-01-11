Følgende procedure anvendes til dynamisk modellering af en robot med $n$ frihedsgrader
0. Find robottens DH-parametre $(a_i,d_i,\alpha_i,\theta_i)$ for $i=1,2,...,n$.
1. Opstil en kinematisk model $T_n⁰(\mathbf{q})$ for robotten
2. Udregn koordinaterne $\mathbf{p}_{ci}^0(q)$ for massemidtpunkterne for hvert link (beskrevet i Base rammen)
3. Udregn vinkelhastighederne $\mathbf\omega_i^0(\mathbf{q},\dot{\mathbf{q}})$. for hvert link (beskrevet i Base rammen)
4. Udregn hastighederne $\mathbf v_{ci}^0(\mathbf{q},\dot{\mathbf{q}})$ for massemidtpunkterne for hvert link (beskrevet i Base rammen)
5. Udregn [[Rotationale impulsmomenter|inertitensor]] $I_{li}^0(\mathbf{q})$ for hvert link (beskrevet i Base rammen)
6. Udregn systemets [[Subjects/3. Semester/Modellering af elektromekaniske systemer/Topics/Potentiel Energi|potentielle energi]] $E_{pot}(\mathbf q)$
7. Udregn systemets [[Subjects/3. Semester/Modellering af elektromekaniske systemer/Topics/Kinetisk Energi|kinetiske energi]] $E_{kin}(\mathbf q, \dot{\mathbf q})$
8. Opstil bevægelseslignignerne for systemets ud fra Lagrange D'Alamberts princip.

# 1. Kinematik
Den kinematiske model for robotten opstilles ud fra DH-parametrene $(a_i,d_i,\alpha_i,\theta_i)$ for $i=1,2,...,n$. Dette giver en koordinat transformation
## $$T_n^0(\mathbf q)=A_1(q_1)\cdot A_2(q_2)\cdot ...\cdot A_n(q_n)=\begin{bmatrix}R_n^0(\mathbf q) & \mathbf o_n^0(\mathbf(q)\\0 & 1\end{bmatrix}$$
hvor
## $$A_i=\begin{bmatrix}\cos(\theta_i)&-\sin(\theta_i)\cos(\alpha_i)&\sin(\theta_i)\sin(\alpha_i)&a_i\cos(\theta_i)\\\sin(\theta_i)&\cos(\theta_i)\cos(\alpha_i)&-\cos(\theta_i)\sin(\alpha_i)&a_i\sin(\theta_i)\\0&\sin(\alpha_i)&\cos(\alpha_i)&d_i\\0&0&0&1\end{bmatrix}$$
# 2. Koordinater for massemidtpunkter
Massemidtpunktet for link $i$ kan udregnes som
## $$\begin{bmatrix}\mathbf p_{ci}^0(\mathbf q)\\1\end{bmatrix}=T_i^0\begin{bmatrix}\mathbf p_{ci}^i\\1\end{bmatrix}$$
hvor $\mathbf p_{ci}^i$ er massemidtpunktet i ramme $i$ og $\mathbf p_{ci}^0$ er massemidtpunktet i ramme $0$ (Base rammen).

# 3. Vinkelhastigheder for massemidtpunkter
Vinkelhastigheden for massemidtpunktet af Link $i$ er
## $$\mathbf \omega_i^0=\mathbf \omega_{i-1}^0+R_{i-1}^0(\mathbf q)\mathbf \omega_{i-1,i}^{i-1}=\mathbf \omega_{i-1}^0+\mathbf\omega_{i-1,i}^0$$
hvor $\mathbf\omega_{i-1,i}^{i-1}$ er vinkelhastigheden af Ramme $i$ med hensyn til Ramme $i-1$ udtrykt i ramme $i-1$.

Eftersom vi benytter DH-parametre, er rotationen _altid_ omkring $z$-aksen (vi antager rotationelle led)
## $$\mathbf\omega_{i-1,i}^0=\mathbf z_{i-1}\dot q_i$$
hvor $\mathbf z_{i-1}$ er en enhedsvektor i $z$-aksen retning for Ramme $i-1$.

Vi får så **Jakobianten for orientering**.
## $$J_O^{li}=\begin{bmatrix}\mathbf z_0 & \mathbf z_1 & ... & \mathbf 0 & ... & \mathbf 0\end{bmatrix}$$

# 4. Hastigheder for massemidtpunkter
Fra [[Procedure for robot modellering#2. Koordinater for massemidtpunkter|punkt 2]] har vi koordinaterne for massemidtpunktet for link $i$.
## $$\mathbf p_{ci}^0=R_i^0(\mathbf q)\mathbf p_{ci}^i+\mathbf 0_i^0(\mathbf q)$$
Hastigheden for massemidtpunktet er dermed ($\mathbf p_{ci}^i$ er konstant)
## $$\mathbf v_{ci}^0(\mathbf q, \dot{\mathbf q})=\frac {d\mathbf p_{ci}^0(\mathbf q)}{dt}=\dot R_i^0(\mathbf q)\mathbf p_{ci}^i+\dot{\mathbf o}_i^0(\mathbf q)$$
Når DH parametre benyttes, kan hastigheden regnes (for rotationelle led) som **Jakobianten for position**
## $$\mathbf v_{ci}^0(\mathbf q, \dot{\mathbf q})=J_P^{li}\dot q$$
hvor
### $$J_P^{li}=\begin{bmatrix}\mathbf z_0\times(\mathbf p_{ci}-\mathbf p_0) &\mathbf z_1\times(\mathbf p_{ci}-\mathbf p_1) & ... & \mathbf z_{i-1}\times(\mathbf p_{ci}-\mathbf p_{i-1}) &\mathbf 0 & ... & \mathbf 0\end{bmatrix}$$
hvor $\mathbf p_k$ er positionsvektoren for origo af Ramme $k$.

# 5. Inertitensor i base rammen
Den såkaldte inertitensor $I_{l_i}$ givet i base rammen kan omformuleres ved vrug af en inertitensor, der ligger i ledets massemidtpunkt ($I_{l_i}^i$)
## $$I_{l_i}(\mathbf q)=R_i^0(\mathbf q)I_{l_i}^i{R_i^0}^T(\mathbf q)$$
# 6. Potentiel energi
Den [[Subjects/3. Semester/Modellering af elektromekaniske systemer/Topics/Potentiel Energi|potentielle energi]] skal udregnes i en inertiel ramme (fx. Base rammen), der ikke bevæges. Dermed kan den potentielle energi udregnes fra
## $$E_{pot}(\mathbf q)=\sum^n_{i=1}E_{pot,l_i}(\mathbf q) \quad\text{[J]}$$
hvor $E_{pot,l_i}$ er den potentielle energi for Link $i$.

Den _samlede_ potentielle energi bliver således
## $$E_{pot}(\mathbf q)=-\sum_{i=1}^nm_{l_i}\mathbf g_0^T\mathbf p_{ci}(\mathbf q)\quad\text{[J]}$$
hvor $m_{l_i}$ er massen af Link $i$, $\mathbf g_0$ er tyngdeaccelerationen i Base rammen, og $\mathbf p_{ci}(\mathbf q)$ er positionen for massemidtpunktet for Link $i$.

# 7. Kinetisk energi
Den [[Subjects/3. Semester/Modellering af elektromekaniske systemer/Topics/Kinetisk Energi|kinetiske energi]] skal udregnes i en inertiel ramme (fx. Base rammen), der ikke bevæges.
Dermed kan den kinetiske energi udregnes fra
## $$E_{kin}(\mathbf q, \dot{\mathbf q})=\sum_{i=1}^nE_{kin,l_i}(\mathbf q, \dot{\mathbf q}=\quad\text{[J]}$$
hvor $E_ {kin,l_i}$ er den kinetiske energi for Link $i$.

Den kinetiske energi for _Link $i$_ bliver således
### $$E_{kin,l_i}(\mathbf q,\dot{\mathbf q})=\frac 1 2 m_{l_i}\dot{\mathbf q}^T{J_P^{l_i}}^T(\mathbf q) J_P^{l_i}(\mathbf q)\dot{\mathbf q}+\frac 1 2\dot{\mathbf q}^T{J_O^{l_i}}^T(\mathbf q)R_i^0(\mathbf q)I_{l_i}^i{R_i^0}^T(\mathbf q)J_O^{l_i}(\mathbf q)\dot{\mathbf q}$$
hvor
## $$\frac 1 2 m_{l_i}\dot{\mathbf q}^T{J_P^{l_i}}^T(\mathbf q) J_P^{l_i}(\mathbf q)\dot{\mathbf q}\rightarrow\text{Translatoriske }E_{kin,l_i}$$
og
## $$\frac 1 2\dot{\mathbf q}^T{J_O^{l_i}}^T(\mathbf q)R_i^0(\mathbf q)I_{l_i}^i{R_i^0}^T(\mathbf q)J_O^{l_i}(\mathbf q)\dot{\mathbf q}\rightarrow\text{Rotationelle }E_{kin,l_i}$$
se [[Subjects/3. Semester/Modellering af elektromekaniske systemer/Topics/Kinetisk Energi|Kinetisk Energi]].
Den kinetiske energi for en robot, kan også skrives
## $$E_{kin}=\frac 1 2\dot q^TB(q)\dot q$$

# 8. Lagrange D'Alemberts princip
Lagrange D'Alamberts princip kan for $\mathbf q=\begin{bmatrix}q_1,&q_2,&...,&q_n\end{bmatrix}$ skrives
# $$\begin{matrix}\frac d{dt}\frac{\delta\mathcal L}{\delta\dot q_1}-\frac{\delta\mathcal L}{\delta q_1}=Q_1\\\frac d{dt}\frac{\delta\mathcal L}{\delta\dot q_2}-\frac{\delta\mathcal L}{\delta q_2}=Q_2\\...\\\frac d{dt}\frac{\delta\mathcal L}{\delta\dot q_n}-\frac{\delta\mathcal L}{\delta q_n}=Q_n\end{matrix}$$
se også [[Euler-Lagrange modellering#Ikke-konservative systemer|Euler-Lagra]]
hvor $Q_1,Q_2,...,Q_n$ er generaliserede krafter og $\mathscr L$ er _Lagrangian_ givet ved
## $$\mathscr L(\mathbf q, \dot{\mathcal q})=E_{kin}(\mathbf q, \dot{\mathcal q})-E_{pot}(\mathbf q)\quad\text{[J]}$$
hvor $E_{pot}$ er systemets potentielle energi og $E_{kin}$ er systemets kinetiske energi.
