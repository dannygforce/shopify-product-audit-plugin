# CSV-Backup-Format (Shopify Product Export)

Format des automatischen Backups vor jedem Push (siehe SKILL.md Phase 6). Spiegelt das native Shopify Admin → Products → Export Format wider, damit der User das CSV bei Bedarf auch ohne diesen Skill re-importieren kann.

## Pfad & Naming

- macOS / Linux: `~/Downloads/`
- Windows: `%USERPROFILE%\Downloads\` bzw. `pathlib.Path.home() / "Downloads"`
- Filename: `shopify-audit-backup-{YYYY-MM-DD}-batch-{N}.csv`

**Bestehende Dateien nie überschreiben.** Vor dem Schreiben Existenz prüfen, bei Konflikt `N+1` bis frei. Wenn du Python verwendest: open mode `'x'` (exclusive create), reagiere auf `FileExistsError` mit `N+1`. Bei Bash-Redirect: `[ -f path ] && N=$((N+1))` Loop. Verhaltensgarantie: kein Backup überschreibt je ein vorhandenes.

## Scope pro CSV

Eine Backup-Datei = **die 20 Produkte des aktuellen Batches**, mit **Original-Werten aller Felder** (nicht nur die betroffenen) — so ist auch Drift auf Nicht-Ziel-Feldern rollback-fähig.

**Beispiel — User-Scope 27 Produkte:**
- Batch 1: pull 20 → audit → diff → `batch-1.csv` mit diesen 20 → push → verify → Pause + Bestätigung
- Batch 2: pull nächste 7 → `batch-2.csv` mit diesen 7 → audit → push → verify

Falsch wäre: ein Pull `first: 50` + ein Mega-CSV mit 27 Zeilen.

## Spalten (in dieser Reihenfolge)

```
Handle, Title, Body (HTML), Vendor, Product Category, Type, Tags, Published,
Option1 Name, Option1 Value, Option2 Name, Option2 Value, Option3 Name, Option3 Value,
Variant SKU, Variant Grams, Variant Inventory Tracker, Variant Inventory Qty,
Variant Inventory Policy, Variant Fulfillment Service, Variant Price, Variant Compare At Price,
Variant Requires Shipping, Variant Taxable, Variant Barcode,
Image Src, Image Position, Image Alt Text,
Gift Card, SEO Title, SEO Description, Variant Image, Variant Weight Unit, Variant Tax Code,
Cost per item, Price / International, Compare At Price / International, Status
```

## Mehrzeiligkeit

Produkte mit mehreren Variants oder Bildern werden mehrzeilig geschrieben, exakt wie Shopify nativ exportiert:
- Erste Zeile: voller Produkt-Daten-Block
- Folgezeilen: nur `Handle` + die jeweiligen Variant- bzw. Image-Spalten, alle anderen leer

## Was das CSV NICHT enthält

**Custom Metafields werden vom Shopify Product Export nicht abgebildet.** Wenn der aktuelle Push Custom-Metafield-Schreibvorgänge enthält (z.B. `custom.material`, `custom.passform`), reicht dieses CSV als alleiniger Rollback-Pfad nicht — siehe SKILL.md Phase 6 (Pre-Push Warnung) und Undo-Flow.

## Hard-Stop bei Backup-Fehler

**Wenn der Schreibvorgang fehlschlägt: kein Push.** Erlaubt sind nur:
- (a) Write erneut versuchen, falls der User in der Zwischenzeit eine Permission erteilt hat
- (b) Hard Stop mit präziser Fehlermeldung (Pfad + OS-Fehler) + Bitte um Permission

Nicht erlaubt: alternative Pfade (Downloads bleibt Downloads), User-getipptes CSV als Ersatz, Push „weil Backup nur Sicherheitsnetz ist". Nach Hard Stop stößt der User den Push neu an.
