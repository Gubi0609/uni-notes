
# Krav
Måleområde: 0 - 240 g\*cm
Udgangsignal: 0 - 10 V
Måle modstand: 100 m$\Omega$

Buzzer skal hyle ved overstigning af torque på 150 g\*cm

# Forstærkning
Ud fra motorens datasheet, kan aflæses strøm ved hver torque. Det aflæses at strøm ved torque på 240 g\*cm (se krav) er
$$I_{\text{max}}=0.01098\cdot 240\text{ g*cm}=2.635\text{ A}$$

Voltage over shunten (som er vores målemodstand) kan nu udregnes ved denne strøm
$$V_{\text{shunt, max}}=I_{\text{max}}\cdot R_{\text{shunt}}=2.635\cdot0.1=0.2635$$


Formlen for at finde det nødvendige gain for en op amp er
$$A_{CL}=V_{\text{O, max}}/V_{\text{i, max}}=10V / 0.2635 V = 37,95$$