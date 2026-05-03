# /diff

Zeige alle Änderungen an index.html seit dem letzten Backup.

## Ablauf

### Schritt 1 – Vergleich via git
```bash
git diff HEAD index.html
```
Oder gegen letzten Commit:
```bash
git show HEAD:index.html > /tmp/prev.html && diff /tmp/prev.html index.html
```

### Schritt 2 – Übersicht ausgeben

```
📋 Änderungen diese Session
━━━━━━━━━━━━━━━━━━━━━━━━━━━
Geänderte Bereiche:
  [Funktionsname / CSS-Klasse / Konstante]
    → [kurze Beschreibung was sich geändert hat]

Neue Funktionen:
  + [Funktionsname]

Geänderte State-Felder:
  S.[feld] – [was sich geändert hat]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Gesamt: ~[N] Zeilen geändert
```

## Verwendung
Nützlich vor `/end-session` um zu sehen was diese Session geändert hat,
und um die Commit-Message für `/git-push` vorzubereiten.
