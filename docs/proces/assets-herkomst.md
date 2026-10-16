# Herkomst van assets

Per bestand: waar het vandaan komt en onder welke voorwaarden het gebruikt mag worden.

| Bestand(en) | Bron | Licentie of voorwaarden |
|---|---|---|
| `assets/art/player/held_walk.png`, `held_idle.png` | Zelf getekend met `tools/maak_sprites.py` | Eigen werk |
| `assets/art/enemies/*.png` (negen vijanden) | Zelf getekend met `tools/maak_sprites.py` | Eigen werk |
| `assets/art/bullet/bolt_00..29.png` | Zelf getekend met `tools/maak_sprites.py` | Eigen werk |
| `assets/art/upgrades/*.svg` (iconen van de upgrades) | Zelf getekend met `tools/maak_upgrade_iconen.py` | Eigen werk |
| `assets/art/floor/decoratie.png` (16 motieven: bloemen, gras, varen, paddenstoelen, stenen, stronk, boomstam, struik, riet, lelieblad) | Zelf getekend met `tools/maak_omgeving.py` | Eigen werk |
| De grond (gras, aarde, zand rond vijvers en de stenen muur) | Tijdens het spelen opgebouwd uit ruis door `scenes/world/terrein.gd`; er is geen plaatje voor | Eigen werk |
| `assets/art/floor/grass.png` | Zelf gegenereerd binnen dit project (nog gebruikt als achtergrond van het hoofdmenu) | Eigen werk |
| `assets/audio/boss_battle.wav` (bossmuziek) | *Epic Boss Battle [Seamlessly Looping]* door Juhani Junkala, via [OpenGameArt](https://opengameart.org/content/boss-battle-music), gedownload op 16 oktober 2026 | **CC0** (publiek domein): vrij te gebruiken, ook in de release, zonder naamsvermelding. Ik noem de maker toch in de credits. De licentie is gecontroleerd op de pagina |
| `assets/audio/House In a Forest Loop.ogg` | *House In a Forest Loop* © 2012 HorrorPen, via [OpenGameArt](https://opengameart.org/content/loop-house-in-a-forest) en de Godot-tutorial *Dodge the Creeps* | **CC BY 3.0**: vrij te gebruiken **met naamsvermelding** (zie de credits in de README) |
| `assets/audio/sfx/*.wav` (effecten, ook het game-over-geluid) | Zelf gegenereerd met `tools/maak_geluiden.py` uit sinusgolven en ruis | Eigen werk |
| `assets/fonts/Cinzel-Regular.ttf`, `Cinzel-Bold.ttf` | *Cinzel* © 2020 The Cinzel Project Authors, ontworpen door Natanael Gama, van [github.com/NDISCOVER/Cinzel](https://github.com/NDISCOVER/Cinzel) | SIL Open Font License 1.1 (zie `assets/fonts/LICENSE.txt`). Vrij te gebruiken en mee te leveren; de licentie moet erbij |
| `assets/art/ui/*.png` (kaders, knoppen, vinkvakjes en de sierlijn) | Zelf getekend met `tools/maak_ui.py` | Eigen werk |
| `icon.png`, `assets/art/icoon.ico` (spelicoon en exe-icoon) | Zelf getekend met `tools/maak_sprites.py` (de held op een groen vlak) | Eigen werk |

## Waarom alles zelf gemaakt is

In het begin zaten er gedownloade sprites van itch.io in het spel (een soldaat, vier demonen en een
magische pijl). Die hadden voorwaarden die het doorgeven van de losse bestanden verbieden, en dat
past slecht bij een repository die je met anderen wilt delen. Daarom zijn ze vervangen door eigen
tekeningen, zodat er geen licenties meer te controleren zijn behalve die van de muziek en het
lettertype. De oude bestanden staan nog in de commitgeschiedenis.

## Hoe de sprites gemaakt zijn

De tekeningen staan als tekstrijen in `tools/maak_sprites.py`: een letter per pixel, met een palet
per figuur. De omtrek wordt automatisch toegevoegd en de loop-animatie bestaat uit twee standen
die steeds wisselen met een klein sprongetje. `tools/pixelkunst.py` schrijft de PNG-bestanden zelf
(zlib), dus er is geen extern pakket nodig. Opnieuw maken: `py tools/maak_sprites.py`. Met
`--voorbeeld` komen er uitvergrote voorbeelden in `build/sprites/`.

De vijandsprites zijn vellen van 64x16 met vier frames van 16x16; de speler is 800x100 (lopen,
acht frames) en 600x100 (stilstaan, zes frames) van 100x100 per frame. Ze worden niet opgeknipt:
de `.tres` of de scene wijst met `AtlasTexture`-uitsnedes naar het vel.

## Opmerkingen

- **Muziek:** CC BY 3.0 verplicht tot naamsvermelding (HorrorPen, licentie CC BY 3.0). Dat staat in de
  credits van de README.
- **Game-over-geluid:** het bestand uit de Godot-tutorial had geen vermelde licentie en is
  vervangen door een eigen geluid.
