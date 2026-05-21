# Feld-spezifische Audit-Regeln

Bewertungs-Referenz pro Feld **wenn das Feld im Scope ist**. Keine Checkliste, die proaktiv abgearbeitet wird — Audit-Scope ergibt sich immer aus Live-Daten + User-Vorgabe (siehe SKILL.md Phase 2). Wenn ein Feld im aktuellen 20er-Batch nirgends auftaucht, **nicht prüfen**.

## Inhalt & Identifier

### Title-Format
Pattern aus Mehrheit der Produkte ableiten (z.B. 70%-Match = Referenz). Produkte die abweichen = Befund. Wenn kein klares Mehrheits-Pattern erkennbar: melden, beim User nachfragen.

### Beschreibung (Body HTML)
- cleanes HTML, keine inline styles
- Struktur konsistent über den Batch
- keine Word-Artefakte (`<o:p>`, `mso-*`, leere `<span>`)

### Vendor
Gesetzt, konsistent geschrieben. Varianten wie `acme` / `ACME` / `Acme Inc.` zählen als Befund.

### Product Type
Gesetzt, aus definierter Taxonomie (siehe `audit-rules.md` falls vorhanden).

### Handle
Im Audit-Default nicht prüfen — Handle-Änderungen brechen URLs. Nur prüfen wenn User explizit verlangt.

## Metafelder

### Bestehende Metafelder
Werte plausibel und vollständig wo gepflegt. Leere Strings zählen als Befund (gegenüber `null`).

### Fehlende Metafelder
Definierte Metafelder (aus `audit-rules.md` oder User-Vorgabe) sind leer.

### Niemals löschen
**`global.title_tag` und `global.description_tag` sind API-Aliasse von `seo.title` / `seo.description` — eine Speicherstelle, zwei Namen.** Löschen entfernt auch den `seo`-Wert und korrumpiert das SEO-Feld. Nie als „doppelt" melden. Namespace `global` im Allgemeinen in Ruhe lassen.

## SEO

### Meta Title & Meta Description
Das sind **SEO-Felder** (Search Engine Listing Preview), **nicht** Metafelder. Im Report immer als „Meta Title" / „Meta Description" bezeichnen, klar getrennt von Custom-Metafields.

Storage: liegen auf den oben genannten `seo.title` / `seo.description` Werten (bzw. ihren `global.*_tag` Aliassen).

## Identifier-Felder

### SKU-Format
Entspricht Pattern aus `audit-rules.md`. Wenn keine Regel definiert: nur Konsistenz prüfen (alle SKUs leer = Befund; gemischte Formate ohne Mehrheit = Rückfrage).

### Barcode / EAN
**Präzise melden, nie generisch:**
- „fehlt komplett" / „ungültiges Format (X Stellen statt 13)" / „doppelt vergeben mit Produkt Y"
- Kein generisches „Barcode-Problem"
- Pro Variant melden, nicht pro Produkt — ein Produkt kann teil-befüllt sein

## Visuals

### Alt-Texte
**Mit Image-Index melden:**
- „Bild 2 von 4 hat keinen Alt-Text"
- „alle 4 Bilder ohne Alt-Text"

Nie einfach „Alt-Text fehlt" ohne welches Bild.

### Bilder-Anzahl
Mindestschwelle aus `audit-rules.md` oder User-Vorgabe. Ohne Regel keine Schwelle erfinden.

### Variant-Bild-Zuordnung
Jede Variant hat ein eigenes Bild (wenn vom Store so vorgesehen — Größen-Variants brauchen i.d.R. kein eigenes Bild, Farb-Variants schon).

## Variants

### Variant-Optionen Konsistenz
Schreibweisen einheitlich. Klassiker: „Schwarz" vs. „schwarz" vs. „Black" vs. „Noir" am selben Produkt-Set.

### Variant-Naming
**„Default Title" ist nur bei Multi-Variant-Produkten ein Befund.** Bei single-variant ist es Shopify-Standard, kein Bug, nie als Finding listen.

## Tags

### Pflicht-Tags
Gemäß `audit-rules.md`. Casing/Pattern wie definiert. Ohne Regel: nur strukturelle Inkonsistenzen prüfen (z.B. `sale` vs. `Sale` vs. `SALE` am selben Store).
