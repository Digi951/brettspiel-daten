# brettspiel-daten

Kuratierte Brettspiel-Daten für BoardGameLog.

## awards.json

Gewinner von Spiel des Jahres (ab 1979), Kennerspiel des Jahres (ab 2011) und
Kinderspiel des Jahres (ab 2001). Wird von der App zur Laufzeit von
`raw.githubusercontent.com/Digi951/brettspiel-daten/main/awards.json` geladen
(Fallback: gebündelte Kopie in der App).

### Schema

```json
{ "version": 1, "language": "de", "updated": "YYYY-MM-DD", "awards": [
  { "year": 2024, "category": "spiel|kennerspiel|kinderspiel", "title": "…", "description": "…",
    "translations": { "en": { "title": "…", "description": "…" } },
    "aliases": ["…"] }
] }
```

Neue Felder dürfen ergänzt werden (die App ignoriert Unbekanntes). Unbekannte
`category`-Werte werden übersprungen.

`translations` und `aliases` sind optional. `translations.<sprachcode>.title`
ist Pflicht, sobald der Sprachcode auftaucht; `description` ist optional.

### Pflege

Jährlich nach der Preisverleihung (Juli) die neuen Gewinner ergänzen und
`updated` aktualisieren. Quelle: https://www.spiel-des-jahres.de

## awards/fr.json

Länderpreis für französische App-Sprache: **As d'Or** (Festival International
des Jeux, Cannes), Kategorien Jeu de l'Année, Jeu Expert, Jeu Initié, Jeu Enfant,
Jahrgänge ab 2012 (Initié ab 2022). Die App lädt die Datei nur, wenn ihre
Sprache `fr` ist; alle anderen Sprachen bleiben beim Spiel des Jahres. Ein 404
bedeutet „kein Länderpreis für diese Sprache".

```json
{ "version": 1, "language": "fr", "updated": "YYYY-MM-DD",
  "awardName": "As d'Or",
  "categories": [ { "id": "annee", "label": "Jeu de l'Année", "short": "Année" } ],
  "awards": [
    { "year": 2023, "category": "annee", "title": "Akropolis",
      "description": "…", "aliases": ["…"] }
  ] }
```

- `categories` bestimmt Reihenfolge und Tab-Beschriftung in der App (`short`
  im Picker, `label` in der Wunschlisten-Notiz). Einträge mit einer `category`,
  die in `categories` fehlt, überspringt die App.
- Titel und Beschreibung sind direkt französisch (kein `translations`-Block).
- `description` optional: nur bei sicher bekannten Spielen, sonst weglassen.
- `aliases` optional, nur fürs Matching gegen Sammlung/Wunschliste.
- Expert hieß 2012–2015 „Grand Prix du Jury" und läuft hier unter `expert`.
  Der „Prix du Jury" dieser Jahre ist nicht enthalten.
- **Pflege:** jährlich im **Februar/März** nach dem Festival in Cannes (nicht
  im Juli). Quelle: https://www.festivaldesjeux-cannes.com/label-as-d-or/palmares/
  plus eine zweite Quelle zur Gegenprobe; `updated` setzen und die gebündelte
  Kopie `Resources/awards-fr.json` der App synchron halten.

## awards/es.json und awards/it.json

Weitere Länderpreise nach demselben Schema wie `awards/fr.json`, je mit **einer**
Kategorie (die App blendet dann die Tab-Leiste aus; ist das Kategorie-`label`
gleich dem `awardName`, steht die Kategorie nicht doppelt in der Notiz):

- **es** — *Premio JdA* (Juego del Año en España), Jurado JdA, ab 2012.
  Quelle: https://premio-jda.es (Beiträge „Premio JdA <Jahr>"). Der Kinderpreis
  JdAI existiert erst seit 2024 und ist (noch) nicht enthalten.
- **it** — *Gioco dell'Anno* (Lucca Comics & Games), erstmals 2013 vergeben.
  Quelle: https://www.giocodellanno.it/albo-doro-gioco-dellanno/. Rollenspiel-,
  Designer- und Sonderpreise sind bewusst nicht enthalten.

**Pflege:** Der Premio JdA wird im **Oktober** vergeben (2025: 12. Oktober), der
Gioco dell'Anno bei Lucca Comics & Games Ende **Oktober/Anfang November**. Beide
Jahrgänge 2026 fehlen, bis die Preise vergeben sind. Danach `updated` setzen und
die gebündelten Kopien `Resources/awards-es.json` / `awards-it.json` der App
synchron halten.

## Kompatibilitäts-Kontrakt

- Bestehende Felder werden **nie umbenannt oder entfernt**, nur ergänzt.
- `title`/`description` sind immer das deutsche Original; Übersetzungen leben
  ausschließlich in `translations.<sprachcode>` (`title` Pflicht,
  `description` optional).
- `aliases` (optional) enthält zusätzliche Titelvarianten nur für den
  Sammlungs-Abgleich in der App — sie werden nie angezeigt.
- Die URL `…/main/awards.json` bleibt dauerhaft bestehen und liefert die
  deutsche Liste. Ein späterer Landespreis-Ausbau fügt nur `manifest.json` +
  `awards/<locale>.json` hinzu.
- Bei EN-Titeln gilt: im Zweifel weglassen (App fällt auf Deutsch zurück),
  niemals raten.
