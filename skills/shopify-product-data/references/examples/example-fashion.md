# Audit-Rules - Beispiel: Fashion / Apparel

> ⚠️ **Inspiration, keine Vorgabe.** Dieses Beispiel zeigt wie eine ausgefüllte `audit-rules.md` für einen Fashion-Store aussehen könnte. Übernimm es nur wenn die Werte tatsächlich für deinen Kunden passen.

---

## Title-Format

Pattern: `{Brand} {Produktname} - {Kategorie}`

Beispiele für gültige Titel:
- Acme Pullover Hoodie - Oberteile
- Brand X Slim Fit Jeans - Hosen

Beispiele für ungültige Titel (zur Abgrenzung):
- pullover hoodie (klein, ohne Brand, ohne Kategorie)
- ACME HOODIE BLACK (Caps, falsches Pattern)

## Beschreibung

- Cleanes HTML, keine inline styles
- Struktur: Intro-Absatz → Bullet-Liste mit Features → Specs-Block → CTA
- Erste Sätze unter 160 Zeichen für SEO-Snippet-Tauglichkeit
- Keine Word-Artefakte (`<o:p>`, `mso-*`, leere `<span>`)

## Pflicht-Metafelder

- `custom.material` (z.B. "Baumwolle", "Polyester")
- `custom.pflege` (Pflegehinweise)
- `custom.passform` (z.B. "Slim Fit", "Regular")
- `custom.herkunft` (Herstellungsland)

Datenquellen für automatische Befüllung:
- `custom.material` → aus Beschreibung extrahieren wenn Begriffe wie "100% Baumwolle", "Polyester-Mix" vorkommen
- `custom.pflege` → aus Beschreibung wenn "30°C", "Handwäsche", "nicht bügeln" etc. erwähnt
- `custom.passform` → aus Title/Beschreibung wenn "Slim", "Regular", "Oversize" erwähnt

## Meta Title & Meta Description

(SEO-Felder, NICHT Metafelder.)

Meta Title - max. 60 Zeichen, Pattern: `{Produktname} | {Brand}`

Meta Description - max. 155 Zeichen, muss Brand + Hauptbenefit + CTA enthalten

## Tags

- `bestseller` → wenn Verkäufe in Top 10% (manuell setzen, nicht automatisch)
- `sale` → wenn `compare_at_price > price`
- `new` → wenn `published_at` < 30 Tage
- `nachhaltig` → bei zertifizierten Materialien (GOTS, Bluesign)

## SKU-Pattern

Format: `{BrandKürzel}-{Kategorie}-{Farbe}-{Größe}`

Beispiel: `ACME-HOOD-BLK-M`

Regex: `^[A-Z]{2,5}-[A-Z]{3,5}-[A-Z]{2,4}-(XS|S|M|L|XL|XXL|\d+)$`

## Barcode/EAN

- Pflicht auf allen Variants
- 13-stellige EAN

## Alt-Text Pattern

Pattern: `{Produktname} - {Variant-Name} - Bild {n}`

Beispiel: `Acme Pullover Hoodie - Schwarz M - Bild 2`

## Vendor

Erlaubte Schreibweisen (case-sensitive):
- Acme
- Brand X
- Lieferant Y

Häufige Inkonsistenzen die zu fixen sind:
- `acme`, `ACME`, `Acme Inc.` → alle zu `Acme`

## Product Type

Erlaubte Werte:
- Oberteile
- Hosen
- Accessoires
- Schuhe

## Variant-Optionen Konsistenz

Farben (deutsch, kein Mix mit Englisch/Französisch):
- Schwarz (nicht `schwarz`, `Black`, `Noir`)
- Weiß (nicht `weiss`, `White`)
- Rot (nicht `rot`, `Red`)

Größen-Format: `XS`, `S`, `M`, `L`, `XL`, `XXL` (Großbuchstaben, keine Punkte)

## Variant-Naming

- Bei mehreren Variants: klare Namen, kein "Default Title"
- Bei single-variant Produkten: "Default Title" akzeptabel (Shopify-Standard)

## Bilder-Anzahl

Mindestens **3 Bilder** pro Produkt.

## Variant-Bild-Zuordnung

- Jede Farb-Variant muss ein eigenes Bild zugewiesen haben
- Größen-Variants müssen kein eigenes Bild haben
