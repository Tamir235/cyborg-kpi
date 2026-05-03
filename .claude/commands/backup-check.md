# /backup-check

Prüfe ob ein Backup nötig ist und erinnere daran.

## Ablauf

### Schritt 1 – Backup-Status prüfen
- Suche nach Dateien in `backups/`
- Prüfe das Datum der neuesten Datei
- Berechne wie viele Tage seit letztem Backup

### Schritt 2 – Empfehlung ausgeben

```
💾 Backup Status
━━━━━━━━━━━━━━━━━━━━━━━━
Letztes Backup: [Datum oder "keines gefunden"]
Tage vergangen: [X]

Status: [✅ Aktuell / ⚠️ Veraltet / 🔴 Kein Backup!]
```

### Schritt 3 – Bei Bedarf anleiten
Wenn Backup nötig:
```
So machst du ein Backup:
1. In der App:
   Home → Avatar → Daten → JSON exportieren
   → In backups/ speichern

2. Fertig ✓
```

## Wann ist ein Backup nötig?
- Mehr als 3 Tage seit letztem Backup
- Vor größeren Änderungen (Navigation, Module)
- Nach einer produktiven Session mit vielen Änderungen
- Immer vor Migrations-Code ausführen
