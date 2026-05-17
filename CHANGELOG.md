# Changelog

Alle nennenswerten Änderungen an diesem Plugin werden hier dokumentiert.

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
