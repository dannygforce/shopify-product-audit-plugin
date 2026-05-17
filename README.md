# Shopify Product Audit

Systematischer Audit & Cleanup deiner Shopify-Produktdaten — direkt in Claude Code, lokal, mit CSV-Backups und expliziter Bestätigung vor jeder Änderung.

**Für wen?** Shop-Owner und Agenturen im DACH-Raum, die einen sauberen Datenstand wollen — bevor sie mit SEO, Performance Marketing oder einem Theme-Relaunch starten.

---

## Was du bekommst

Ein präziser, kundentauglicher Audit-Report über deine Produktdaten — auf Deutsch, mit konkreten Befunden pro Produkt, ohne raten.

Du wählst was geprüft wird (z.B. Titel, Metafelder, Alt-Texte, SKU-Format, Variant-Konsistenz, Barcode/EAN). Der Skill liest read-only aus deinem Store, gruppiert die Findings nach struktureller Übersicht und einzelnen Produkten, und lässt dich dann **in drei sauberen Wellen** entscheiden, was gefixt wird.

Vor jeder Schreib-Operation: CSV-Backup im Shopify-Export-Format, Diff-Vorschau, explizite Bestätigung. Nach jedem Push: Verify-Check über alle geänderten Produkte.

---

## Voraussetzungen

- **Claude Code** installiert ([claude.com/claude-code](https://claude.com/claude-code))
- **Shopify Dev MCP** in Claude Code konfiguriert (Setup unten)
- **Admin-Zugriff** auf deinen Shopify-Store (oder den des Kunden)

---

## Setup in 3 Schritten

### 1. Shopify AI Toolkit installieren (enthält Shopify Dev MCP)

Direkt in Claude Code eingeben:

```
/plugin marketplace add Shopify/shopify-ai-toolkit
/plugin install shopify-plugin@shopify-ai-toolkit
```

Das installiert offizielles Shopify-Tooling inkl. Dev MCP. Voraussetzung: **Node.js 18+** ist auf dem System installiert.

Offizielle Doku: [shopify.dev/docs/apps/build/devmcp](https://shopify.dev/docs/apps/build/devmcp)

### 2. Mit deinem Store authentifizieren

```bash
shopify store auth --store deinstore.myshopify.com --scopes write_products,read_products
```

Browser öffnet sich, du loggst dich im Shopify-Admin ein, fertig. (`deinstore.myshopify.com` durch die echte myshopify-Domain deines Stores ersetzen.)

### 3. Dieses Plugin installieren

Direkt in Claude Code:

```
/plugin marketplace add dannygforce/shopify-product-audit-plugin
/plugin install shopify-product-audit@shopify-product-audit-plugin
```

Alternativ lokal aus diesem Ordner installieren:

```
/plugin marketplace add /pfad/zu/shopify-product-audit
/plugin install shopify-product-audit
```

Danach Session neu starten oder `/reload` ausführen.

---

## Loslegen

In Claude Code einfach formlos sagen was du willst:

> "Mach einen Audit der Produktdaten"
>
> "Prüf die Metafelder auf Vollständigkeit"
>
> "Cleane die Titel der Sale-Collection"
>
> "Audit für Produkt-IDs 12345, 67890"

Der Skill startet automatisch, fragt dich zuerst was geauditet werden soll, welche Quelle gelten soll und welches Zielformat — und legt dann los.

---

## So sieht der Output aus

Ein Auszug aus einem typischen Audit-Report (anonymisiert):

```markdown
## Erkanntes Title-Pattern

Mehrheit der Produkte (14 von 20) folgt dem Schema: `{Brand} {Produktname} - {Kategorie}`
Beispiel: "Acme Pullover Hoodie - Oberteile"

Abweichungen: 6 Produkte (siehe Detail-Befunde unten)

## Übersicht: SEO-Felder (Meta Title & Meta Description)

- **Meta Title** — fehlt bei 12 von 16 Produkten
- **Meta Description** — fehlt bei 13 von 16 Produkten

## Übersicht: Barcode-Format

- 13-stelliger EAN: 6 Variants
- Ungültig: Produkt 12345 (5 Stellen), Produkt 67890 (leerer String)
- Fehlt komplett: 8 Produkte

### Produkt 12345 — Acme Pullover Hoodie

- Titel weicht vom Mehrheits-Pattern ab (erwartet: "Acme {Produktname} - {Kategorie}")
- Bild 2 von 4 hat keinen Alt-Text
- Bild 3 von 4 hat keinen Alt-Text
- Barcode fehlt komplett auf Variant "Schwarz / M"
- Barcode hat ungültiges Format auf Variant "Schwarz / L" (12 Stellen, EAN braucht 13)
```

Danach gruppiert der Skill die Fixes in drei Wellen (No-brainer / Schreibweisen / Datenpflege), du bestätigst pro Welle, und der Skill schreibt zurück in den Store — mit Backup und Verify.

---

## Workflow im Detail

7 Phasen, sauber getrennt:

1. **Setup** — Was soll geprüft werden, welche Quelle, welches Zielformat
2. **Audit** (read-only) — Daten lesen, prüfen
3. **Audit-Report** — Übersichten + Pro-Produkt-Findings, ohne Schweregrad
4. **Vorgaben einsammeln** — Fixes in drei Wellen gruppieren, pro Welle Regeln klären
5. **Diff-Vorschau** — Alt vs. Neu, explizite Bestätigung
6. **Backup & Push** — CSV-Backup (Shopify-Export-Format), dann schreiben, dann vollständiges Verify
7. **Abschlussbericht** — Zusammenfassung, nächster Batch

### Sicherheits-Features

- **Read-only by default** — nichts wird ohne explizite Bestätigung geschrieben
- **Max 20 Produkte pro Run** — keine ungewollten Massen-Updates
- **CSV-Backup vor jedem Push** — kompatibel mit Matrixify, Shopify Bulk Import, Standard Admin Re-Import
- **Vollständiger Verify-Check** — jedes geänderte Produkt wird nach dem Push neu gelesen und Feld für Feld gegen den Plan abgeglichen
- **80%-Smell-Warnung** — wenn mehr als 80% des Batches geändert würden, fragt der Skill explizit nach (Brownfield-Stores haben oft 100% Alt-Text-Lücken — das ist legitim, aber du sollst es bewusst freigeben)
- **Hard Stops** bei MCP-Fehlern, Backup-Problemen, Verify-Abweichungen

---

## Datenschutz

Alles läuft lokal auf deinem Rechner.

- Produktdaten gehen nur zwischen **deinem Rechner ↔ deinem Shopify-Store** über das offizielle Shopify Dev MCP.
- Backups landen ausschließlich in **deinem lokalen Downloads-Ordner**.
- Nichts wird an Dritte gesendet, nichts wird auf fremden Servern gespeichert, nichts wird geloggt.
- Wenn du das Plugin für einen Kunden-Store nutzt, bleiben die Daten beim Kunden — du brauchst nur den Admin-Zugriff, den du ohnehin hast.

---

## Konfiguration pro Store (optional)

Für wiederkehrende Audits beim selben Kunden lohnt sich eine `audit-rules.md` mit den Store-spezifischen Regeln (Title-Pattern, SKU-Pattern, Pflicht-Metafelder, Vendor-Schreibweisen, Alt-Text-Pattern, ...).

Template kopieren:

```bash
cp ~/.claude/plugins/shopify-product-audit/skills/shopify-product-audit/references/audit-rules-template.md ./audit-rules.md
```

Das Template ist generisch und leer — du füllst nur aus was relevant ist. Im Ordner `references/examples/` findest du Beispiele für Fashion, Skincare und B2B-Tools — als Anregung, nicht als Vorgabe.

Wenn keine `audit-rules.md` da ist, fragt der Skill die fehlenden Regeln im Chat ab.

---

## Brauchst du Hilfe?

Dieses Plugin ist die Eigenleistung-Variante. Wenn du lieber:

- einen **kompletten Theme-Audit + Fix-Plan** mit PDF-Report willst,
- oder gar nicht selbst auditen, sondern **das Cleanup beauftragen** möchtest,
- oder einen **Performance- / Conversion-Audit** brauchst,

→ melde dich bei [haunschmid-gruber.com](https://haunschmid-gruber.com).

Wir bauen conversionstarke Shopify-Stores für DTC-Brands im DACH-Raum.

---

## Lizenz

Kostenlos nutzbar — auch in bezahlten Kunden-Engagements. Keine Gewähr für Schäden oder Datenverluste; mach immer ein manuelles Shopify-Backup zusätzlich zum automatischen CSV-Export, bevor du Änderungen schreibst.

---

## Author

Daniel Gruber — [haunschmid-gruber.com](https://haunschmid-gruber.com)
