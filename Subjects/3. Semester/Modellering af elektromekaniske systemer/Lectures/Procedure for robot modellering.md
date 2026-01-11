Følgende procedure anvendes til dynamisk modellering af en robot med $n$ frihedsgrader
0. Find robottens DH-parametre $(a_i,d_i,\alpha_i,\theta_i)$ for $i=1,2,...,n$.
1. Opstil en kinematisk model $T_n⁰(\mathbf{q})$ for robotten
2. Udregn koordinaterne $\mathbf{p}_{ci}^0(q)$ for massemidtpunkterne for hvert link (beskrevet i Base rammen)
3. Udregn vinkelhastighederne $\mathbf\omega_i^0(\mathbf{q},\dot{\mathbf{q}})$. for hvert link (beskrevet i Base rammen)
4. Udregn hastighederne $\mathbf v_{ci}^0(\mathbf{q},\dot{\mathbf{q}})$ for massemidtpunkterne for hvert link (beskrevet i Base rammen)
5. Udregn inertitensor $I_{li}^0(\mathbf{q})$ for hvert link (beskrevet i Base rammen)
6. Udregn systemets potentielle energi $E_{pot}(\mathbf q)$
7. Udregn systemets kinetiske energi $E_{kin}(\mathbf q, \dot{\mathbf q})$
8. Opstil bevægelseslignignerne for systemets ud fra Lagrange D'Alamberts princip.