# Audit-Rules - Beispiel: Skincare / Cosmetics

> ⚠️ **Inspiration, keine Vorgabe.** Dieses Beispiel zeigt wie eine ausgefüllte `audit-rules.md` für einen Skincare-/Cosmetics-Store aussehen könnte. Übernimm es nur wenn die Werte tatsächlich für deinen Kunden passen.

---

## Title-Format

Pattern: `{Produktcode} {Produktname}`

Beispiele für gültige Titel:
- BW1 2-in-1 Hair & Body Wash
- FC3 Anti-Aging Face Cream

Beispiele für ungültige Titel (zur Abgrenzung):
- bw1 hair body wash (klein, falsche Reihenfolge)
- 2-in-1 Hair & Body Wash (Produktcode fehlt)

## Beschreibung

- Cleanes HTML, keine inline styles
- Struktur: Hero-Headline (h2) → Intro-Absatz → Bullet-Liste mit Wirkstoffen/Benefits → Anwendungshinweis → INCI-Liste am Ende
- Mindestens ein USP im Intro (z.B. "frei von Parabenen", "vegan")

## Pflicht-Metafelder

- `custom.inci` (vollständige INCI-Inhaltsstoffliste)
- `custom.anwendung` (Anwendungshinweise)
- `custom.fuellmenge_ml` (Volumen in ml)
- `custom.hauttyp` (z.B. "Alle Hauttypen", "Trockene Haut", "Empfindliche Haut")
- `custom.frei_von` (z.B. "Parabene, Silikone, Mikroplastik")

Datenquellen für automatische Befüllung:
- `custom.fuellmenge_ml` → aus Title oder Beschreibung extrahieren ("250ml", "100 ml")
- `custom.frei_von` → aus Beschreibung wenn "ohne X", "frei von X" erwähnt
- `custom.hauttyp` → aus Beschreibung wenn explizit genannt

## Meta Title & Meta Description

(SEO-Felder, NICHT Metafelder.)

Meta Title - max. 60 Zeichen, Pattern: `{Produktname} - {Hauptbenefit} | {Brand}`

Meta Description - max. 155 Zeichen, muss Brand + Hauttyp + Hauptwirkstoff + CTA enthalten

## Tags

- `bestseller` → wenn Verkäufe in Top 10% (manuell setzen)
- `vegan` → wenn als vegan gekennzeichnet
- `mens` / `womens` / `unisex` → Zielgruppe
- `routine-essential` → für Basisprodukte einer Pflegeroutine

## SKU-Pattern

Format: `{ProduktcodeKürzel}-{FüllmengeMl}`

Beispiel: `BW1-250`

## Barcode/EAN

- Pflicht auf allen Variants
- 13-stellige EAN

## Alt-Text Pattern

Pattern: `{Produktname} {Füllmenge} - Bild {n}`

Beispiel: `BW1 2-in-1 Hair & Body Wash 250ml - Bild 2`

## Vendor

Erlaubte Schreibweisen:
- (eine konsistente Schreibweise pro Brand, hier eintragen)

## Product Type

Erlaubte Werte:
- Reinigung
- Pflege
- Anti-Aging
- Sonnenschutz
- Set / Geschenkbox

## Variant-Optionen Konsistenz

Füllmengen einheitlich:
- 50 ml, 100 ml, 200 ml, 250 ml (mit Leerzeichen vor "ml")
- Nicht: `250ml`, `250ML`, `250milliliter`

## Variant-Naming

- Bei verschiedenen Größen: klare Variant-Namen mit Füllmenge
- Bei single-variant Produkten: "Default Title" akzeptabel (Shopify-Standard)

## Bilder-Anzahl

Mindestens **3 Bilder** pro Produkt (Packshot frontal, Lifestyle/Anwendung, Detailshot Inhaltsstoffe oder Textur).

## Variant-Bild-Zuordnung

- Größen-Variants müssen kein eigenes Bild haben (Packshot-Größenunterschied minimal)
- Bei verschiedenen Düften/Sorten: jede Sorte braucht eigenes Bild
