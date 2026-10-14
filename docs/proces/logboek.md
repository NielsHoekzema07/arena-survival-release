# Logboek

Per week: bestede uren, wat er af is, en welk probleem is tegengekomen met de oplossing. Ook geraadpleegde bronnen (titel + link + Godot-versie) horen hier.

---

## Week 1 — Oriëntatie en voorbereiding

**Uren:** 10
**Gedaan:**

- Onderwerp afgebakend en Plan van Aanpak geschreven
- Godot 4.7.2 geïnstalleerd
- Git-repository opgezet met projectstructuur en README

**Problemen en oplossingen:**

**Bronnen:**

---

## Week 2 — Engine leren

**Uren:** 10
**Gedaan:**

- Officiële tutorial *Your first 2D game* volledig doorlopen (aparte repository `dodge-the-creeps`)

**Wat ik heb geleerd:**

- Scene- en node-structuur:
- Verschil `_process` en `_physics_process`:
- Gebruik van `delta`:
- `@export` / `[Export]`:
- Signals:

**Problemen en oplossingen:**

**Bronnen:**

---

## Week 3 — Speler en besturing

**Uren:** 10
**Periode:** 9 september (commits in de git-geschiedenis)
**Gedaan:**

- Speler als `CharacterBody2D` met 8-richtingen beweging via de input map (`get_vector`, dus diagonaal niet sneller)
- Camera die de arena-rand volgt en er niet buiten kijkt
- Arena met raster op de vloer om beweging zichtbaar te maken
- Arena-afmeting op één plek vastgelegd (`Speelveld.GROOTTE`); vloer, muren, camera en spawner lezen daar hun maat uit
- Collision layers vastgelegd in `docs/collision-layers.md` (player, enemy, player_bullet, pickup, world)

**Problemen en oplossingen:**

- *Speler moet door vijanden heen kunnen lopen en toch schade krijgen.* Een `CharacterBody2D` botst met alles in zijn mask. Daarom botst de body alleen op muren en zit de aanraking met vijanden in een aparte `Area2D` (hurtbox). Uitleg staat in de collision-layers-doc.

**Bronnen:**

---

## Week 4 — Vijandsysteem

**Uren:** 10
**Periode:** 9 - 11 september
**Gedaan:**

- Vijandscene die de speler achtervolgt (`direction_to` en `move_and_slide`)
- Spawner die vijanden buiten beeld laat verschijnen, met een Timer als spawninterval
- Vijanden zoeken de speler via de groep `player` en niet via een vast pad

**Problemen en oplossingen:**

- *Vijanden kruipen uiteindelijk allemaal op hetzelfde punt.* Ze krijgen `enemy` in hun eigen mask zodat ze elkaar wegduwen. Dat kost physics-tijd; gemeten (RTX 3060 laptop, headless): bij 500 vijanden 20 ms in plaats van 7 ms per frame. Zie `docs/collision-layers.md`. Dit is belangrijk voor de pooling-meting: botsing en pooling zijn twee losse kostenposten.

**Bronnen:**

---

## Week 5 — Wapen- en levenssysteem

**Uren:** 10
**Periode:** 11 - 18 september
**Gedaan:**

- Wapen dat automatisch op de dichtstbijzijnde vijand schiet, met zichtbaar bereik (gestreepte cirkel)
- Projectielen als `Area2D` met collision layers; ze ruimen zichzelf op buiten het speelveld
- Levenspunten (start op 1000 zodat percentages niet wegrondden), onkwetsbaarheid van 0,5 s na een treffer, game over en herstart
- Vijanden hebben levenspunten en gaan pas na meerdere treffers dood

**Problemen en oplossingen:**

- *Speler kreeg bij elke spawn schade uit het niets.* `add_child` werd aangeroepen voordat de vijand op zijn plek stond, waardoor Godot de body aanmeldde op de positie van de spawner (het midden van de arena) en de hurtbox van de speler dat als treffer zag. Gemeten: zes phantom-treffers in 400 frames, precies op het spawninterval. Opgelost met de volgorde: instantieren, eigenschappen zetten, dan pas `add_child`. Dezelfde fout zat in het wapen. Dit geldt ook voor object pooling later.
- *Bij 5 levenspunten rondt een vermenigvuldiging weg* (3 schade × 0,9 blijft 3). Daarom start de speler op 1000.

**Bronnen:**

---

## Week 6 — Progressiesysteem

**Uren:** 10
**Periode:** 18 september - 2 oktober
**Gedaan:**

- Drie vijandtypes (daarna vier) via `VijandType`-resources: waarden in plaats van aparte scriptklassen, zodat er straks maar één object pool nodig is (`docs/vijandtypes.md`)
- Vliegende vijanden die over vijvers gaan; natuurlijke arena met vijvers en decoratie
- Eerst tijdgebaseerde golven van 30 s, daarna een echt wave-systeem (`WaveManager`): aftellen, vechten, wave voltooid, upgradekeuze, volgende wave (`docs/waves.md`)
- Speelveld verkleind van 5000x3000 naar 2000x1200
- Vijanden sneller dan de speler (Imp 340, Eye 310, Blackguard 260, Abomination 120 tegenover 300), een dash met onkwetsbaarheid en een spawnwaarschuwing
- Upgrades: 35 stuks in drie zeldzaamheden, kogeleffecten (split, ricochet, explosie, bliksem, vuur, gif, bevriezing, ringschot), duivelsdeals, vloek en uitdagingen vóór een wave (`docs/upgrades.md`)
- Nieuwe HUD en nieuwe mappenstructuur
- Vijandvariatie: schieter, splitter en vijand met schild; elites; eindbazen elke 5e wave; pickups (hartje, woede, spoed)
- Upgrades uitgebreid: bounce shot, boemerang, herrollen, overslaan en synergieën

**Problemen en oplossingen:**

- *Moeilijkheidsfactoren in de resource schrijven werkt niet.* Een `.tres` is gedeeld: schrijf je erin, dan worden vijanden op het scherm met terugwerkende kracht sterker. Factoren worden daarom bij het spawnen toegepast.
- *Een wave bleef hangen op één vijand die achter een vijver vastzat.* Opgelost met een vangnet: na 20 s zonder kill worden achterblijvers verplaatst.
- *Sterke upgrade-combinaties maakten de run eindeloos makkelijk* (bot haalde wave 30). Opgelost door de HP-groei per wave deels kwadratisch te maken.
- *`Bullet.tscn` met hoofdletter* gaf een waarschuwing omdat het niet op Linux/macOS zou werken; hernoemd. Een verouderde uid in `player.tscn` hersteld.
- *Balans controleren zonder zelf te spelen:* een testscript dat headless een bot laat spelen (vluchten, dashen, upgrades kiezen). Dat is een indicatie, geen bewijs; de echte test is spelen.

**Wat nog moet:** zelf spelen en bijstellen (moeilijkheid, tempo, upgrades, uitdagingen).

**Bronnen:**

---

## Week 7 — Verdieping: object pooling

**Uren:** _
**Status:** nog niet begonnen. Dit is het verdiepingsonderwerp en volgt na het afronden van de game. De git-tag `v1-geen-pooling` moet gezet worden vóór er pooling wordt toegevoegd, zodat er een baseline is.

---

## Week 8 — Testen en afwerking

**Uren:** _ (de onderdelen hieronder zijn al gebouwd tijdens week 5 en 6; die uren staan daar)
**Gedaan (vooruit op de planning):**

- Hoofdmenu, pauzescherm en instellingen (volumes, schermtrilling, schadecijfers)
- Geluid: muziek en 15 effecten op twee audiobussen. De effecten zijn zelf gegenereerd met `tools/maak_geluiden.py`, zodat ze licentievrij zijn
- Records en instellingen bewaard in `user://voortgang.cfg`
- Game feel: schermtrilling, hit-stop, schadecijfers, deeltjes bij inslag en doodgaan
- Prestatie-overlay op F3 (FPS, frametijd, nodes, aantal vijanden en kogels)
- Hint over de besturing in de eerste runs

**Problemen en oplossingen:**

- *Een lichaam toevoegen in een physics-callback geeft een fout* ("Can't change this state while flushing queries"). Gebeurde toen een splitter doodging door een kogel en zijn kleintjes meteen werden gemaakt. Opgelost met `call_deferred`.
- *Sterke upgrade-combinaties maakten een run onverslaanbaar* (een bot haalde wave 25 zonder schade). Daarom groeit het aantal vijanden tegelijk vanaf wave 9 en groeit de HP kwadratisch.
- *Een schieter die buiten het wapenbereik blijft is niet te doden en laat de wave hangen.* De afstand van de schieter ligt daarom onder het bereik van het wapen.
- *De speler werd na een speeltest te snel te sterk.* Stat-upgrades verlaagd, zeldzame upgrades later en trager waarschijnlijk, herstel verlaagd en vijanden sneller zwaarder gemaakt. Over water lopen is verwijderd.
- *Een testscript schreef records naar het echte opslagbestand van de speler.* Na elke testrun verwijder ik `user://voortgang.cfg`.

---

## Week 9 — Documentatie en presentatie

**Uren:** _

---

## Week 10 — Buffer en reflectie

**Uren:** _
