# Audit-Rules

Kopiere diese Datei als `audit-rules.md` ins Projekt-Root deines Shopify-Stores und fülle die Regeln pro Kunde aus. Der Skill liest diese Datei automatisch wenn vorhanden.

Lass Sektionen leer wenn der entsprechende Audit-Punkt nicht geprüft werden soll. In dem Fall fragt der Skill den User im Chat ab.

Im Ordner `examples/` findest du ausgefüllte Vorlagen für typische Branchen als Inspiration - nicht als Vorgabe. Jeder Store ist anders.

---

## Title-Format

Pattern:

Beispiele für gültige Titel:
-
-

Beispiele für ungültige Titel (zur Abgrenzung):
-
-

## Beschreibung

Vorgaben für sauberes HTML, Struktur, Stilelemente:
-
-

## Pflicht-Metafelder

Metafelder die in jedem Produkt befüllt sein müssen:
-
-

Datenquellen für automatische Befüllung (welches Metafeld kann aus welcher Quelle abgeleitet werden):
-
-

## Meta Title & Meta Description

(SEO-Felder, NICHT Metafelder.)

Meta Title - max. Zeichen, Pattern:

Meta Description - max. Zeichen, Pflicht-Inhalte:

## Tags

Pflicht-Tags und ihre Bedingungen:
-
-

## SKU-Pattern

Format:

Beispiel:

Regex (optional):

## Barcode/EAN

Anforderungen (z.B. 13-stellige EAN, GTIN, optional, Pflicht auf allen Variants):

## Alt-Text Pattern

Pattern:

Beispiel:

## Vendor

Erlaubte Schreibweisen:
-
-

Häufige Inkonsistenzen die zu fixen sind:
-

## Product Type

Erlaubte Werte (Taxonomie):
-
-

## Variant-Optionen Konsistenz

Konsistente Schreibweisen für wiederkehrende Optionen (Farben, Größen, Materialien):
-
-

## Variant-Naming

Vorgaben:
-

## Bilder-Anzahl

Mindestanzahl pro Produkt:

## Variant-Bild-Zuordnung

Vorgaben (welche Variant-Optionen brauchen ein eigenes Bild, welche nicht):
-
