# /risk

Analysiere einen Backlog-Item auf Risiken bevor du implementierst.

## Verwendung
```
/risk P1-1
/risk NAV-2
/risk K-1
/risk E-4
```

## Ausgabe-Format

```
⚠️ Risiko-Analyse: [Backlog-ID] – [Name]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Datenverlust-Risiko:    [🟢 keins / 🟡 möglich / 🔴 hoch]
  → [Begründung]

Breaking Change:        [🟢 nein / 🟡 möglich / 🔴 ja]
  → [Was könnte brechen]

Migrations-Aufwand:     [🟢 keiner / 🟡 mittel / 🔴 komplex]
  → [Welche Daten sind betroffen]

Performance-Auswirkung: [🟢 keine / 🟡 minimal / 🔴 spürbar]
  → [Begründung]

Abhängigkeiten:
  → Muss vorher implementiert sein: [IDs oder "keine"]
  → Muss nachher implementiert werden: [IDs oder "keine"]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Empfehlung: [DIREKT implementieren / VOR Migration backup / ERST X dann Y]
```

## Wann /risk benutzen
- Vor allen P4 Migrations-Items (K-1, S-2, E-4, K-6)
- Vor NAV-Items die State-Felder ändern
- Vor jedem Item das `lsSave()` oder `KPIS` verändert
- Immer wenn der User unsicher ist
