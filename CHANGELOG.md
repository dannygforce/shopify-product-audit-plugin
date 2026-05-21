# Changelog

Alle nennenswerten Änderungen an diesem Plugin werden hier dokumentiert.

## [1.7.0] - 2026-05-21

**Hinzugefügt**
- **Verify-Fail Recovery (Phase 6):** Explizite Behandlung von Push/Manual/Normalization-Drift, inkl. Optionen bei teilweise gepushtem Batch (rollback / nur erfolgreiche behalten / abbrechen). Schließt die Lücke, dass „Verify schlägt fehl" bisher kein klar definiertes Verhalten hatte.
- **Custom-Metafield-Warnung VOR Push (Phase 5):** Wenn das Diff Custom-Metafields enthält, wird der User explizit informiert dass der CSV-Backup diese nicht abdeckt und kann entweder ein zusätzliches JSON-Backup anfordern oder das Risiko bewusst eingehen. Bisher kam die Info erst beim Rollback — zu spät.
- **Scope-Eskalations-Pfad (Auth):** Wenn ein Audit-Punkt mitten in der Session einen Scope braucht der nicht im Standard-Set ist (z.B. `read_themes`, `read_translations`), gibt's einen Hard Stop und expliziten User-Check, statt stiller Scope-Erweiterung.
- **HTML/Body Normalisierungsregeln (Phase 6 Verify):** Whitespace-Collapse zwischen Tags, Tag-Set-Vergleich, Metafield-JSON-Deep-Equal. Verhindert false positives beim Verify, die Shopify-serverseitige Sanitization sonst produziert.
- **Progressive Disclosure:** Drei neue Reference-Files (`references/field-rules.md`, `references/csv-backup-format.md`, `references/audit-rules-interview.md`) + README in `references/examples/`. SKILL.md verlinkt sie statt alles inline zu haben.

**Geändert**
- **Description (Skill-Trigger):** Tighter, englische Trigger-Varianten ergänzt („audit my products", „clean product titles", „fix metafields"), explizites NICHT-verwenden-Signal für Pricing-Bulk, Inventory-Only, Orders, Theme-Code, Translations.
- **Phase 1 mit drei klaren Einstiegspfaden:** A) Smart Setup mit konkreten Feldern, B) Discovery für Rundum-Audit, C) `audit-rules.md` schreiben (verlinkt auf das Interview-Verfahren). Bisher waren die drei Pfade in einer Sektion verschränkt.
- **Hard-MUSTs mit Begründung:** „Warum 20 pro Batch", „Warum keine Schweregrade", „Warum Phase-Struktur nicht skippable" jetzt erklärt statt nur dekretiert. Behält die Härte, gibt aber Kontext für Edge-Cases.

**Behoben**
- Phrasing „Store auf dem Claude Code gerade läuft" durch korrekte Beschreibung („Store, der via `shopify store auth` konfiguriert ist") ersetzt.
- `audit-rules-template.md` ist jetzt aus SKILL.md verlinkt, damit das Modell das vorhandene Template nutzt statt eines aus dem Gedächtnis zu schreiben.

## [1.6.0] - 2026-05-17

**Hinzugefügt**
- **Smart Setup:** Phase 1 parst jetzt zuerst die User-Message und übernimmt bereits beantwortete Fragen explizit, statt starr alle 3 Fragen sequentiell zu stellen. Macht den Einstieg deutlich smoother wenn der User schon Pattern/Quelle/Scope mitgegeben hat.
- **Undo-Flow:** Neue Sektion für Rollback. Findet das jüngste Backup-CSV im Downloads-Ordner, zeigt Diff (aktuell vs. Backup), schreibt vor dem Rollback ein Pre-Rollback-Backup (`shopify-audit-prerollback-...csv`), spielt zurück, verifiziert vollständig. Triggert auf "undo", "rückgängig", "rollback", "backup einspielen". Mit explizitem Hinweis dass Custom Metafields nicht im CSV-Export enthalten sind und manuell rollback-werden müssen.

**Geändert**
- SKILL.md von 416 auf 305 Zeilen reduziert (~27% inklusive der neuen Undo-Section; reine Bestands-Straffung ~40%). Redundante Emphasis ("NICHT VERHANDELBAR" mehrfach), doppelt formulierte Regeln zwischen Workflow und "Was du NIE tust", überlange Begründungen und doppelte Backup-Pfad-Beschreibung entfernt. Alle harten Regeln bleiben erhalten (verified per grep gegen kritische Patterns).
- Pflicht-Outputs-Block aufgelöst und in die jeweiligen Phasen integriert.

## [1.5.0] - 2026-05-17

### Launch-Readiness für die öffentliche Veröffentlichung als Lead Magnet.

**Geändert**
- README komplett neu: korrekte Installationsbefehle gegen Shopify-Doku verifiziert (`/plugin marketplace add Shopify/shopify-ai-toolkit` für Dev MCP, `shopify store auth --store ... --scopes ...` für Auth), Beispiel-Output, Datenschutz-Sektion, klare Lizenz, CTA zu haunschmid-gruber.com.
- README mit SKILL.md konsistent gemacht: kein Schweregrad mehr im Report, Verify ist vollständig (nicht „erste 3"), keine 15-Punkte-Liste mehr vorne im Funnel.
- CSV-Backup deckt jetzt den vollständigen Batch ab, nicht nur die betroffenen Produkte - damit ist auch Drift auf nicht-betroffenen Feldern rollback-fähig.
- 80%-Smell ist kein Hard Stop mehr, sondern eine Warnung in Phase 5 mit expliziter Confirm-Anforderung. Brownfield-Stores mit flächendeckenden Lücken (z.B. 100% fehlende Alt-Texte) sind jetzt legitim auditierbar.
- Wenn `audit-rules.md` fehlt: Regel wird im Chat abgefragt, nie geraten. Wenn der User keine Regel hat, wird der Audit-Punkt explizit übersprungen und im Report erwähnt.
- Phase 7 erweitert um einmaligen CTA am Gesamt-Ende der Session (nicht nach jedem Batch).
- plugin.json: Description gekürzt auf marketplace-taugliche Länge, Version-Bump.

**Entfernt**
- Veraltete Referenz auf eine „15-Punkte-Liste" im Phase-1-Block (war Relikt aus älteren Versionen).

## [1.4.3] - 2026-05-04

Letzter interner Stand vor Launch-Readiness-Pass.
