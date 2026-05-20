# Audit-Rules - Beispiel: B2B / Werkzeug & Industriebedarf

> ⚠️ **Inspiration, keine Vorgabe.** Dieses Beispiel zeigt wie eine ausgefüllte `audit-rules.md` für einen B2B-/Werkzeug-Store aussehen könnte. Übernimm es nur wenn die Werte tatsächlich für deinen Kunden passen.

---

## Title-Format

Pattern: `{Hersteller} {Artikelnummer} - {Produktname} ({wichtigste Spezifikation})`

Beispiele für gültige Titel:
- Bosch GBH 2-26 - Bohrhammer (830 W, SDS-plus)
- Hilti TE 3000-AVR - Abbruchhammer (2000 W)

Beispiele für ungültige Titel (zur Abgrenzung):
- bohrhammer (zu generisch, kein Hersteller, keine Spezifikation)
- Bosch Bohrhammer (ohne Artikelnummer und Specs)

## Beschreibung

- Cleanes HTML, keine inline styles
- Struktur: Einsatzbereich → technische Specs als Tabelle oder Liste → Lieferumfang → Hinweise (Sicherheit, Garantie)
- B2B-Sprache: faktisch, präzise, keine Marketing-Floskeln

## Pflicht-Metafelder

- `custom.hersteller_artikelnummer` (Hersteller-MPN)
- `custom.gewicht_kg`
- `custom.leistung_watt` (wo zutreffend)
- `custom.spannung_v`
- `custom.lieferumfang` (Liste der enthaltenen Teile)
- `custom.zulassung` (CE, GS, etc.)

Datenquellen für automatische Befüllung:
- `custom.hersteller_artikelnummer` → aus Title extrahieren wenn Pattern `{Hersteller} {Artikelnummer}` erkennbar
- `custom.leistung_watt`, `custom.spannung_v` → aus Beschreibung wenn explizit genannt
- `custom.zulassung` → aus Beschreibung wenn "CE", "GS-geprüft", "TÜV" erwähnt

## Meta Title & Meta Description

(SEO-Felder, NICHT Metafelder.)

Meta Title - max. 60 Zeichen, Pattern: `{Hersteller} {Artikelnummer} {Produktname}`

Meta Description - max. 155 Zeichen, muss Hersteller + Hauptspezifikation + Einsatzbereich + Lieferzeit enthalten

## Tags

- `b2b-only` → nur für gewerbliche Kunden sichtbar
- `lagerware` / `bestellware` → Verfügbarkeit
- `aktion` → bei aktivem Rabatt
- `auslaufmodell` → bei nicht mehr produzierten Modellen

## SKU-Pattern

Format: meist Hersteller-MPN direkt übernehmen, ergänzt um interne Lager-ID

Beispiel: `BOSCH-GBH226` oder `HILTI-TE3000AVR`

## Barcode/EAN

- 13-stellige EAN wo verfügbar
- Bei Eigenmarken oder Sonderbestellungen optional, aber MPN dann zwingend gepflegt

## Alt-Text Pattern

Pattern: `{Hersteller} {Artikelnummer} {Produktname} - Bild {n}`

Beispiel: `Bosch GBH 2-26 Bohrhammer - Bild 2`

## Vendor

Hier ist Vendor = Hersteller (nicht Brand des Stores).

Erlaubte Schreibweisen (immer Original-Schreibweise des Herstellers):
- Bosch (nicht `BOSCH`, `bosch`)
- Hilti
- Makita
- DeWalt (nicht `Dewalt`, `DEWALT`)

## Product Type

Erlaubte Werte (nach DIN/Branchen-Taxonomie):
- Bohrhämmer
- Schlagschrauber
- Sägen
- Schleifgeräte
- Messtechnik
- Verbrauchsmaterial

## Variant-Optionen Konsistenz

Bei Werkzeugen üblich: Spannung, Leistung, Akku-Konfiguration

Spannungen einheitlich: `12 V`, `18 V`, `36 V` (mit Leerzeichen, immer mit `V`)

Akku-Konfiguration einheitlich: `Solo` (ohne Akku), `1x Akku`, `2x Akku + Ladegerät`

## Variant-Naming

- Bei mehreren Variants: klare technische Namen mit Spannung/Leistung/Konfiguration
- Bei single-variant Produkten: "Default Title" akzeptabel (Shopify-Standard)

## Bilder-Anzahl

Mindestens **4 Bilder** pro Produkt (Hauptbild, Detailansicht, Lieferumfang, Anwendungssituation).

## Variant-Bild-Zuordnung

- Bei unterschiedlichen Akku-Konfigurationen: eigenes Bild zur Visualisierung des Lieferumfangs
- Bei reinen Spannungs-Variants ohne optische Unterschiede: kein eigenes Bild nötig
