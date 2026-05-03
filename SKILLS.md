# SKILLS.md – Cyborg KPI
> Custom Slash Commands & Workflows für Claude Code Sessions
> Stand: Mai 2026 | Version: 1.0

---

## Übersicht

Diese Datei definiert alle verfügbaren Slash Commands für Claude Code.
Bei Session-Start werden alle Commands aus dieser Datei automatisch geladen.

---

## Session Commands

### `/start-session`
**Zweck:** Neue Session initialisieren, Kontext aufbauen

```
Schritte:
1. CLAUDE.md vollständig lesen
2. ARCHITECTURE.md vollständig lesen
3. DESIGN.md vollständig lesen
4. SKILLS.md vollständig lesen
5. index.html überfliegen (Struktur, nicht jede Zeile)
6. Letztes Backup in /backups/ prüfen (Datum + Größe)
7. Zusammenfassung ausgeben
```

**Ausgabe:**
```
╔══════════════════════════════════╗
║   🤖 Cyborg KPI – Session Start  ║
╚══════════════════════════════════╝
📅 index.html zuletzt geändert: [Datum]
💾 Letztes Backup: [Datum] · [Einträge] Einträge

Module Status:
  Kraft     ✅  Engine    🔲
  Struktur  ✅  Peak      🔲
  Skills    🔲  Recovery  🔲

Nächste Tasks:
  1. [Backlog-ID] – [Beschreibung]
  2. [Backlog-ID] – [Beschreibung]
  3. [Backlog-ID] – [Beschreibung]

⚠️  Offene Fragen: [falls vorhanden, sonst "keine"]
══════════════════════════════════
Bereit. Was sollen wir angehen?
```

---

### `/end-session`
**Zweck:** Session sauber abschließen, alle Docs aktualisieren

```
Schritte:
1. CLAUDE.md aktualisieren:
   - Erledigte Items → [x]
   - Neue Items ergänzen
   - Module-Status aktualisieren
   - Versionshistorie ergänzen
2. ARCHITECTURE.md aktualisieren (falls Datenstrukturen geändert)
3. DESIGN.md aktualisieren (falls UI-Entscheidungen getroffen)
4. Zusammenfassung ausgeben
```

**Ausgabe:**
```
╔══════════════════════════════════╗
║  ✅ Cyborg KPI – Session Ende    ║
╚══════════════════════════════════╝
Erledigt diese Session:
  ✓ [Item 1]
  ✓ [Item 2]

Neu im Backlog:
  + [Neues Item falls entstanden]

Docs aktualisiert:
  CLAUDE.md      ✅
  ARCHITECTURE.md [✅ / ⏭ nicht nötig]
  DESIGN.md      [✅ / ⏭ nicht nötig]

══════════════════════════════════
⚠️  BACKUP REMINDER:
  1. index.html kopieren → /backups/index-[datum].html
  2. App öffnen → Daten → JSON exportieren → /backups/
```

---

### `/status`
**Zweck:** Schneller Überblick ohne Dateien zu öffnen

**Ausgabe:** Kompakte Tabelle aller Backlog-Items mit Status + welches Modul gerade aktiv ist.

---

### `/implement [id]`
**Zweck:** Einen Backlog-Item sicher implementieren

**Beispiel:** `/implement P1-1`

```
Schritte:
1. Backlog-Item aus CLAUDE.md lesen und zusammenfassen
2. Relevante Code-Stelle in index.html finden
3. Geplante Änderung als Diff anzeigen:
   - Alte Zeilen mit - markieren
   - Neue Zeilen mit + markieren
4. WARTEN auf Bestätigung ("ja" / "ok" / "mach es")
5. Änderung schreiben
6. Kurze Erklärung was geändert wurde
7. Testing-Hinweis ausgeben
```

**Wichtig:** Niemals direkt schreiben ohne Bestätigung. Immer Diff zeigen.

---

### `/review [modul]`
**Zweck:** Strukturierten Modul-Review durchführen

**Beispiel:** `/review skills`

```
Schritte:
1. Aktuelle KPI-Definition aus index.html zeigen
2. Einträge aus letztem Backup zeigen (Datum, Werte, Häufigkeit)
3. Standard-Fragen stellen:
   a) Welche KPIs sind aktiv / nie genutzt?
   b) Fehlen KPIs die zum Cyborg-Profil passen?
   c) Sind Units und Targets sinnvoll?
   d) Macht eine Progressions-Kette Sinn?
   e) Braucht das Formular mehr/weniger Felder?
4. Ergebnisse für CLAUDE.md Backlog vorbereiten
```

---

### `/diff`
**Zweck:** Alle Änderungen dieser Session an index.html anzeigen

Zeigt eine übersichtliche Liste aller modifizierten Funktionen/Bereiche.

---

### `/backup-check`
**Zweck:** Backup-Status prüfen

```
Prüft:
- Datum des neuesten Backups in /backups/
- Geschätzte Anzahl neuer Einträge seit letztem Backup
- Empfehlung: Backup nötig? Ja/Nein
```

---

### `/migrate-check`
**Zweck:** Prüfen ob Migrations-Code nötig ist

```
Prüft:
- Gibt es Backlog-Items mit Datenstruktur-Änderungen?
- Sind bestehende localStorage-Daten davon betroffen?
- Migrations-Strategie vorschlagen
```

---

### `/test [bereich]`
**Zweck:** Testing-Checkliste für einen bestimmten Bereich ausgeben

**Beispiele:**
- `/test kraft` → Kraft-spezifische Tests
- `/test migration` → Migrations-Tests
- `/test all` → Komplette Checkliste

```
Standard-Tests (immer):
□ Dark Mode korrekt
□ Light Mode korrekt
□ Neuer Eintrag speichert (DevTools → Application → localStorage)
□ Reload lädt Daten korrekt
□ Export JSON funktioniert
□ Import eigenes JSON funktioniert

Migrations-Tests:
□ Backup laden → Migration triggert
□ Alle alten Einträge vorhanden
□ Neue Struktur korrekt
□ Kein Datenverlust

Progressions-Tests:
□ Unlock berechnet sich korrekt aus Logs
□ Banner erscheint bei 80%-Schwelle
□ Unlock-Animation spielt ab
□ Gesperrte KPIs nicht antippbar
```

---

### `/explain [funktion]`
**Zweck:** Eine Funktion aus index.html erklären

**Beispiel:** `/explain sysSc`

Gibt eine klare Erklärung in einfachem Deutsch aus – kein Code-Kauderwelsch.

---

### `/add-kpi [system] [name]`
**Zweck:** Neuen KPI zu einem System hinzufügen

**Beispiel:** `/add-kpi kraft australianRows`

```
Schritte:
1. KPI-Definition vorbereiten (k, label, unit, target, hb)
2. In KPIS-Objekt einordnen (Position fragen)
3. Prüfen ob Formular-Änderung nötig
4. Prüfen ob getEnts() Anpassung nötig
5. Diff zeigen → Bestätigung → Implementieren
```

---

### `/unlock-chain [kpi]`
**Zweck:** Progressionskette für einen KPI anzeigen

**Beispiel:** `/unlock-chain hspuWall`

Zeigt: Vorstufen → aktueller Status → nächste Stufe → Unlock-Bedingung

---

## Vorgeschlagene weitere Commands

Diese Commands sind noch nicht implementiert aber empfohlen:

### `/changelog`
Zeigt alle Änderungen aller bisherigen Sessions chronologisch.
Quelle: Versionshistorie aus CLAUDE.md + ARCHITECTURE.md

### `/risk [id]`
Analysiert einen Backlog-Item auf Risiken:
- Datenverlust-Risiko?
- Performance-Auswirkung?
- Breaking Change?
- Migrations-Aufwand?

### `/estimate [id]`
Schätzt Implementierungsaufwand für einen Backlog-Item:
- Anzahl betroffene Code-Zeilen
- Komplexität (einfach/mittel/komplex)
- Abhängigkeiten zu anderen Items

### `/snapshot`
Erstellt einen "Stand jetzt"-Kommentar im Code:
```javascript
// SNAPSHOT [Datum] – [X] Einträge, Score [Y]%, Module: Kraft✅ Skills🔲
```

### `/debug [symptom]`
Hilft bei der Fehlersuche:
**Beispiel:** `/debug "Modal zeigt falsche Übung"`
Analysiert den Code systematisch und schlägt Fix vor.

### `/design [bereich]`
Zeigt Design-Entscheidungen aus DESIGN.md für einen Bereich.
**Beispiel:** `/design unlock` → zeigt B+E Spezifikation

### `/refactor [funktion]`
Schlägt Refactoring für eine Funktion vor ohne Verhalten zu ändern.
Nützlich wenn Funktionen zu groß werden (> 50 Zeilen).

---

## Command-Chaining

Commands können kombiniert werden:

```
/start-session → /review skills → /implement SK-1 → /end-session
```

Claude Code führt sie der Reihe nach aus.

---

## Hinweise für Claude Code

- **Immer** `/start-session` am Anfang ausführen wenn der Nutzer es vergisst
- **Immer** an `/end-session` erinnern wenn die Session > 30 Minuten läuft
- Bei jedem `/implement` den Diff zeigen und **warten** – nie direkt schreiben
- Bei Unsicherheit über eine Entscheidung → `/risk` zuerst
- CLAUDE.md ist die **einzige Quelle der Wahrheit** – bei Widersprüchen mit dem Code gewinnt CLAUDE.md

---

## Versionshistorie

| Version | Datum | Änderung |
|---|---|---|
| 1.0 | Mai 2026 | Initiale Commands + Vorschläge |
