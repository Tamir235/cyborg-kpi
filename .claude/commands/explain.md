# /explain

Erkläre eine Funktion oder einen Code-Bereich in einfachem Deutsch.

## Verwendung
```
/explain sysSc
/explain getRecommendation
/explain isUnlocked
/explain render
```

## Ablauf

### Schritt 1 – Code finden
Öffne index.html und finde die Funktion.

### Schritt 2 – Erklärung ausgeben

Format:
```
📖 [Funktionsname]
━━━━━━━━━━━━━━━━━━━━━━━━

Was sie macht:
[1-2 Sätze in einfachem Deutsch]

Wie sie aufgerufen wird:
[Wo im Code wird sie genutzt?]

Parameter:
  [param1] – [was das ist]
  [param2] – [was das ist]

Gibt zurück:
  [was kommt raus]

Beispiel:
  sysSc('kraft', S.logs, S.targets)
  → gibt 0.38 zurück (38% Score für Kraft)

Besonderheiten / Fallstricke:
  [falls relevant]
```

## Regel
Keine technischen Fachbegriffe ohne Erklärung.
Ziel: Auch ohne Coding-Hintergrund verstehen.
