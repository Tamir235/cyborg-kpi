# /migrate

Implementiere oder prüfe Migrations-Code für Datenstruktur-Änderungen.

## Verwendung
```
/migrate weighted-dips
/migrate struktur
/migrate pistol
/migrate check
```

## /migrate check
Prüfe welche Migrationen noch ausstehen:

```
Migrations-Status:
  migrateEngine()        [✅ / 🔲] – lauftyp default 'zone2'
  migrateWeightedDips()  [✅ / 🔲] – value → kg+reps
  migrateStruktur()      [✅ / 🔲] – hang → deadHang KPI
  migratePistol()        [✅ / 🔲] – Kraft → Skills
```

## Ablauf für spezifische Migration

### Schritt 1 – Backup prüfen
```
⚠️ Migration verändert bestehende Daten!
Hast du ein aktuelles Backup? (ja/nein)
```
Nicht weitermachen bis Backup bestätigt.

### Schritt 2 – Migrations-Code zeigen
Zeige den vollständigen Migrations-Code als Diff.

### Schritt 3 – Bestätigung abwarten

### Schritt 4 – Implementieren
Migration in `migrateAll()` Funktion eintragen.
`_migrated` Flag setzen damit Migration nur einmal läuft.

### Schritt 5 – Test-Anleitung
```
Test mit Backup-Daten:
1. backups/cyborg-2026-04-28.json importieren
2. Prüfen ob alte Daten korrekt migriert wurden
3. Prüfen ob neue Einträge korrekt gespeichert werden
4. Export → Import → wieder prüfen
```

## Migrations-Regeln
```javascript
// Alle Migrationen MÜSSEN idempotent sein:
function migrateX() {
  if (S.logs.x?.[0]?._migrated) return; // bereits migriert
  // ... migration code ...
  S.logs.x = S.logs.x.map(e => ({...e, _migrated: true}));
  lsSave();
}
```
