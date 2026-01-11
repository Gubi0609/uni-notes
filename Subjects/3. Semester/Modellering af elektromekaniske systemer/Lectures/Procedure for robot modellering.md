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
## $$T_n^0(\mathbf q)=A_1(q_1)\cdot A_2(q_2)\cdot ...\cdot A_n(q_n)=\begin{bmatrix}R_n^0(\mathbf q)&\mathbf o_n^0(\mathbf(q)\\\end{bmatrix}$$