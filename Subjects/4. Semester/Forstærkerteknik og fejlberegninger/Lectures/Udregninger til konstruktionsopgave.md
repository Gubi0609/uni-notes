
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

| Parameter                                       | Value       |
| ----------------------------------------------- | ----------- |
| $V_{OS}$ input offset voltage                   | $3$ mV      |
| $I_S$ Input bias current                        | $-20$ nA    |
| $I_{OS}$ Input offset current                   | $2$ nA      |
| $A_{OL}$ Open loop gain                         | $100$ V/mV  |
| GBW Gain Bandwidth product                      | 0.7 MHz     |
| SR Slewrate                                     | 0.3 V/us    |
| $V_O$ voltage output swing from rail (positive) | 1.5 V (max) |
| $V_O$ voltage output swing from rail (negative) | 20 mV (max) |

## Closed loop knæk frekvens
Den closed loop knæk frekvens for op ampen kan udregnes som
$$f_{BCL}=\frac {f_t} {1+R_f/R_{in}}$$
hvor $f_t$ er gain bandwidth product (se tabel). Så bliver knæk frekvensen altså
$$f_{BCL}=\frac {0.7\cdot 10^6}{1+10000/378800}=681995 Hz$$

Det kan altså ses, at der skal en meget høj frekvens på input til at nedsænke vores gain ift. frekvens.

## Beta for systemet
Beta for systemet kan udregnes som
$$A_{CL}=\frac {A_{OL}} {1+A_{OL}\beta}\Lef$$