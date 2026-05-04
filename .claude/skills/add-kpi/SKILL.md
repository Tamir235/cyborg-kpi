# /add-kpi

Füge einen neuen KPI zu einem System hinzu.

## Verwendung
```
/add-kpi kraft australianRows
/add-kpi engine kadenz
/add-kpi struktur mobility
```

## Ablauf

### Schritt 1 – KPI-Definition vorbereiten
```javascript
{ k: 'australianRows', label: 'Australian Rows', unit: 'Reps', target: 15, hb: 1 }
```
- `k`: camelCase Key (eindeutig im System)
- `label`: Anzeigename
- `unit`: Einheit (Reps, kg, s, min/km, bpm, /10, W, %)
- `target`: Zielwert (optional)
- `hb`: 1 = höher ist besser, 0 = niedriger ist besser

### Schritt 2 – Position fragen
```
Wo soll [KPI] in der Liste erscheinen?
Aktuell: [bestehende KPIs in Reihenfolge]
Vorschlag: nach [KPI X]
```

### Schritt 3 – Formular prüfen
Braucht fKraft/fEngine/etc. neue Felder?
Braucht `getEnts()` eine Anpassung?

### Schritt 4 – Diff zeigen, Bestätigung abwarten

### Schritt 5 – Implementieren
- KPI in `KPIS.[system]` Array eintragen
- Formular anpassen falls nötig
- INFO-Eintrag hinzufügen wenn Erklärung nötig

## Wichtige Regeln
- `k` darf nicht mit bestehendem Key kollidieren
- `hb` korrekt setzen – falsch = PR-Erkennung invertiert
- Neue KPIs brauchen keine Migration (leere History ist OK)
