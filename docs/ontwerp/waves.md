# Wave-systeem

`WaveManager` (`scenes/waves/wave_manager.gd`) bepaalt het ritme van het spel;
`EnemySpawner` voert het spawnen uit. Alle getallen zijn `@export` op de
WaveManager.

## Verloop

`AFTELLEN` (4 s) → `ACTIEF` (spawnen tot alle vijanden dood zijn) → `KLAAR`
(2 s, speler krijgt 15% levenspunten terug) → `UPGRADE` (kies een upgrade, soms
meerdere) → eventueel `MODIFIER` (kies een uitdaging, vanaf wave 3 om de wave) →
volgende wave. Zie [upgrades.md](upgrades.md) voor de upgrades en uitdagingen.

Een wave is klaar als het aantal te doden vijanden op 0 staat. De teller loopt
via het signaal `Enemy.gestorven`, niet via `queue_free`.

## Per wave

| | Formule | Wave 1 | Wave 5 | Wave 10 |
|---|---|---|---|---|
| Aantal vijanden | `12 + 6 × (wave − 1)` | 12 | 36 | 66 |
| Interval tussen salvo's | `1,5 s × 0,92^(wave−1)`, min. 0,4 s | 1,5 | 1,1 | 0,7 |
| Vijanden per salvo | `1 + (wave − 1) / 3` | 1 | 2 | 4 |
| Levenspunten | `× (1 + 0,15 × n + 0,02 × n²)`, n = wave − 1 | ×1,00 | ×1,92 | ×3,97 |
| Contactschade | `× (1 + 0,10 × (wave − 1))` | ×1,00 | ×1,40 | ×1,90 |

Nooit meer dan 60 vijanden tegelijk (`max_tegelijk`): zie
[collision-layers.md](collision-layers.md) voor wat dat in physics kost.

## Typen per wave

`VijandType.eerste_wave` bepaalt wanneer een type kan voorkomen:

| Type | Vanaf wave |
|---|---|
| Depraved Blackguard | 1 |
| Crimson Imp | 2 |
| Clawed Abomination | 3 |
| Floating Eye | 4 |

## Elites, eindbazen en pickups

Vanaf wave 5 verschijnen elites; elke 5e wave komt er een eindbaas bij. Zie
[vijandtypes.md](vijandtypes.md) voor de waarden. De baas telt mee in het aantal vijanden
dat dood moet, en gesplitste vijanden (Slimelings) tellen er ook bij.

## Spawnen

Vijanden verschijnen op een willekeurige plek in het veld, minstens 400 px van
de speler. Lopers spawnen niet in het water; vliegers wel.

Eerst verschijnt 0,8 s een rode markering (`SpawnWaarschuwing`) met een krimpende
ring; pas daarna komt de vijand. `waarschuwing_duur` staat als `@export` op de
spawner. Een vijand telt direct mee voor het maximum aantal tegelijk, ook
voordat de markering is afgelopen.

## Nog te doen
## Upgrades

Na `KLAAR` opent het upgradescherm en staat het spel op pauze. De speler kiest
met muis of toets 1/2/3 uit drie willekeurige upgrades; daarna telt de volgende
wave af. Een upgrade is een `UpgradeDefinitie`-resource (`resources/upgrades/`),
`UpgradeManager` houdt bij hoe vaak elke is gekozen en past het effect toe. De
resources zelf worden nooit aangepast, zodat een nieuwe run schoon begint.

| Upgrade | Effect per keer | Max |
|---|---|---|
| Zwaardere kogels | +25% schade | 5 |
| Sneller vuren | 15% korter vuurinterval | 5 |
| Groter bereik | +15% bereik | 4 |
| Doorborende kogels | +1 vijand doorboord | 3 |
| Extra levenspunten | +200 max. HP en direct erbij | 5 |
| Herstel | 40% HP terug | onbeperkt |
| Sneller lopen | +8% loopsnelheid | 4 |

De drie opties komen nooit alle uit dezelfde categorie (aanval, verdediging,
beweging). Een upgrade die op zijn maximum zit, wordt niet meer aangeboden.

## Achterblijvers

Een loper kan achter een vijver vastlopen. Is alles gespawnd en is er 20 s geen
kill geweest, dan zet de spawner de resterende vijanden op een nieuwe plek, zodat
een wave nooit blijft hangen.

## Snelheden en dash

De speler loopt 300 px/s. Vijanden zijn bewust (bijna) even snel of sneller:

| Type | Snelheid | Ten opzichte van de speler |
|---|---|---|
| Clawed Abomination | 120 | 40% |
| Depraved Blackguard | 260 | 87% |
| Floating Eye | 310 | 103% |
| Crimson Imp | 340 | 113% |

Snelheid schaalt niet mee per wave. Nieuwe vijanden lopen de eerste 0,6 s op
verminderde snelheid (50% oplopend naar 100%), zodat je ze ziet aankomen.

Tegen snellere vijanden heeft de speler een **dash** (Spatie of Shift): 260 px in
0,15 s, onkwetsbaar tijdens de dash, cooldown 1,5 s (balkje onder de healthbar).
De upgrade "Snellere dash" verkort de cooldown met 15%.

## Balanscontrole met een bot

Geen bewijs, maar een eerste indicatie. Een script speelde headless 4 runs per
variant (via `Engine.time_scale`):

| Botgedrag | Bereikte wave |
|---|---|
| Alleen vluchten, willekeurige upgrades | 3 - 4 |
| Vechten, wegduwen bij nabijheid, dashen, slimme upgrades | 6 - 8 |

Een echte speler speelt beter dan de bot, dus 8-12 is een redelijke verwachting.
Vluchten alleen werkt niet meer (de Imp is sneller), je moet dus schieten.

## Nog te doen

Extra's (zie het stappenplan): hit-feedback, highscore, elites en dergelijke.

## Uitdagingen

Vanaf wave 3 kies je om de wave een uitdaging (of je slaat hem over). Er zijn negen:
Overstroming, Ruwe nacht, Snelle horde, Stormloop, Taaie horde, en nieuw Bloedmaan (taaier,
minder vijanden, volledig herstel), Zwerm (dubbel zoveel zwakke vijanden), IJzeren vuist
(dubbele levenspunten, minder en trager) en Bliksemaanval (sneller, achter elkaar, herstel).
Een uitdaging is een `WaveModifier`-resource in `resources/modifiers/`.

## Na een eindbaas

Na elke eindbaas krijg je een extra keuze vooraf, met alleen **epische** upgrades (of zeldzame als
er te weinig episch beschikbaar is), voordat de gewone keuze volgt.

## Gevaren in de arena

Vanaf wave 4 verschijnen er tijdens een wave gevaren (`scenes/world/gevaren.gd`), elke 4 tot 8,5 s
en steeds vaker. Ze kondigen zich aan met een waarschuwing, en ze raken ook de vijanden:

- **Bliksem:** een rode cirkel loopt vol (1,3 s) en dan slaat hij in. De schade is 100 (schaalt
  mee met de wave) voor jou en het dubbele voor vijanden in de cirkel.
- **Vuurpoel:** na 1 s waarschuwing brandt hij 6 s en doet elke halve seconde schade aan wie erin staat.

## Klassen

Aan het begin van elke run kies je een klasse (`scenes/ui/klasse_scherm.gd`): de **Jager** (+20% snelheid,
+18% vuursnelheid, -20% levenspunten), de **Tank** (+60% levenspunten, +10% herstel na een wave, 8%
trager) of het **Glazen kanon** (+80% schade, -40% levenspunten). Daarna werken alle upgrades gewoon.

## Weer

Per run is er helder weer, regen, mist of een donkere avond (`scenes/world/weer.gd`). Het is alleen
sfeer en kan in de instellingen uit. In de dagelijkse run is het weer per datum hetzelfde.

## Prestaties

Twaalf prestaties (`scripts/prestaties.gd`), bewaard in de records en zichtbaar in het hoofdmenu:
bijvoorbeeld wave 5, 10 en 15 halen, een eindbaas verslaan zonder schade, alle vier de bazen
verslaan, 300 kills in een run of met alle klassen spelen.
