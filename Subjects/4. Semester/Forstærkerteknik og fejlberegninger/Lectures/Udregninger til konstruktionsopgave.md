
# Krav
Måleområde: 0 - 240 g\*cm
Udgangsignal: 0 - 10 V
Måle modstand: 100 m$\Omega$

Buzzer skal hyle ved overstigning af torque på 150 g\*cm

# Forstærkning
Ud fra motorens datasheet, kan ses **stall current** og **stall torque** ved 12 V som
$$\tau_{\text{stall}} = 360\text{ g*cm}$$ $$I_{\text{stall}} = 3.952\text{ A}$$

Ud fra dette, er altså
$$I_{\text{stall}} = K_m\tau_{\text{stall}}=3.952\text{ A} = K_m\cdot 360\text{ g*cm}\Leftrightarrow K_m=3.952 / 360 = 0.01098$$

Vi ved så også fra kravene, at vores max torque er 240 g\*cm. Strøm ved dette er så
$$I_{\text{max}}=0.01098\cdot 240\text{ g*cm}=$$