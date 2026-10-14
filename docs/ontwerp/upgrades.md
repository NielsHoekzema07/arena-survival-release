# Upgrades

Na elke wave kies je uit drie upgrades. Een upgrade is een `UpgradeDefinitie`-resource
in `resources/upgrades/`; `UpgradeManager` (`scenes/upgrades/upgrade_manager.gd`) houdt
bij hoe vaak elke is gekozen en past het effect toe. De resources zelf worden nooit
aangepast, zodat een nieuwe run schoon begint.

## Zeldzaamheid

| Niveau | Kleur | Basiskans | Groei per wave | Eerst beschikbaar |
|---|---|---|---|---|
| Gewoon | grijs | 60 | geen | wave 1 |
| Zeldzaam | blauw | 28 | +6% per wave | wave 2-3 |
| Episch | paars | 8 | +12% per wave | wave 4-5 |

Gewone upgrades zijn kleine verbeteringen. Zeldzame en epische upgrades zijn sterker of
doen iets nieuws. Naarmate je verder komt worden ze waarschijnlijker, en elke upgrade heeft
een `eerste_wave` zodat bijzondere upgrades niet meteen in wave 1 het spel breken. De drie
opties komen nooit alle uit dezelfde categorie (aanval, verdediging, beweging, risico).

## Hoe effecten werken

Alle kogeleffecten (doorboren, ricochet, explosie, bliksem, vuur, gif, bevriezing,
levensdief, split en ringschot) staan in één object, `KogelEffecten`, dat het wapen met
alle kogels deelt. Een upgrade past alleen dat object aan. De kogel leest het bij een
treffer. Een nieuw kogeleffect toevoegen is dus een veld in `KogelEffecten`, een regel in
`Bullet._treffer()` en een regel in `UpgradeManager._pas_effect()`.

Een upgrade kan een **tweede effect** hebben (`effect2`). Dat is bedoeld voor
duivelsdeals: een bonus en een nadeel in één kaart. Het nadeel staat in rood op de kaart.

## Gewone upgrades

| Upgrade | Effect | Max |
|---|---|---|
| Zwaardere kogels | +20% schade | 5 |
| Sneller vuren | 12% sneller | 5 |
| Groter bereik | +15% bereik | 4 |
| Snellere kogels | +25% kogelsnelheid | 4 |
| Extra levenspunten | +150 max. HP en direct erbij | 5 |
| Herstel | 30% HP terug | onbeperkt |
| Sneller lopen | +8% loopsnelheid | 4 |
| Snellere dash | 15% kortere cooldown | 4 |
| Langere dash | +25% dashafstand | 3 |
| Doornen | vijanden die je raken krijgen 50 schade terug | 5 |

## Zeldzame upgrades

| Upgrade | Effect | Max |
|---|---|---|
| Scherpschutter | +35% schade | 3 |
| Machinegeweer | 20% sneller vuren | 3 |
| Pantser | +350 max. HP | 3 |
| Windloper | +10% loopsnelheid | 3 |
| Levensdief | 6% van je schade geneest je | 4 |
| Doorborende kogels | kogels gaan door +1 vijand | 3 |
| Split shot | +1 kogel in een waaier, elke kogel 65% schade | 3 |
| Ricochet | een kogel springt na een treffer naar de volgende vijand | 3 |
| Explosieve kogels | 50% schade in een gebied rond de treffer | 3 |
| Brandende kogels | 20 schade per seconde, 3 s | 4 |
| Giftige kogels | 12 schade per seconde, 6 s | 4 |
| Bevriezing | 35% langzamer, 1,5 s | 3 |
| Schokgolf | word je geraakt, dan duwt een golf vijanden weg | 3 |
| Mijnen | bij elke dash een mijn (120 schade) | 4 |
| Dubbele dash | twee dashes opsparen | 1 |

### Met nadeel (categorie risico)

| Upgrade | Bonus | Nadeel | Max |
|---|---|---|---|
| Vloek van overvloed | na elke wave een upgrade extra kiezen | 30% meer vijanden per wave | 2 |
| Duivelsdeal: bloeddorst | +50% schade | vijanden 10% sneller | 2 |
| Duivelsdeal: glazen kanon | +80% schade | 30% minder max. HP | 2 |
| Duivelsdeal: hongerige horde | 40% sneller vuren | 25% meer vijanden | 2 |

## Epische upgrades

| Upgrade | Effect | Max |
|---|---|---|
| Kettingbliksem | een treffer springt naar 2 andere vijanden (50% schade) | 2 |
| Ringschot | elke 5e salvo een ring van 8 kogels (60% schade) | 3 |
| Wapenmeester | +30% schade en 15% sneller vuren | 2 |
| Reuzenhart | +700 max. HP en volledig genezen | 2 |
| Duivelsdeal: bloedpact | +100% schade | 50% minder max. HP | 1 |

## Meer upgrades

| Upgrade | Zeldzaamheid | Effect | Max |
|---|---|---|---|
| Bounce shot | zeldzaam | kogels kaatsen op de rand van het veld terug | 3 |
| Boemerang | episch | kogels keren om en komen terug naar jou, en raken vijanden opnieuw | 1 |

## Herrollen en overslaan

Op het upgradescherm kun je de drie opties opnieuw trekken (**R**, twee keer per run) of
de keuze overslaan (**S**) voor 35% van je levenspunten.

## Synergieën

Bepaalde combinaties van upgrades doen samen iets extra's. Ze worden automatisch actief
en staan in het pauzescherm (Esc).

| Synergie | Combinatie | Effect |
|---|---|---|
| Napalm | brandende kogels + explosieve kogels | explosies zetten vijanden in brand |
| IJsbliksem | bevriezing + kettingbliksem | bliksem vertraagt de vijanden die hij raakt |
| Stekelgolf | doornen + schokgolf | de schokgolf doet extra schade gelijk aan je doornen |
| Bloedbad | levensdief + explosieve kogels | explosies genezen je via je levensdief |

## Uitdagingen (wave-modifiers)

Vanaf wave 3, daarna om de wave, kies je vóór de wave een uitdaging of sla je over. De
wave wordt zwaarder; na afloop krijg je de beloning. `WaveModifier`-resources staan in
`resources/modifiers/`.

| Uitdaging | Effect | Beloning |
|---|---|---|
| Snelle horde | vijanden 25% sneller | een extra upgrade |
| Taaie horde | vijanden 50% meer HP | een extra upgrade |
| Overstroming | 50% meer vijanden | 50% HP terug |
| Stormloop | vijanden verschijnen twee keer zo snel | 50% HP terug |
| Ruwe nacht | 25% sneller, taaier en talrijker | twee extra upgrades |

## Balans

De sterkte van een upgrade is bepaald zodat één keer kiezen merkbaar maar nooit
spelbrekend is:

- **Split shot** levert per extra kogel 65% schade, dus één stack is een verbetering
  van circa 30% in plaats van een verdubbeling.
- **Levensdief** is 8% per stack. Bij 4 schoten per seconde en 40 schade is dat circa 13
  levenspunten per seconde per stack, vergelijkbaar met een wave-herstel van 25%.
- **Duivelsdeals** hebben een nadeel dat de rest van de run blijft werken, dus ze zijn
  sterker dan gewone upgrades.
- **Kettingbliksem, ringschot en explosie** raken meerdere vijanden. Daarom komen ze
  later (eerste_wave 3-4) en hebben ze een kleiner schade-aandeel.

**Sneeuwbaleffect.** Een eerste run met een slimme bot haalde wave 30 zonder te
sterven: sterke combinaties (split shot, ricochet, explosie en bliksem samen) maakten de
rest van de run triviaal. Daarom groeien de levenspunten van vijanden ook kwadratisch per
wave (`hp_groei_kwadratisch`, zie [waves.md](waves.md)), zodat de curve bij sterke
builds sneller omhoog gaat.

Controle met een bot na die aanpassing (10 runs, 4 met willekeurige keuzes en 6 met
slimme keuzes): de bot haalde wave 4 tot 8. Een echte speler speelt beter dan de bot
(die alleen wegduikt en dasht), dus ik verwacht wave 8-15. Dit is een indicatie, geen
bewijs; de getallen staan als `@export` op de WaveManager.

## Afremmen van de spelergroei

Na een speeltest bleek de speler te snel te sterk te worden. Daarom zijn de volgende
aanpassingen gedaan:

- Alle percentages van de stat-upgrades liggen lager (bijvoorbeeld Scherpschutter van +50%
  naar +35%, Pantser van +500 naar +350 levenspunten).
- Zeldzame en epische upgrades worden trager waarschijnlijker per wave.
- Split shot, ricochet, vuur, gif en bevriezing komen pas vanaf wave 3 in de keuze.
- Het herstel na een wave is 15% in plaats van 25%, en een hartje geneest 12% in plaats van 20%.
- Vijanden groeien sneller mee, zie [waves.md](waves.md).
- De upgrade Waterloper (over vijvers lopen) is verwijderd.
