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
| **Kogelspoor** (lijn achter elke kogel) | Kost per kogel extra werk en zou de pooling-meting beïnvloeden. De inslageffecten zijn er wel. |
| **Pathfinding rond vijvers** | Lopers lopen recht op de speler af en kunnen achter een vijver blijven hangen. Dat is nu opgevangen met een vangnet (na 20 s zonder kill worden achterblijvers verplaatst). Echte pathfinding is veel werk voor een klein spelgevoel-effect. |
| **Eigen sprites voor de nieuwe vijanden** | De Spectral Archer, Slime Brute, Shieldbearer en de bazen hergebruiken bestaande spritesheets met een kleurtint. Eigen art kost tijd en zou licenties of eigen tekenwerk vragen. |
| **Webversie (HTML5)** | De exportsjablonen zijn niet geïnstalleerd. In de README staat hoe je het zelf doet. |
| **Controller-ondersteuning** | De game is gebouwd voor toetsenbord. Het PVA vraagt er niet om. |
| **Meerdere arena's of maps** | Eén arena met willekeurig geplaatste vijvers en decoratie is genoeg voor het doel van de opdracht. |
