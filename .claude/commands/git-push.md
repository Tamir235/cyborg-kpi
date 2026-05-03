# /git-push

Commit und Push nach einer Session. Automatisch sinnvolle Commit-Message generieren.

## Ablauf

### Schritt 1 – Änderungen prüfen
```bash
git status
git diff --stat
```

### Schritt 2 – Commit-Message generieren
```
Format: type(scope): beschreibung

Beispiele:
feat(nav): Quick Log Sheet mit 6 Kacheln implementiert
fix(kraft): Modal öffnet jetzt korrekte Übung aus KPI-Ansicht
docs: CLAUDE.md v2.6 – technische Architektur ergänzt
refactor(engine): Pace auto-berechnet aus Distanz + Dauer
style: Premium Dark Mode Design System umgesetzt
```

### Schritt 3 – Bestätigung
```
Commit-Message: "[generierte Message]"
Push zu: github.com/Tamir235/cyborg-kpi

Bestätigen? (ja/nein)
```

### Schritt 4 – Ausführen
```bash
git add index.html CLAUDE.md DESIGN.md SKILLS.md .claude/
git commit -m "[Message]"
git push
```

## Commit-Typen
```
feat     → neues Feature implementiert
fix      → Bug behoben
docs     → CLAUDE.md / DESIGN.md geändert
style    → Design-Änderungen, CSS
refactor → Code umstrukturiert ohne Feature-Änderung
chore    → .gitignore, settings, etc.
```

## Wichtig
- backups/ ist in .gitignore → werden NICHT gepusht
- index.html, CLAUDE.md, .claude/ → werden IMMER gepusht
- Bei sensiblen Änderungen: erst /backup-check ausführen
