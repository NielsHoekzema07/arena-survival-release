# Vijandtypes en balansinstellingen

Overzicht van de vijandtypes en de waarden waarmee ze onderscheiden worden.
Dit is het bewijsstuk dat het Plan van Aanpak in week 6 vraagt.

## Opzet

Er is **één** `enemy.gd` en **één** `enemy.tscn`. Een type is een resource
(`VijandType`) met alleen data erin, opgeslagen als `.tres` in
`resources/vijandtypes/`. De spawner trekt bij elke spawn een type en geeft het
mee aan `spawn_op()`.

Dat is bewust zo, om twee redenen:

- Het Plan van Aanpak vraagt vijandtypes te onderscheiden via instelbare waarden
  in plaats van via aparte scriptklassen per type.
- In fase 7 is er dan **één** object pool nodig in plaats van een pool per type.
  Een vijand die uit de pool komt krijgt gewoon een ander type toegewezen.

Een vierde type toevoegen is een `.tres` aanmaken en in de lijst op de spawner
zetten. Er hoeft geen regel code bij.

## De drie types

| | Clawed Abomination | Depraved Blackguard | Crimson Imp | Floating Eye |
|---|---|---|---|---|
| Rol | traag, taai, weinig schade | middenmoot | snel, breekbaar, hard | vliegt over water |
| Levenspunten | 175 | 105 | 70 | 85 |
| Treffers tot dood (bij 35 schade) | 5 | 3 | 2 | 3 |
| Loopsnelheid | 120 px/s | 260 px/s | 340 px/s | 150 px/s |
| Contactschade | 60 | 100 | 150 | 90 |
| Vliegt | nee | nee | nee | **ja** |
| Spritevergroting | 4,2× | 3,5× | 3,0× | 3,2× |
| Botsingsstraal | 28 | 24 | 19 | 22 |
| Spawngewicht | 10 | 45 | 45 | 25 |
| Kans | 8% | 36% | 36% | 20% |

De gewichten zijn relatief, niet in procenten: ze worden opgeteld en de kans is
het aandeel in dat totaal. Bij 10 + 45 + 45 + 25 = 125 komt de Blackguard dus in
36 procent van de spawns voorbij. Zo kun je een type toevoegen zonder alle
andere getallen opnieuw te laten optellen tot honderd.

### Vliegende vijanden

`vliegt` op een `VijandType` doet precies één ding: het haalt de laag `water`
uit de `collision_mask`. De vlieger steekt vijvers dus over, maar houdt `world`
en botst nog gewoon op de arenamuur. Zie
[collision-layers.md](collision-layers.md) voor waarom water een eigen laag
heeft.

Er hangt ook een visueel deel aan: een vlieger deint op en neer via
`zweefhoogte`. Dat is geen franje maar noodzaak — zonder dat is voor de speler
niet te zien waarom de een wel over het water kan en de ander niet. Alleen de
sprite beweegt, niet de botsingsvorm, anders zou het trefvlak mee op en neer
gaan.

Een vlieger mag ook bóven water spawnen; de spawner slaat de vijvercontrole
over als het gekozen type vliegt.

## Waarom deze getallen

**De levenspunten hangen aan het wapen.** Om bij te blijven geldt:

```
schoten per seconde  >=  treffers per kill  x  spawns per seconde
```

Het wapen doet 35 schade en vuurt vier keer per seconde. Gemiddeld over de drie
types zijn dat (5 + 3 + 2) / 3 = 3,3 treffers per kill, dus ongeveer 1,2 kills
per seconde tegen 1 spawn per seconde. Genoeg marge om vooruit te komen, niet zo
veel dat het saai wordt.

Pas je de spawnfrequentie of de wapenschade aan, reken deze som dan opnieuw.
Zet je de levenspunten van de Abomination bijvoorbeeld op 260, dan zijn dat acht
treffers en kom je onder de 1,0 kills per seconde — dan loopt het aantal
vijanden onherroepelijk op.

**Contactschade werkt anders dan je verwacht.** De speler is na een treffer 0,5
seconde onkwetsbaar, dus hij krijgt hooguit **twee treffers per seconde**,
ongeacht hoeveel vijanden er tegen hem aan staan. De "dps" van een type is
daarmee gewoon zijn contactschade maal twee. Met 1000 levenspunten overleeft de
speler dus ongeveer:

| Type | schade per treffer | dps | seconden |
|---|---|---|---|
| Clawed Abomination | 60 | 120 | 8,3 |
| Depraved Blackguard | 100 | 200 | 5,0 |
| Crimson Imp | 150 | 300 | 3,3 |

**Botsingsstraal hoort bij de spritevergroting.** Staan die uit verhouding, dan
raakt een vijand je terwijl hij nog zichtbaar naast je loopt, of andersom. Let
er ook op dat vijanden elkaar opzij duwen: een grotere straal betekent dat een
Abomination meer ruimte inneemt in een kluwen.

## Oplopende moeilijkheidsgraad

De tijdgebaseerde golven van 30 seconden zijn vervangen door een echt wave-systeem.
Zie [waves.md](waves.md). De waarden in de tabel hierboven zijn de basiswaarden
van wave 1; de schaling per wave wordt bij het spawnen toegepast en niet in de
`.tres` geschreven, omdat een resource gedeeld is.

## Bijzondere types

Naast de vier gewone types zijn er drie met eigen gedrag. Ze gebruiken dezelfde
spritesheets als de gewone vijanden, met een `tint` om ze uit elkaar te houden.
Dat kan omdat een type alleen data is: een nieuw type is een `.tres`, geen code.

| Type | Vanaf wave | Gedrag | Levenspunten | Snelheid |
|---|---|---|---|---|
| Spectral Archer | 4 | schiet elke 2,4 s op afstand en houdt ongeveer 250 px afstand | 80 | 190 |
| Slime Brute | 5 | splitst bij doodgaan in twee Slimelings | 130 | 150 |
| Slimeling | - | alleen als restant van een Slime Brute | 35 | 235 |
| Shieldbearer | 7 | 140 schild dat eerst schade opvangt | 90 | 200 |

De afstand van de Archer ligt bewust onder het wapenbereik (200): een schieter die
daarbuiten blijft is niet te raken en laat de wave hangen.

Een splitter laat kleintjes achter die meetellen voor de wave. De spawner meldt die
eerst bij de WaveManager (`extra_vijanden`) en pas daarna de kill van de splitter zelf,
anders eindigt de wave te vroeg. Het spawnen gebeurt uitgesteld, omdat een kogel die
de splitter raakt in een physics-callback zit en daar geen nieuw lichaam toegevoegd mag
worden.

## Elites en eindbazen

**Elites** komen vanaf wave 5 voor met een kans die per wave stijgt (6% plus 2% per wave,
maximaal 22%). Een elite is 1,35 keer zo groot, heeft drie keer de levenspunten en 1,5
keer de contactschade, is goudkleurig en laat altijd een pickup vallen. De waarschuwing
voor een elite is geel en groter.

**Eindbazen** verschijnen elke 5e wave bovenop de gewone vijanden. De eerste is de
Abomination King (2000 levenspunten, schaalt mee met de wave), de tweede de vliegende
Imp Lord. Een baas:

- stopt een seconde met een rood knipperende waarschuwing en stormt dan op je af (charge)
- schiet af en toe een ring van 14 kogels
- laat zich niet wegduwen door een schokgolf
- heeft een eigen gezondheidsbalk bovenin
- laat drie pickups vallen

## Pickups

Vijanden laten soms iets vallen (gewone vijanden 6%, elites altijd, bazen drie stuks).
Er zijn nooit meer dan 12 tegelijk, en ze verdwijnen na 14 seconden.

| Pickup | Effect |
|---|---|
| Hartje (60%) | 20% van je maximale levenspunten |
| Woede (20%) | 8 seconden 60% sneller vuren |
| Spoed (20%) | 8 seconden 30% sneller lopen |

Het zijn geen ervaringspunten: de upgrades komen aan het einde van een wave.
