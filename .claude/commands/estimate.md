# /estimate

Schätze den Implementierungsaufwand für einen Backlog-Item.

## Verwendung
```
/estimate P1-1
/estimate NAV-2
/estimate SK-1
```

## Ausgabe-Format

```
📏 Aufwand-Schätzung: [Backlog-ID] – [Name]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Betroffene Code-Bereiche:
  → [Funktion / Konstante / CSS] – [Art der Änderung]

Geschätzte Zeilen:  ~[N] geändert / ~[N] neu
Komplexität:        [Einfach / Mittel / Komplex]
Zeitschätzung:      ~[X] Minuten

Abhängigkeiten:
  → Vorher nötig: [IDs oder "keine"]

Risiken: [kurze Zusammenfassung oder "keine"]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Bereit für /implement? [Ja / Erst /risk ausführen]
```

## Komplexitäts-Kriterien
```
Einfach:  1 Funktion, keine Datenstruktur-Änderung, kein Migration
Mittel:   2-3 Funktionen, neue State-Felder, einfache Migration
Komplex:  Neue View, Breaking Change, komplexe Migration, Cross-System
```
