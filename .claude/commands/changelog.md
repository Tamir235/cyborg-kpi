# /changelog

Zeige alle Änderungen aller bisherigen Sessions chronologisch.

## Ablauf

### Schritt 1 – Quellen lesen
- Versionshistorie aus CLAUDE.md
- Versionshistorie aus DESIGN.md
- Commits aus git log (falls Git eingerichtet)

### Schritt 2 – Chronologische Übersicht ausgeben

```
📜 Cyborg KPI · Changelog
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[Datum] · v[Version]
  ✓ [Änderung 1]
  ✓ [Änderung 2]

[Datum] · v[Version]
  ✓ [Änderung 1]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Gesamt: [N] Sessions · [N] Features · [N] Fixes
```

### Schritt 3 – Offene Items
```
Noch offen:
  🔴 [N] P1-Items (Safety)
  🟡 [N] P2-Items (Core UX)
  🟠 [N] P3-Items (Navigation)
```

## Tipp
Kombiniere mit `/status` für einen vollständigen Überblick:
```
/changelog   → Was war
/status      → Was ist
/implement   → Was wird
```
