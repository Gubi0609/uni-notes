
# Krav
Måleområde: 0 - 240 g\*cm
Udgangsignal: 0 - 10 V
Måle modstand: 100 m$\Omega$

Buzzer skal hyle ved overstigning af torque på 150 g\*cm

# Forstærkning
Ud fra motorens datasheet, kan aflæses strøm ved hver torque. Det aflæses at strøm ved torque på 240 g\*cm (se krav) er
$$I_{\text{max}}=2.64\text{ A}$$

Voltage over shunten (som er vores målemodstand) kan nu udregnes ved denne strøm
$$V_{\text{shunt, max}}=I_{\text{max}}\cdot R_{\text{shunt}}=2.64\cdot0.1=0.264$$


Formlen for at finde det nødvendige gain for en op amp er
$$A_{CL}=V_{\text{O, max}}/V_{\text{i, max}}=10V / 0.264 V = 37,88$$

# Forstærker kredsløb
En differential forstærker er valgt, hvor der kigges på differensen over shunt modstanden
![[Pasted image 20260608100825.png|500]]

Hvis $R_1=R_2=R_{in}$ og $R_3=R_4=R_f$, er gain for kredsløbet
$$A_{CL}=R_f/R_{in}$$
Hvis $R_{in}= 10 \text{k}\Omega$ vælges, kan $R_f$ udregnes, da vi kender vores ønskede gain
$$R_f=37.88\cdot10\text{ k}\Omega=378.8\text{ k}\Omega$$

## Negativ feedback
Som også kan ses fra ovenstående diagram, vælges der negativ feedback. Dette stabiliserer gain markant 

# Op Amp
En **LM358A** op amp er valgt. Den har følgende karakteristika

| Parameter                     | Value      |
| ----------------------------- | ---------- |
| $V_{OS}$ input offset voltage | $\pm 3$ mV |
| $I_S$ Input bias current      | $-10$ nA   |
| $I_{OS}$ Input offset current | $0.5$ nA   |
| $A_{OL}$ Open loop gain       | $140$ V/mV |
| GBW Gain Bandwidth product    | 1.2 MHz    |
| SR Slewrate                   | 0.5 V/us   |
| $V_O$ voltage outpu           |            |
