
---
**Date:** 2026-09-03

## Preparation

>[!TODO] HOMEWORK
>- [ ]  Chapter 1 and Sections 2.1 - 2.3 in [[Artificial Intelligence_ A Modern Approach (4th Edition).pdf|Artificial Intelligence: A Modern Approach 4th]]

> [!DANGER] EXERCISES
> - [ ] 

---
# Relevant documents
[[2026-09-03b - Introductory instructor slides.pdf]]
[[2026-09-03a - Introductory course slides.pdf]]
[[2026-09-03c - Artificial Intelligence introduction.pdf]]
[[2026-09-03d - Python introduction.pdf]]

# Topics


# Notes

Nogen betragter AI i forhold til menneskers _performance_ mens andre fokuserer på _rationalitet_ (At gøre det rigtige)
- Nogen fokuserer også på indre processer såsom tanke prcoess og _reasoning_, mens andre kigger på _opførsel_

Turing testen er en test hvor en computer skal lade som om den er menneske via skreven tekst. For at kunne det, skal den bruge
- Naturlig sprog processering for at kommunikere succefuldt
- Videns representation for at gemme hvad den ved og "hører"
- Automatiseret _reasonging_ for at svare på spørgsmål og drage nye konklusioner
- Machine learning for at kunne tilpasse nye tilfælde og genkende mønstre

En **total turing test** er ligesom ovenstående, men robotten skal kunne interegere med mennesker og objekter i den virkelgie verden. Til det skal den bruge
- Copmuter vision for at kunne se
- Tale genkendelse for at kunne høre
- Robot-manipulatorer for at interegere med verden

Der hvor man ikke har _regler_ for logik (skak har fx regler, mens politik er mere tåget) kan vi bruge _statistik/sandsynlighed_

En **rationel agent** er en der tager et valg, der fører til det bedste udfald. Eller hvis der er usikkered det bedst _forventede_ udfald

Rationelitet er ofte bedre end logik, da det er matematisk defineret (bedste valg fx)

At _gøre det rigtige_ kaldes **standard model**

**Value allignment problem** er når vi giver AI et mål, vi tror stemmer overens med hvad vi gerne vil have, men som måske ikke gør. Dette opstår tit i komplekse systemer såsom selvkørende biler.
- hvis det sker i laboratorie, kan vi bare genstarte, men i den virkelige verden er der konsekvenser.
- Vi skal i stedet have agenter, der vil opfylde _vores mål_, men som er usikker på hvad de er. Den vil derfor være forsigtig og spørge om lov.

Vi kan opdatere sandsynlighederne baseret på ny info fra eksperimenter/erfaring

_Computability_ er hvorvidt en funktion kan udregnes med en effektiv procedure.

_Tractability_ er om et problem vokser eksponentielt når instances vokser. Et intractable problem kan ikke løses i god tid for moderat store instances.

En **videns-baseret agent** har tre trin:
- Stimulus må oversættes til en intern repræsentation
- Repræsentationen skal manipuleres af kognitive processer, som afleder en _ny_ intern repræsentation
- Disse oversættes tilbage til en handling.

Udviklingen i AI stoppede op, da man gik fra _microworlds_ med meget få mulige udfald/states til problemer såsom skak, der har tonsevis af udfald/states.

Introduktionen af **Big Data** (store dataset såsom WWW), har ført til gigantisk udvikling i AI, og store dataset er ofte bedre end at "tweake" sin model.

Agenter senser og påvirker deres miljø

Selvom der kan være flere typer data (e.g. hele universet) er vi kun interesseret i få ting (e.g. lyd) når vi designer en agent.
- Den del som agenter senser og den del den påvirker

![[Pasted image 20261123155902.png]]

En action på et givet tidspunkt er taget på baggrund af alt det agenten _har_ målt (**percept sequence**), men ikke på fremtidige målninger.

**Agent function** er en matematisk beskrivelse af en agent
**Agent program** er en konkret implementation, der kører på et fysisk system.

Rationalitet måles på _performance_ (hvor godt var et valg?)

> For each possible percept sequence, a rational agent should select an action that is expected to maximize its performance measure, given the evidence provided by the percept sequence and whatever built-in knowledge the agent has.

En agent kan ikke være _omniscient_ (alt vidende) da den ikke i forvejen kender alle udfald, men kan _gætte_ med god sandsynlighed på udfald.

For at få viden om verden og dens udfald, må en agent _undersøge_ eller **explore**.

Hvis en agent bare opfører sig på baggrund af _designerens viden_ og ikke på baggrund af dens egen opfattelse, har den ikke **autonomi**

**Task enviroment** indeholder miljø, performance measure, aktuatorer og sensorer.
- **PEAS** **P**erformance, **E**nvironment, **A**ctuators, **S**ensors

Hvis en agents sensorer giver den adgang til _complete state_ af miljøet på hvert tidspunkt, er opgaven **fully obsevable**
- I praksis er det kun de states, der er vigtige for valget af action, der gør om opgaven er fully observable eller ej






---
#lecture 