# /start-session

Führe diese Schritte aus wenn eine neue Session beginnt:

## 1. Alle Docs lesen
Lies diese Dateien vollständig in dieser Reihenfolge:
- `CLAUDE.md` – Vision, Backlog, Regeln
- `DESIGN.md` – Design System, Komponenten
- `SKILLS.md` – verfügbare Slash Commands
- `calisthenics-wiki.md` – verifizierte Skill-Progressionen, Cross-Unlocks, Schwellen

## 2. Code-Stand erfassen
- Öffne `index.html` und verschaffe dir einen groben Überblick
- Prüfe welche Features bereits implementiert sind
- Vergleiche mit dem Backlog in CLAUDE.md

## 3. Backup prüfen
- Prüfe ob eine Datei in `backups/` existiert
- Notiere Datum des letzten Backups

## 4. Zusammenfassung ausgeben

Gib exakt dieses Format aus:

```
╔══════════════════════════════════════╗
║   🤖 Cyborg KPI · Session Start      ║
╚══════════════════════════════════════╝

📅 Letztes Backup: [Datum oder "keines gefunden"]
📱 index.html: [grobe Einschätzung Stand]

Module Status:
  Kraft     [✅/🔲]    Engine    [✅/🔲]
  Struktur  [✅/🔲]    Peak      [✅/🔲]
  Skills    [✅/🔲]    Recovery  [✅/🔲]

Nächste Tasks:
  1. [Backlog-ID] – [Beschreibung]
  2. [Backlog-ID] – [Beschreibung]
  3. [Backlog-ID] – [Beschreibung]

⚠️ Offene Fragen: [falls vorhanden, sonst "keine"]
══════════════════════════════════════
Bereit. Was sollen wir angehen?
```

## Wichtige Erinnerungen
- Nie direkt schreiben ohne Diff + Bestätigung
- Unlock-Status NIE in State cachen
- KI immer über AIProvider – nie direkter API-Call
- Quick Log Sheet ersetzt S.modal='pick'
