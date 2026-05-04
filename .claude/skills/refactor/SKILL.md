# /refactor

Schlage Refactoring für eine Funktion vor ohne ihr Verhalten zu ändern.

## Verwendung
```
/refactor vDash
/refactor renderModal
/refactor getEnts
```

## Ablauf

### Schritt 1 – Funktion analysieren
```
📊 Analyse: [Funktionsname]
━━━━━━━━━━━━━━━━━━━━━━━━
Zeilen:       [N]
Probleme:
  → [Problem 1]
  → [Problem 2]
```

### Schritt 2 – Vorschlag als Diff zeigen
### Schritt 3 – WARTEN auf Bestätigung
### Schritt 4 – Implementieren

## Regeln
- Kein Verhalten ändern – nur Struktur
- Keine neuen Features einbauen
- Bevorzuge Extraktion von reinen Hilfsfunktionen

## Wann refactorn?
- Funktion > 50 Zeilen → Kandidat
- Funktion > 100 Zeilen → refactorn
- Gleicher Code-Block 3× wiederholt → Extraktion
