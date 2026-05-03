# /test

Generiere eine spezifische Test-Checkliste für einen Bereich.

## Verwendung
```
/test P1-1
/test navigation
/test migration
/test skills
/test all
```

## Standard-Tests (immer)
```
□ Dark Mode korrekt (alle Farben, keine weißen Flecken)
□ Light Mode korrekt
□ Neuer Eintrag speichert (DevTools → Application → localStorage)
□ Reload lädt Daten korrekt (alle Einträge noch da)
□ Export JSON funktioniert (Datei öffenbar, Daten korrekt)
□ Import eigenes JSON (exportieren → importieren → identisch)
```

## /test navigation
```
□ Home-Screen lädt korrekt
□ Quick Log Sheet öffnet mit + Button
□ Alle 6 Kacheln sichtbar und antippbar
□ Kachel-Tap öffnet direkt Formular (kein Zwischen-Modal)
□ Avatar oben rechts → Profil-Screen
□ Profil-Screen zeigt Badges + PRs
□ Nach Training-Log: Recovery Sheet erscheint nach 500ms
□ Recovery Sheet: auto-dismiss nach 10s
□ Weekly Challenge auf Dashboard sichtbar
□ Weekly Challenge auf Analyse (erste Card) sichtbar
□ Back-Navigation funktioniert korrekt
```

## /test skills
```
□ Skills-Hauptansicht: Auto-Fokus zeigt richtigen Skill
□ Gruppe antippen → Skill Tree öffnet
□ Done-Nodes: lila ✓
□ Next-Nodes: orange →
□ Locked-Nodes: ausgegraut 🔒
□ Milestone-Banner erscheint bei >80%
□ Cross-Unlock: V-Sit tracken → Manna-Kette freigeschaltet?
□ Cross-Unlock: HBH >30s → Dragon Flag freigeschaltet?
□ DNA-Card zeigt korrekte Blocker
□ DNA-Card: grün wenn Blocker erfüllt
```

## /test migration
```
□ Backup laden: backups/cyborg-2026-04-28.json importieren
□ migrateEngine(): lauftyp 'zone2' bei altem Eintrag
□ migrateWeightedDips(): reps:8, kg:5 aus altem Eintrag
□ migrateStruktur(): hang-Werte als deadHang KPI
□ migratePistol(): Pistol-Einträge in Skills
□ Alte Einträge noch alle vorhanden
□ Neue Einträge speichern korrekt
□ Export nach Migration → Import → identisch
□ Migration läuft kein zweites Mal (_migrated Flag)
```

## /test all
Führt alle obigen Checklisten nacheinander aus.
