# /git-push

Commit und Push nach einer Session. Automatisch sinnvolle Commit-Message generieren.

## Ablauf

### Schritt 1 – Änderungen prüfen
Führe aus:
```bash
git status
git diff --stat
```
Zeige was geändert wurde.

### Schritt 2 – Commit-Message generieren
Basierend auf den Änderungen eine sinnvolle Message:

```
Format: type(scope): beschreibung

Beispiele:
feat(nav): Quick Log Sheet mit 6 Kacheln implementiert
fix(kraft): Modal öffnet jetzt korrekte Übung aus KPI-Ansicht
docs: CLAUDE.md v2.5 – Fokus persönliches Tool
refactor(engine): Pace auto-berechnet aus Distanz + Dauer
style: Premium Dark Mode Design System umgesetzt
```

### Schritt 3 – Bestätigung
```
Commit-Message: "[generierte Message]"
Push zu: github.com/[repo]

Bestätigen? (ja/nein)
```

### Schritt 4 – Ausführen
```bash
git add .
git commit -m "[Message]"
git push
```

### Schritt 5 – Bestätigung
```
✅ Gepusht: [commit hash]
📦 GitHub: github.com/[repo]/commits
```

## Commit-Typen
```
feat     → neues Feature implementiert
fix      → Bug behoben
docs     → CLAUDE.md / ARCHITECTURE.md / DESIGN.md geändert
style    → Design-Änderungen, CSS
refactor → Code umstrukturiert ohne Feature-Änderung
test     → Tests hinzugefügt
chore    → .gitignore, settings, etc.
```

## Scopes (Bereiche)
```
kraft / engine / peak / skills / struktur / recovery
nav / analyse / profil / dashboard
ki / dna / challenge / badges
docs / design / config
```

## Wichtig
- Backups/ ist in .gitignore → werden NICHT gepusht
- index.html, CLAUDE.md, .claude/ → werden IMMER gepusht
- Bei sensiblen Änderungen: erst /backup-check ausführen
