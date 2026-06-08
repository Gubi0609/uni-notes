
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
$$A_{CL}=V_{\text{O, max}}/V_{\text{i, max}}=10V / 0.264 V = 37.88$$

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
$$\beta=\frac {R_{in}}{R_{in}+R_f}=\frac {10000\Omega}{10000\Omega+378800\Omega}=0.0257$$

$\beta$ er **feedback faktoren**, altså hvor meget af output, der går retur til indgangene.
## Alpha for systemet
Alpha for systemet kan udregnes som
$$\alpha=\frac {R_f}{R_f+R_{in}}=\frac {378800\Omega}{378800\Omega+10000\Omega}=0.9743$$

$\alpha$ er **feedforward faktoren**, altså hvor meget af input, der går tabt pga. for eksempel spændingsdelere ved indgangene.
## Error for systemet
Den teoretiske error er
$$\text{Error}=1-\frac {A_{Ol}}{\frac 1\beta+A_{OL}}=1-\frac {100000}{\frac 1 {0.0257}+100000}=0.00038$$

Så den teoretiske fejl er faktisk meget meget lille. Dette kan dog ikke ses på de reelle målinger.


## Full power bandwidth
Full power bandwidth indikerer den højeste frekvens hvormed output signalet stadig kan følge med indgangsignalet.
$$f_{FP}=\frac {SR}{2\pi\, V_{\text{o, max}}}$$
hvor $V_{\text{o, max}}$ er 10 V og SR er slewrate fra tabellen.
$$f_{FP}=\frac {0.3\cdot 10^6 V/s}{2\pi\, 10 V}=4774.65 Hz$$

==Op ampen kan altså ikke følge med PWM kredsløbet (ud fra målte frekvenser, ikke teoretiske). Derfor er et RC kredsløb altså nødvendigt før input, for at stabilisere==

## Worst case output voltage
Vi kan ud fra worst case offset og bias voltage

# RC Kredsløb
![[Screenshot from 2026-06-07 18-44-30.png|700]]

På det endelige kredsløb sættes et RC lav pas filter på begge input. De har begge den teoretiske knæk frekvens
$$f_b=\frac 1 {2\pi\,R\,C}=\frac 1 {2\pi\cdot 10000 \Omega\cdot 0.000001 F}=15.92 Hz$$
Med denne meget lave knæk frekvens, bliver input til op amp + og - port dæmpet meget, men med den samme faktor.

# PWM generator
For PWM generatoren, har den en frekvens givet ud fra
$$f=\frac 1 {ln(2)\,C\,(R_1+R_2+R_3)}$$

Da $R_2$ og $R_3$ er modstandende inde i potentiometeret, er forholdet mellem dem altid ens. Dermed kommer $R_2+R_3$ til at være konstant $100\text{ k}\Omega$. $R_1=1000\Omega$ og $C=0.00000001 F$
$$f=\frac 1 {ln(2)\,0.00000001 F\,(1000\Omega+100000\Omega)}=1428.41 Hz$$

## Magnitude og fase af signal fra RC filter
På grund af RC lav pas filteret og PWM generatoren, kommer indgangsignalerne til op ampen til at være dæmpet (**teoretisk set**)
Der kommer også til at være et fase skift. Begge kan udregnes ud fra
$$A_v=\frac 1 {1+j(f/f_b)}=\frac 1 {1+j(1428.41/15.92)}=0.0111\angle{-89.3615^\circ}$$

