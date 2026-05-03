# /diff

Zeige alle Änderungen an index.html seit dem letzten Backup.

## Ablauf

### Schritt 1 – Letztes Backup finden
Suche die neueste Datei in `backups/` mit `.html` Endung.

### Schritt 2 – Vergleich ausgeben

```
📋 Änderungen diese Session
━━━━━━━━━━━━━━━━━━━━━━━━━━━
Vergleich: index.html ↔ backups/[letzte-html-datei]

Geänderte Bereiche:
  [Funktionsname / CSS-Klasse / Konstante]
    → [kurze Beschreibung was sich geändert hat]

Neue Funktionen:
  + [Funktionsname]

Entfernte Funktionen:
  - [Funktionsname]

Geänderte State-Felder:
  S.[feld] – [was sich geändert hat]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Gesamt: ~[N] Zeilen geändert
```

### Schritt 3 – Wenn kein HTML-Backup vorhanden
```
⚠️ Kein index.html Backup gefunden.
Nur JSON-Backups (App-Daten) gefunden.

HTML-Backup erstellen:
  cp index.html backups/index-[datum].html
```

## Verwendung
Nützlich vor `/end-session` um zu sehen was diese Session geändert hat,
und um die Commit-Message für `/git-push` vorzubereiten.
