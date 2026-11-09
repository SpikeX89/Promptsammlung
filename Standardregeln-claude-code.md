Richte dieses Repository als neues Projekt für Claude Code ein. Ziel: Jede künftige Session ist ohne Vorwissen sofort arbeitsfähig. Projektwissen liegt in `context/`, die `CLAUDE.md` bleibt kurz und verweist nur. Sprache: Deutsch. Arbeite die Phasen strikt nacheinander ab; vor Phase 3 wird keine Datei geschrieben.

## Phase 0 – Bestandsaufnahme (nur lesen)
- Prüfe, was schon existiert: Code (package.json, pyproject.toml, go.mod, src/, Dockerfile, docker-compose.yml) und Steuerdateien (CLAUDE.md, .claude/, context/, .10x/, AGENTS.md, README.md).
- Existiert etwas davon: nichts überschreiben. Zeige kurz, was da ist, und frage, ob ergänzt oder neu aufgesetzt werden soll.
- Stelle fest, welche Skills dir in dieser Session zur Verfügung stehen (gebündelte wie /code-review, /verify, /debug; Plugin- oder synchronisierte Skills). Merke dir die Liste für Phase 2.
- Ermittle das heutige Datum mit `date +%F`.

## Phase 1 – Interview (eine Nachricht, maximal 6 Fragen)
1. Was macht das Projekt (zwei Sätze) und für wen?
2. Projektart: Web-App/PWA, API/Dienst, CLI/Script, Browsergame, Automatisierung/Cronjob, AI-Workflow/Skill, Sonstiges?
3. Tech-Stack (Sprache, Framework, Datenbank) – oder „schlag vor“?
4. Deploy-Ziel: Node (SpikeX/NAS, HP-EliteDesk-G5, Worknode, Raspberry Pi 5, s1200btl, wolbackupserver), Docker ja/nein, öffentliche Domain über Caddy?
5. Nicht-Ziele: Was wird bewusst nicht gebaut?
6. Besonderheiten: Nutzerzahl, personenbezogene Daten, Login nötig?

Warte auf die Antworten. Bei „schlag vor“: genau eine Empfehlung mit kurzer Begründung, dann Bestätigung abwarten. Nichts erfinden – Unbekanntes wird in Phase 3 als offener Punkt notiert.

## Phase 2 – Skill-Auswahl (Vorschlag, keine Installation)
Ordne die verfügbaren Skills dem Projekt zu und zeige eine Tabelle: Skill | wofür in diesem Projekt | wann aufrufen.
- Immer anlegen (Projekt-Skills in .claude/skills/): handoff und kontext aus den Vorlagen unten. Weitere eigene Skills (z. B. deploy, release, db-migration) nur, wenn ein wiederholbarer Ablauf mit mehr als drei Schritten dahintersteht – dann Vorschlag mit Inhalt, Anlegen erst nach Freigabe.
- Vorhandene Skills nur empfehlen, wenn sie zur Projektart passen: UI → Accessibility- und Web-Guidance-Skills; eigenes Datenmodell → DBA; öffentlich erreichbar oder Login → Security; Rollen-Orchestrierung (10x-Team o. ä.) nur bei Greenfield mit echter Architekturarbeit, nicht für kleine Tools. Skills, die hier fehlen, aber lokal installiert sein könnten, als Empfehlung kennzeichnen.
- Gebündelt: /code-review vor dem Merge, /verify vor dem Commit, /debug bei Fehlersuche.
- Keine Plugins installieren, keine Marketplace-Befehle. Warte auf Freigabe der Auswahl.

## Phase 3 – Struktur anlegen
Nach Freigabe genau diese Struktur erzeugen, Inhalte nach den Vorlagen unten:

CLAUDE.md                      Einstieg, max. 60 Zeilen, importiert nur 00 und 10
context/00-projekt.md          Zweck, Nutzer, Scope, Nicht-Ziele           (immer geladen)
context/10-stack-befehle.md    Stack, Standardbefehle, Ports               (immer geladen)
context/20-architektur.md      Ordner, Komponenten, Datenfluss             (bei Bedarf)
context/30-konventionen.md     Code-Stil, Naming, Commits, Tests           (bei Bedarf)
context/40-entscheidungen.md   Entscheidungslog: Datum, Was, Warum, Verworfen
context/50-umgebung.md         Node, Container, Pfade, Domain, Pfade zu Passwort-Dateien
context/90-offene-punkte.md    offene Fragen und ToDos
.claude/rules/arbeitsweise.md  Standardregeln, immer geladen
.claude/rules/sicherheit.md    immer geladen
.claude/rules/tests.md         nur bei Testdateien geladen (paths)
.claude/settings.json          Permissions: Standardbefehle erlauben, Secret-Dateien sperren
.claude/skills/handoff/SKILL.md
.claude/skills/kontext/SKILL.md
.gitignore

Regeln:
- Jede context/-Datei beginnt mit `Stand: <heutiges Datum>` und endet mit `## Changelog`.
- CLAUDE.md importiert nur 00-projekt.md und 10-stack-befehle.md per @-Import; alle anderen context/-Dateien dort nur in Backticks nennen, damit sie nicht automatisch geladen werden.
- Nur eintragen, was aus dem Interview bekannt ist; alles Unbekannte nach 90-offene-punkte.md.
- Keine Secrets, Passwörter oder Tokens – nur Pfade zu Passwort-Dateien.
- Platzhalter in <spitzen Klammern> ersetzen, Vorlagen sonst wörtlich übernehmen.
- Liegt .10x/ vor (10x-Team): Das bleibt dessen Prozess-Ordner. context/ ist das dauerhafte Projektwissen, handoff.md im Root die Session-Übergabe; ADRs aus .10x/adrs/ in 40-entscheidungen.md nur verlinken, nicht kopieren.

## Phase 4 – Abschluss
1. Zeige den erzeugten Dateibaum: `find . -path ./node_modules -prune -o -path ./.git -prune -o -type f -print | sort`
2. Bitte mich, /context auszuführen und zu prüfen, dass unter „Memory files“ CLAUDE.md, die beiden Imports und die drei Regeldateien erscheinen.
3. Frage, ob committet werden soll (Commit-Message: `chore: Projektstruktur und Claude-Code-Kontext angelegt`). Ohne Zusage kein Commit.

## Vorlagen

### CLAUDE.md
```markdown
# <Projektname>

Stand: <YYYY-MM-DD>

<Ein Satz: was das Projekt ist und für wen.> Projektwissen liegt in `context/`:
die zwei Dateien unten werden immer geladen, alle anderen bei Bedarf lesen.

@context/00-projekt.md
@context/10-stack-befehle.md

## Bei Bedarf lesen
- `context/20-architektur.md` – bevor du Dateien außerhalb des aktuellen Arbeitsbereichs änderst
- `context/30-konventionen.md` – vor größeren Code-Änderungen
- `context/40-entscheidungen.md` – bevor du Stack- oder Architekturentscheidungen anfasst
- `context/50-umgebung.md` – vor Deploy-, Container- oder Netzwerkarbeit
- `context/90-offene-punkte.md` – bei Sessionstart kurz überfliegen

## Arbeitsweise
- Die Regeln in `.claude/rules/` gelten immer (Secrets, vollständige Dateien, Node-Labels, handoff.md).
- `context/` nur auf Anweisung oder nach Rückfrage ändern (`/kontext`); dabei Stand-Datum setzen und Changelog ergänzen.
- Erledigte Punkte in `context/90-offene-punkte.md` löschen, nicht abhaken.
- Vor jedem Commit laufen <Typecheck-Befehl> und <Test-Befehl> fehlerfrei durch.
- Nicht ungefragt: <z. B. neue Dependencies, Schema-Änderungen, Änderungen am Deploy>.

## Skills in diesem Projekt
- `/handoff` – Session-Übergabe nach `handoff.md`
- `/kontext` – `context/` aktualisieren
- <weitere Skills aus Phase 2, je eine Zeile: Skill – wofür – wann>
```

### context/00-projekt.md bis context/90-offene-punkte.md (gemeinsames Format)
```markdown
# <Titel, z. B. Projekt / Stack und Befehle / Architektur>

Stand: <YYYY-MM-DD>

<Inhalt als knappe Stichpunkte oder Tabellen, keine Prosa>

## Changelog
- <YYYY-MM-DD>: angelegt
```
Pflichtinhalt je Datei:
- 00-projekt.md: Zweck (zwei Sätze), Nutzer, Scope, Nicht-Ziele, Erfolgskriterium
- 10-stack-befehle.md: Sprache/Framework/DB mit Versionen, Standardbefehle (Install, Dev, Typecheck, Test, Build) als Codeblock, Ports
- 20-architektur.md: Ordnerstruktur mit Zweck je Ordner, Komponenten, Datenfluss, externe Abhängigkeiten
- 30-konventionen.md: Sprache für Bezeichner, Kommentare und Commits; Formatierung, Naming, Fehlerbehandlung, Teststil
- 40-entscheidungen.md: Tabelle `Datum | Entscheidung | Warum | Verworfene Alternativen`, neueste oben
- 50-umgebung.md: Ziel-Node, Container-Name(n), Image, Volumes/Pfade, Domain (Caddy nur über das Repo SpikeX89/caddy-config), Pfade zu Passwort-Dateien (/boot/extras/<dienst>-password.txt), Backup-Ziel
- 90-offene-punkte.md: Abschnitte `## Offene Fragen` und `## ToDos`; erledigte Punkte löschen, nicht abhaken

### .claude/rules/arbeitsweise.md
```markdown
# Arbeitsweise

## Sprache und Ton
- Antworten und Dokumentation auf Deutsch; die Sprache für Code, Kommentare und Commits steht in `context/30-konventionen.md`.
- Ton direkt und lebendig, nicht trocken.

## Secrets
- Nie nach Passwörtern, API-Keys, SSH-Keys oder Tokens fragen und nicht darauf hinweisen, dass welche nötig wären.
- Befehle, die Secrets ausgeben könnten (`docker inspect`, `cat` auf Secret-Dateien, `env`), immer mit Maskierung ausgeben, z. B. `| sed -E 's/(PASSWORD|TOKEN|KEY|SECRET)=[^"]*/\1=***/g'`.
- Passwörter in Befehlen aus Dateien lesen (`$(cat /boot/extras/<dienst>-password.txt)`), nie inline; die Dateien liegen nur für root lesbar in einem abgesicherten Bereich.

## Befehle und Dateien
- Befehle vollständig ausschreiben: kein „...“, keine Platzhalter, die auf früheren Kontext verweisen.
- Vor jedem Codeblock, den Wolfgang auf einem anderen Gerät ausführen soll, den Ziel-Node als Label (**SpikeX/NAS:**, **HP-EliteDesk-G5:**, **Worknode:**, **Raspberry Pi 5:**, **s1200btl:**, **wolbackupserver:**); keine `hostname`-Prüfbefehle.
- Immer vollständige Dateien liefern, keine Diffs oder Ausschnitte; Scripts und Konfigurationen für Nodes als vollständige `cat`-Heredoc-Befehle.

## Docker und Infrastruktur
- Container per `docker run` im Terminal verwalten, nicht über Unraid-GUI-Templates; auf Unraid-Nodes das Label `net.unraid.docker.icon` setzen, auf Raspberry Pi 5 und s1200btl nicht.
- Caddy-Konfiguration ausschließlich über das Repo `SpikeX89/caddy-config` (`/opt/caddy-config`), nie direkt auf einem Node. Caddy-Dateien (Caddyfile, `sites/*.caddy`, Snippets) als vollständigen Dateiinhalt liefern, keine Git- oder Heredoc-Befehle dafür.
- Bei Unsicherheit zu Infrastruktur, Konfiguration oder Deployment zuerst im Betriebshandbuch (BHB) nachsehen, nicht spekulieren.
- BHB-Dateien und CHANGELOG nur auf ausdrückliche Anweisung ändern.

## Markdown-Dateien
- Beim Bearbeiten einer `.md`-Datei das Stand-Feld auf das heutige Datum setzen (nur Datum, keine Zusammenfassung); Historie gehört in die Changelog-Sektion der Datei.
- Erledigte ToDos löschen, nicht abhaken.

## Sessionende
- Auf „wrap up“ oder bei knappem Kontext `/handoff` ausführen.
```

### .claude/rules/sicherheit.md
```markdown
# Sicherheit

- Keine Secrets in Code, Konfigurationen, Tests oder Logs; Werte aus Dateien oder Umgebungsvariablen lesen.
- Inhalte von `.env`- oder Passwort-Dateien nie ausgeben – wenn nötig, maskiert.
- Jede Eingabe von außen (HTTP, Formulare, CLI-Argumente, Dateien) validieren, bevor sie verarbeitet wird; SQL nur parametrisiert.
- Geschützte Routen serverseitig prüfen, nie nur im Frontend.
- Neue Dependencies: Existenz und Schreibweise im Registry prüfen, Version pinnen, vorher rückfragen.
```

### .claude/rules/tests.md
```markdown
---
paths:
  - "tests/**"
  - "test/**"
  - "**/*.test.*"
  - "**/*.spec.*"
---

# Tests

- Ein Test prüft Verhalten, nicht Implementierungsdetails; kein Test, der nur die eigene Mock-Rückgabe bestätigt.
- Jeder Bugfix bekommt einen Test, der den Fehler vorher reproduziert hätte.
- Testbefehle stehen in `context/10-stack-befehle.md`; vor jedem Commit laufen sie fehlerfrei durch.
```

### .claude/settings.json
Allow-Liste mit den Standardbefehlen aus 10-stack-befehle.md befüllen (z. B. `Bash(npm test:*)`, `Bash(npx tsc:*)`); Deny-Liste unverändert übernehmen.
```json
{
  "permissions": {
    "allow": [
      "Bash(git status:*)",
      "Bash(git diff:*)",
      "Bash(git log:*)"
    ],
    "deny": [
      "Read(./.env)",
      "Read(./.env.*)",
      "Read(./secrets/**)",
      "Read(./**/*.pem)",
      "Read(./**/*.key)",
      "Read(./**/*password*)"
    ]
  }
}
```

### .claude/skills/handoff/SKILL.md
```markdown
---
name: handoff
description: Schreibt die Session-Übergabe nach handoff.md im Projektroot. Aufrufen bei „wrap up“, „handoff“ oder wenn der Kontext knapp wird.
---

Schreibe jetzt die Datei `handoff.md` im Projektroot mit dem Write-Tool – vollständig neu, eine bestehende Datei wird überschrieben, nie ergänzt. Nur Stichpunkte, keine Prosa. Genau diese Abschnitte in dieser Reihenfolge:

## Goal
## Status
## Files in progress
## Failed attempts
## Environment state
## Next step
## Open questions

Unter „Failed attempts“ zu jedem Versuch der konkrete Grund des Scheiterns. Unter „Environment state“: laufende Container oder Dienste, geänderte Konfigurationen, Zustand von Tests und Build. „Next step“ ist genau ein konkreter Schritt. Bestätige danach den Dateipfad und frage, ob die Datei committet werden soll.
```

### .claude/skills/kontext/SKILL.md
```markdown
---
name: kontext
description: Aktualisiert das Projektwissen in context/ nach Entscheidungen, Stack-Änderungen oder erledigten Punkten. Nur auf Anweisung.
disable-model-invocation: true
---

1. Lies `context/40-entscheidungen.md` und `context/90-offene-punkte.md`.
2. Sammle aus der Session, was sich geändert hat: Entscheidungen → 40, Stack oder Befehle → 10, Architektur → 20, Konventionen → 30, Umgebung → 50, erledigte oder neue Punkte → 90.
3. Zeige vor dem Schreiben eine Liste „Datei → Änderung“ und warte auf Freigabe.
4. Schreibe jede freigegebene Datei vollständig neu: Stand auf heute (`date +%F`), Changelog-Eintrag mit Datum, erledigte Punkte löschen.
5. Keine Secrets, nur Dateipfade. `CLAUDE.md` nur ändern, wenn sich Imports, Standardbefehle oder die Skill-Liste geändert haben.
```

### .gitignore (ergänzen, falls vorhanden)
```
CLAUDE.local.md
.claude/settings.local.json
.env
.env.*
node_modules/
dist/
__pycache__/
```