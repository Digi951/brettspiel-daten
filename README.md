# brettspiel-daten

Kuratierte Brettspiel-Daten für BoardGameLog.

## awards.json

Gewinner von Spiel des Jahres, Kennerspiel des Jahres und Kinderspiel des
Jahres ab 2011. Wird von der App zur Laufzeit von
`raw.githubusercontent.com/Digi951/brettspiel-daten/main/awards.json` geladen
(Fallback: gebündelte Kopie in der App).

### Schema

```json
{ "version": 1, "language": "de", "updated": "YYYY-MM-DD", "awards": [ { "year": 2024, "category": "spiel|kennerspiel|kinderspiel", "title": "…", "description": "…" } ] }
```

Neue Felder dürfen ergänzt werden (die App ignoriert Unbekanntes). Unbekannte
`category`-Werte werden übersprungen.

### Pflege

Jährlich nach der Preisverleihung (Juli) die neuen Gewinner ergänzen und
`updated` aktualisieren. Quelle: https://www.spiel-des-jahres.de
