
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

