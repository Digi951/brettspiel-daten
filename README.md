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
