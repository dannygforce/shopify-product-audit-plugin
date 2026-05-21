# Audit-Rules-Resolution — Interview statt Halluzination

Lade diese Datei, wenn der User dich auffordert eine `audit-rules.md` zu **schreiben**: „schreib mir eine audit-rules.md", „mach mir best practices", „kannst du Regeln vorschlagen", „leg eine an mit Defaults", o.ä.

## Warum kein Default-Set

Title-Zeichen-Limits, Meta-Title-Ranges, EAN-Pflicht, Bilder-Mindestanzahl, Alt-Text-Limits, Tag-Casing-Defaults sind **erfundene Schwellen ohne Quelle**, sobald sie nicht vom Store-Besitzer kommen. Sie wirken plausibel, sind aber gegen den falschen Store gemessen.

Eine `audit-rules.md` mit halluzinierten Defaults korrumpiert alle späteren Audit-Läufe still — der Skill bezieht die Schwellen daraus und meldet Findings gegen Werte, die der Kunde nie bestätigt hat. Lieber unvollständige Datei als halluzinierte.

## Ablauf

### 1. Refuse generische Best-Practices

Sag dem User wörtlich (oder sinngemäß) das hier:

> Generische Best-Practices kann ich nicht erfinden — die hängen von deinem Store, deinen Kanälen und deiner Lieferanten-Realität ab. Ich kann aber mit dir 5–10 Fragen durchgehen und **deine** Antworten in `audit-rules.md` festhalten.

### 2. Interview-Modus

Strukturierte Fragen, **einzeln nacheinander**, mit konkreten Beispiel-Werten zur Orientierung — aber **keine Default-Antwort vorschlagen**, die der User nur abnicken muss.

**Mindest-Set an Fragen:**
- Title-Pattern
- Pflicht-Metafelder (`namespace.key` + Datentyp)
- SKU-Format (inkl. Beispiel)
- Vendor-Konsistenz-Erwartung (welche Schreibweisen sind erlaubt)
- Bilder-Mindestanzahl
- Alt-Text-Pflicht-Felder
- Tag-Convention (Casing/Pattern)
- Barcode-Pflicht je Sales-Channel
- Meta-Title / Meta-Description-Range (falls SEO-relevant für den Store)

### 3. Nur User-Antworten festhalten

Jede Regel in der entstehenden `audit-rules.md` bekommt eine Quelle-Zeile:

```
Quelle: Interview {YYYY-MM-DD}
```

Wenn der User zu einer Frage „weiß nicht / überspringen" sagt: **Regel weglassen**, nicht mit Default füllen. Die fehlende Regel führt im Audit dazu, dass das jeweilige Feld nicht geprüft wird — das ist korrektes Verhalten, kein Bug.

### 4. Druck-Phrasen abblocken

Wenn der User mitten im Interview sagt:
- „mach einfach was Sinnvolles"
- „nimm Defaults"
- „du weißt schon"
- „spiel halt was rein, ich schau drüber"

→ Hard Stop, Interview wiederholen. Wörtlich (oder sinngemäß):

> Ich kann keine Defaults setzen, die du nicht bestätigt hast — die landen sonst still in deinem Audit-Lauf. Sag mir lieber pro Frage „überspringen", dann lass ich die Regel weg.

### 5. Existing-Daten als Quelle (zulässige Abkürzung)

Wenn der User sagt „nimm das Title-Pattern aus den ersten 10 Produkten" oder ähnlich:

1. Stichprobe ziehen (max 10 Produkte, MCP)
2. Pattern als Vorschlag ausgeben (z.B. „14 von 16 folgen `{Brand} {Name} - {Kategorie}`")
3. User explizit bestätigen lassen — nicht still übernehmen
4. Regel in `audit-rules.md` festhalten mit Quelle: `Quelle: Stichprobe aus Store {X} am {Datum}`

## Verwandte Files

- Leeres Template zum manuellen Befüllen: `references/audit-rules-template.md`
- Ausgefüllte Branchen-Beispiele (Inspiration, **nicht** Vorgabe): `references/examples/`
