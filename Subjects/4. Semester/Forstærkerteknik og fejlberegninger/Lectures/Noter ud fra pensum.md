
Side 557-558 om hvorfor negativ feedback fører til mere stabil gain (MEGET VIGTIGT VIL JEG TRO)

Side 560 viser hvordan closed loop feedback gain afhænger af $\beta$. Måske det kan bruges til at finde frem til vores beta for systemet.

Side 85, ligning 2.37 viser closed loop gain, hvor man har taget højde for frekvens. (NOK MEGET VIGTIGT)
- I datasheetet kan man se gain bandwidth product. På side 86, ligning 2.39 er der en formel til at udregne dette. Det kan nok bruges til at isolere closed loop break off frequency.
- Se også ligning 2.41 på side 87, for hvordan man isolerer $f_{BCL}$ når man har både $f_{BOL}$ og $A_{0OL}$ og $f_{BCL}$
- **Faktisk kan ligning 2.42 bare bruges på side 87. Den er perfekt**

Sammenlign slewrate fra datasheet med min/max frekvens fra PWM (side 92-93 forklarer dette)
- Se også ligning 2.46 på side 93 for _full-power bandwidth_ ligning ud fra slewrate og $V_{o,max}$. Resultatet er Hz, så lige hvad vi skal bruge

Udregning for knækfrekvens af RC lavpas filter på side 485, ligning 8.6
- Nem huskeregel for $A_v$ i dB ift knækfrekvensen er 
- ![[Pasted image 20260607163529.png]]

Input offset voltage kan aflæses fra datasheet. Forklaringer står på side 95-99

Se eksempel 2.10 på side 96 for eksempel på worst case offset

I bunden af side 97, kan ses en ligning for bias voltage ud fra bias current (se datasheet) og $R_2$. Det kan vi bruge

På side 111 står der info om differential forstærker
- Der står også at for at minimere påvirkningen af bias current, skal de to resistor par være lig med hinanden. Da vores ikke er det præcis, kunne det være smart med en udregning for at vise hvor meget det påvirker systemet.