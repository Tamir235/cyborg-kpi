# /unlock-chain

Zeige die vollständige Progressionskette für einen Skill oder KPI.

## Verwendung
```
/unlock-chain hspuWall
/unlock-chain planche
/unlock-chain dragonFlag
/unlock-chain frontLever
/unlock-chain manna
```

## Ausgabe-Format

```
🔓 Unlock-Kette: [Skill-Name]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Vorstufen (müssen erfüllt sein):
  ✅ [Skill A]    – [Aktueller Wert] / [Ziel]  ERFÜLLT
  🔲 [Skill B]    – [Aktueller Wert] / [Ziel]  [X% Fortschritt]
  🔒 [Skill C]    – gesperrt bis [Skill B] erfüllt

Aktueller Status:
  [Skill-Name]: [Aktueller Wert] / [Ziel]
  Fortschritt: [X%] [████░░░░░░]
  Status: [GESPERRT / IN PROGRESS / BEREIT / ABGESCHLOSSEN]

Nächste Stufe:
  → [Nächster Skill] (freigeschaltet wenn [Bedingung])

Cross-Unlocks (diesen Skill beeinflusst):
  ← [Anderer KPI] aus Kraft/Struktur hilft hier
```

## Ablauf

### Schritt 1 – UNLOCK_RULES lesen
Lies die `UNLOCK_RULES` Konstante in index.html für den gesuchten Skill.

### Schritt 2 – Aktuellen Stand berechnen
Berechne aus `S.logs` die aktuellen Werte für alle beteiligten Skills.

### Schritt 3 – Kette visualisieren
Zeige den vollständigen Pfad von Grundvoraussetzungen bis zum Ziel-Skill.

### Schritt 4 – Empfehlung
```
Nächster Schritt zum Unlock:
  Trainiere [Skill X] – [X] [Einheit] fehlen noch
```

## Cross-Unlock Übersicht
```
V-Sit (>20s)         → Manna-Kette freigeschaltet
HBH (>30s)           → Dragon Flag freigeschaltet
Handstand (>20s)     → HSPU Wall freigeschaltet
L-Sit (>30s)         → Front Lever Progression
Muscle-up (>1 Rep)   → Back Lever Progression
```
