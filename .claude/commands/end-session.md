# /end-session

Führe diese Schritte aus am Ende jeder Session:

## Schritt 1 – CLAUDE.md aktualisieren
- Erledigte Items als `[x]` markieren
- Neue Items hinzufügen
- Versionshistorie ergänzen
- Module-Status aktualisieren

## Schritt 2 – DESIGN.md aktualisieren
Nur wenn Design-Entscheidungen getroffen wurden.

## Schritt 3 – Git Push
Führe `/git-push` aus.

## Schritt 4 – Zusammenfassung

```
╔══════════════════════════════════════╗
║   ✅ Cyborg KPI · Session Ende        ║
╚══════════════════════════════════════╝

Erledigt:
  ✓ [Item 1]
  ✓ [Item 2]

Neu im Backlog:
  + [falls entstanden, sonst "keine"]

Docs:
  CLAUDE.md       ✅
  DESIGN.md       [✅ / ⏭ nicht nötig]

GitHub:
  ✅ Gepusht: [commit message]

══════════════════════════════════════
⚠️  BACKUP REMINDER (Nutzerdaten):
  App öffnen → Avatar → Daten → JSON Export
  → In backups/ speichern (nicht in GitHub!)
```

## Wichtig
- GitHub Push = Code-Backup (index.html, Docs, Commands)
- App-Daten-Backup = separat via JSON Export in App
- Beides ist nötig – sie sichern verschiedene Dinge
