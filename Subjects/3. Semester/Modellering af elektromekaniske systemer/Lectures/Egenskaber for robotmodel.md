En dynamisk model for en robot kan skrives på følgende form
## $$B(q)\ddot q+C(q,\dot q)\dot q+g(q)=\tau$$
Samme ligning ses også i [[Robot med to led (Euler-Lagrange model)]].
hvor $q$ er en vektor af $n$ generaliserede koordinater, $B(q)$ er masse-matrix, $C(q,\dot q)$ indeholder _Coriolis og centrifugal-led_, $g(q)$ er krafter der resulterer fra tyngdekraften, og $\tau$ er det kontrolerbare kraftmoment på _hvert led_.

# Kinetisk energi
Den [[Subjects/3. Semester/Modellering af elektromekaniske systemer/Topics/Kinetisk Energi|kinetiske energi]] for en robot kan skrives på følgende form'
## $$E_{kin}=\frac 1 2\dot q^TB(q)\dot q$$
# Coriolis og centrifugal-led
Matricen $C$ har elementer $c_{ij}$ som er givet ved
## $$c_{ij}=\sum_{k=1}^n c_{ijk}\dot q_k$$
hvor koefficienterne $c_{ijk$ kaldes _Christoffel sybols of the }first type_