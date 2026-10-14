# Upgrade-ideeën

Ideeën voor upgrades die nog niet in het spel zitten. Dit is een keuzelijst, geen
plan: wat hier staat is nog niet gebouwd. Zet een vinkje bij wat je wilt hebben.

Al gebouwd: zwaardere kogels, sneller vuren, groter bereik, doorborende kogels,
extra levenspunten, herstel, sneller lopen en snellere dash.

Bij elk idee staat een inschatting van het werk:

- **Klein:** één waarde of een paar regels in bestaande code
- **Middel:** nieuw gedrag in kogel, wapen of speler
- **Groot:** nieuw systeem of nieuwe objecten

## Eigen ideeën

- [x] **Over water lopen** (middel): de speler kan over vijvers lopen. Dit maakt van een
  vijver een vluchtroute. Past bij de vliegende vijanden.
- [x] **Split shot** (middel): één kogel wordt twee of drie kogels in een waaier.
- [ ] **Bounce shot** (middel): een kogel kaatst op de muur terug het veld in.
- [x] **Ricochet** (middel): na een treffer springt de kogel naar de dichtstbijzijnde
  volgende vijand.
- [x] **Piercing** (klein): bestaat al als *Doorborende kogels*.

## Kogels

- [x] **Explosieve kogels** (middel): een treffer geeft schade in een klein gebied.
- [ ] **Zware kogels** (klein): meer knockback, maar een langzamere kogel.
- [x] **Snellere kogels** (klein): hogere kogelsnelheid. Handig tegen snelle vijanden.
- [ ] **Boemerang** (middel): de kogel vliegt terug en raakt vijanden een tweede keer.
- [x] **Kettingbliksem** (middel): een treffer springt naar 2-3 vijanden in de buurt.
- [x] **Vuur of gif** (middel): vijanden nemen schade over tijd.
- [x] **Bevriezing** (middel): treffers vertragen vijanden tijdelijk. Past goed bij de
  snelle Imps.
- [ ] **Kritieke treffer** (klein): kans op dubbele schade, met een geel flitsje.
- [ ] **Executie** (klein): extra schade op vijanden onder 20% levenspunten.
- [x] **Ringschot** (middel): af en toe schiet je in alle richtingen tegelijk.

## Wapen en doelen

- [ ] **Tweede wapen** (middel): een tweede loop die op een ander doel richt.
- [ ] **Doelwit kiezen** (middel): schiet op de zwakste, de snelste of de dichtstbijzijnde
  vijand.
- [ ] **Draaiende zwaarden** (groot): zwaarden die om je heen draaien en vijanden raken
  die te dichtbij komen.
- [x] **Schokgolf bij schade** (middel): als je geraakt wordt, duwt een golf vijanden
  weg.
- [x] **Mijnen** (middel): bij het dashen laat je een mijn achter.
- [ ] **Torentje** (groot): zet een tijdelijk autonoom torentje neer.

## Verdediging

- [ ] **Schild** (middel): een extra laag die één treffer opvangt en daarna oplaadt.
- [x] **Doornen** (klein): vijanden die je raken krijgen zelf schade.
- [x] **Levensdief** (klein): een klein deel van je schade geneest je.
- [ ] **Langere onkwetsbaarheid** (klein): de periode na een treffer wordt langer.
- [ ] **Tweede kans** (middel): eenmalig terugkomen met 30% HP als je doodgaat.
- [ ] **Schadereductie** (klein): elke treffer doet minder schade.
- [ ] **Regeneratie** (klein): langzaam HP herstellen tijdens een wave.
- [ ] **Meer herstel na een wave** (klein): groter deel van je HP terug na elke wave.

## Beweging en dash

- [x] **Dubbele dash** (middel): twee dashes achter elkaar voordat de cooldown begint.
- [ ] **Dash-schade** (middel): vijanden die je tijdens de dash raakt, krijgen schade.
- [ ] **Snelheidsboost na een kill** (klein): korte boost bij elke kill.
- [x] **Langere dash** (klein): meer afstand per dash.
- [ ] **Slow motion na dash** (middel): korte vertraging van alle vijanden.

## Beloningen en economie

Dit sluit aan op het XP-idee uit het Plan van Aanpak.

- [ ] **XP-orbs** (groot): vijanden droppen orbs die je oppakt.
- [ ] **Magneet** (klein, na XP-orbs): orbs trekken naar je toe.
- [ ] **Meer XP of munten** (klein, na XP-orbs): een bonus per kill.
- [ ] **Reroll** (klein): kies drie nieuwe upgrades, een paar keer per run.
- [ ] **Overslaan met bonus** (klein): een upgrade overslaan geeft extra HP of een andere
  beloning.
- [ ] **Zeldzaamheid** (middel): gewone, zeldzame en epische upgrades met verschillende
  sterkte.

## Risico en afwisseling

- [x] **Duivelsdeal** (middel): een sterke upgrade met een nadeel, bijvoorbeeld +50%
  schade maar snellere vijanden.
- [x] **Wave-modifiers** (groot): vóór een wave kies je een uitdaging in ruil voor een
  beloning.
- [x] **Vloek** (middel): extra vijanden in ruil voor een extra upgradekeuze.

## Aanbevolen volgorde

1. Split shot, bounce shot en ricochet: het zijn eigen ideeën, ze veranderen het wapen
   echt en sluiten aan op de bestaande `doorboor`-aanpak.
2. Over water lopen: uniek voor dit veld en het past bij de vliegende vijanden.
3. Bevriezing, schild en levensdief: helpt tegen de snelle vijanden en geeft een keuze
   tussen aanvallen en overleven.
4. Reroll en zeldzaamheid: weinig werk en het maakt de keuze tussen waves spannender.

## Let op bij object pooling

Kogels die splitsen, kaatsen of exploderen verhogen het aantal gelijktijdige
objecten flink. Dat is nuttig voor de meting in fase 7, maar houd de benchmark los
van de upgrades, zodat de metingen vergelijkbaar blijven.

## Status

**Gebouwd** (zie [upgrades.md](../ontwerp/upgrades.md)): split shot, ricochet,
piercing, explosieve kogels, snellere kogels, kettingbliksem, vuur en gif, bevriezing,
ringschot, schokgolf, mijnen, doornen, levensdief, dubbele dash, langere dash,
duivelsdeal, wave-modifiers, vloek en zeldzaamheid. Daarna toegevoegd: bounce shot,
boemerang, reroll, overslaan met bonus en synergieën.

**Bewust niet gebouwd:**

- *Over water lopen:* gebouwd en na een speeltest weer verwijderd.

- *XP-orbs en alles dat daarvan afhangt (magneet, meer XP):* de upgrades komen aan het
  einde van een wave, niet via level-ups.
- *Object pooling:* het verdiepingsonderwerp, dat zelf wordt uitgewerkt.
- *Zware kogels, kritieke treffer, executie, tweede wapen, doelwit kiezen, draaiende
  zwaarden, torentje, schild, langere onkwetsbaarheid, tweede kans, schadereductie,
  regeneratie, meer herstel, dash-schade, snelheidsboost na een kill, slow motion na
  dash:* niet aangevinkt.
