# Later-lijst

Ideeën die tijdens het bouwen opkwamen en **bewust niet** zijn uitgevoerd, om de scope te bewaken.

Dit is geen restlijst maar een bewijsstuk: in het reflectieverslag onderbouwt deze lijst de gemaakte afbakening. Schrijf er dus ook bij *waarom* het buiten scope viel.

## Afwijkingen van het Plan van Aanpak

| Idee | Waarom niet |
|---|---|
| **Ervaringspunten (XP-orbs) en levelen** | Het PVA beschrijft XP die je oppakt om te levelen. Dat is vervangen door een upgradekeuze aan het einde van elke wave, omdat dat een duidelijker spelritme geeft ("wave klaar, upgrade kiezen, volgende wave"). Daardoor vervallen ook de magneet en meer-XP-upgrades. Pickups bestaan wel, maar zijn directe hulp (herstel, sneller vuren, sneller lopen) en geen XP. |
| **Meerdere wapentypes en een tweede wapen** | Het PVA noemt één wapen met upgrades. Meer wapens vergroot de testlast en de balans-inspanning, terwijl de verdieping bij object pooling ligt. |

## Upgrades die niet gebouwd zijn

Uit de ideeënlijst in [upgrade-ideen.md](upgrade-ideen.md) zijn alleen de aangevinkte upgrades gebouwd.

| Idee | Waarom niet |
|---|---|
| Zware kogels, kritieke treffer, executie | Niet gekozen. Het zijn varianten op schadeverhoging, en daar zijn er al genoeg van (zwaardere kogels, Scherpschutter, Wapenmeester). Meer van hetzelfde maakt de speler sneller te sterk. |
| Tweede wapen, doelwit kiezen, draaiende zwaarden, torentje | Nieuwe systemen met eigen objecten en gedrag. Te groot voor de tijd, en ze maken de balans ingewikkelder. |
| Schild, langere onkwetsbaarheid, tweede kans, schadereductie, regeneratie, meer herstel na een wave | Niet gekozen. De speler werd al te snel te sterk, dus extra overleving past er niet bij. |
| Dash-schade, snelheidsboost na een kill, slow motion na een dash | Niet gekozen. De dash en de beweging zijn al uitgebreid (dubbele dash, langere dash, mijnen). |

## Verwijderd na speeltesten

| Idee | Waarom |
|---|---|
| **Over water lopen** (upgrade Waterloper) | Gebouwd en na een speeltest weer verwijderd: de speler werd te snel te goed, en een vluchtroute over de vijvers maakt wegrennen te makkelijk. |

## Techniek en afwerking

| Idee | Waarom niet nu |
|---|---|
| **Object pooling in de game zelf** | Dit is het verdiepingsonderwerp en wordt apart uitgewerkt, met een eigen benchmark. Een vooraf gebouwde variant zou de meting beïnvloeden. |
| **Kogelspoor** (lijn achter elke kogel) | Eerst uitgesteld omdat het de pooling-meting kon beinvloeden. Na de metingen gebouwd: een Line2D met de laatste 8 plekken, gekleurd naar het soort kogel. |
| **Volledige pathfinding (NavigationServer)** | Lopers komen niet meer vast te zitten achter vijvers: ze volgen een eenvoudig stroomveld om het water heen (`scenes/world/looproute.gd`). Dat is bewust simpeler dan de NavigationServer van Godot, omdat de vijvers de enige obstakels zijn. Het vangnet (na 20 s zonder kill worden achterblijvers verplaatst) blijft staan voor het geval dat. |
| **Webversie (HTML5)** | De exportsjablonen zijn niet geïnstalleerd. In de README staat hoe je het zelf doet. |
| **Controller-ondersteuning** | De game is gebouwd voor toetsenbord. Het PVA vraagt er niet om. |
| **Meerdere arena's of maps** | Eén arena met willekeurig geplaatste vijvers en decoratie is genoeg voor het doel van de opdracht. |
