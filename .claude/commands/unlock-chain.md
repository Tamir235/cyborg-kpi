# /unlock-chain

Zeige die vollständige Progressionskette für einen Skill oder KPI.

## Verwendung
```
/unlock-chain hspuWall
/unlock-chain planche
/unlock-chain dragonFlag
/unlock-chain frontLever
```

## Ausgabe-Format

```
🔓 Unlock-Kette: [Skill-Name]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Vorstufen:
  ✅ [Skill A]  – [Wert] / [Ziel]  ERFÜLLT
  🔲 [Skill B]  – [Wert] / [Ziel]  [X%]
  🔒 [Skill C]  – gesperrt bis [Skill B] erfüllt

Aktueller Status:
  Fortschritt: [X%] [████░░░░░░]
  Status: [GESPERRT / IN PROGRESS / BEREIT]

Nächste Stufe:
  → [Nächster Skill] (freigeschaltet wenn [Bedingung])

Cross-Unlocks:
  ← [Anderer KPI] aus Kraft/Struktur hilft hier
```

## Cross-Unlock Übersicht
```
V-Sit (>20s)      → Manna-Kette freigeschaltet
HBH (>30s)        → Dragon Flag freigeschaltet
Handstand (>20s)  → HSPU Wall freigeschaltet
L-Sit (>30s)      → Front Lever Progression
Muscle-up (>1)    → Back Lever Progression
```
