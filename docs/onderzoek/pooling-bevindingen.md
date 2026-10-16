# Bevindingen: waarom pooling bij vijanden trager is dan zonder

Werknotities bij het pooling-onderzoek. De conclusies horen straks in
`onderzoek-object-pooling.md`; dit bestand bewaart wat er is uitgezocht.

## De waarneming

In `data/benchmark-20261014-154340.csv` (10 s per meetpunt, debug-build, patroon
gelijkmatig) is bij **1000 vijanden** de gemiddelde frametijd met pooling hoger dan zonder:

| | Zonder pooling | Met pooling |
|---|---|---|
| Gem. frametijd | 8,1 ms | 13,4 ms |
| p99 | 12,5 ms | 19,7 ms |

Bij 100 vijanden is het gelijk, en bij **kogels** helpt pooling juist (1000 kogels: 1,88 ms
zonder en 1,47 ms met pooling). Herhaalmetingen met 1000 vijanden gaven 7,7-8,0 ms zonder en
10,4-13,5 ms met pooling, dus het effect is reproduceerbaar.

## Waar het zit

Met een stopwatch om de aanroep (`Time.get_ticks_usec()`):

| | Zonder pooling | Met pooling |
|---|---|---|
| `move_and_slide()` per aanroep | 3,7 - 3,9 µs | 5,2 - 5,5 µs |

- Zet je `move_and_slide()` uit, dan is pooling juist sneller (3,3 ms tegen 4,6 ms).
- Het aantal actieve vijanden is in beide varianten gelijk (997 van 1000).
- Het wordt erger naarmate een vijand vaker is hergebruikt: 4,5 µs bij het eerste hergebruik en
  5,7 µs bij het tweede en later.
- Het blijft ook zo als de vijanden stilstaan (6,0 µs met en 2,5 µs zonder pooling), dus het zit niet
  in het opeenhopen van vijanden in het midden.

## Wat het niet is

Elke proef is apart uitgevoerd en maakte het verschil niet weg:

| Proef | Uitkomst |
|---|---|
| Uitzetten via alleen `set_physics_process(false)` in plaats van `process_mode` | niet beter (5,8 - 6,9 µs) |
| Vijanden uit de boom halen zolang ze in de pool zitten | niet beter (5,4 - 5,7 µs) |
| Botsingslaag en -mask niet aanraken bij uitzetten | niet beter (6,2 µs) |
| Botsingsstraal alleen aanpassen als hij verandert | niet beter |
| Animatie (`sprite_frames`, `play`) niet opnieuw toewijzen, en maar één vijandtype | niet beter (5,2 µs) |
| Botsingsmask op 0 (er kan niets botsen) | verschil blijft (10,8 tegen 7,7 ms) |

## Wat het dan wel kan zijn (niet bewezen)

De oorzaak zit in de physics-server van Godot, in de toestand van een lichaam dat al een keer is
gebruikt en weer is uitgezet. Een nieuw lichaam dat in één keer met de goede waarden in de wereld
komt, is goedkoper dan een bestaand lichaam waarvan positie, laag en mask worden aangepast. Dat is
een hypothese; ik heb het niet kunnen bevestigen. Een verder onderzoek zou het Godot-profiel van de
physics-server moeten bekijken of dezelfde meting op een andere Godot-versie moeten herhalen.

## Wat dit betekent

- Object pooling is **niet automatisch sneller**. Het helpt bij lichte objecten (kogels, `Area2D`) en kost
  prestatie bij zwaardere objecten met een fysiek lichaam (`CharacterBody2D`), voor zover gemeten op
  deze machine, in deze Godot-versie, met deze opzet.
- De keuze in de game blijft daarom een bewuste afweging. Mogelijkheden:
  1. Alleen kogels poolen en vijanden niet.
  2. Beide poolen en de afweging in het verslag beschrijven.
- Beperkingen: debug-build en geen release-export, één machine, korte meetduur in de proeven. De
  volledige meetreeks (3 herhalingen, 30 s per punt) moet nog gedraaid worden.

## Besluit voor de game

Er wordt **niets gepoold**: `EnemySpawner.pool_vijanden = false` en `Weapon.pool_kogels = false`.
Eerder gold: kogels wel, vijanden niet. Na de release-meting (en de herhaalde kogelmeting) is ook
dat bijgesteld, omdat pooling bij kogels niet sneller bleek. De onderbouwing en de redenering staan
in `onderzoek-object-pooling.md`, onderdeel 6.
