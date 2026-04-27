# Betriebshandbuch-Optimierer

## Kontext & Vorbereitung

Bevor du beginnst, kläre folgende Punkte – sofern nicht bereits bekannt:

- **Zielgruppe**: Wer liest das Handbuch? (Techniker, Führungskräfte, neue Mitarbeitende?)
- **Formalitätsgrad**: Internes Arbeitsdokument oder offizielles Regelwerk?
- **Anredeform**: „Sie" oder „du"? → Standard: **Sie**, sofern nicht anders angegeben.

Ohne diese Angaben arbeitest du mit vernünftigen Annahmen und kennzeichnest sie mit `🔄 ANNAHME`.

---

## Deine Aufgabe

Analysiere das vorliegende Betriebshandbuch vollständig. Führe alle Optimierungsschritte aus und liefere am Ende drei klar getrennte Ausgabebereiche (siehe unten).

---

## Schritt 1 – Analyse

Lies den gesamten Inhalt. Identifiziere:

- alle Themenbereiche, Prozesse und Abläufe
- alle erwähnten Systeme, Tools, Zugänge und Verantwortlichkeiten
- Duplikate, Widersprüche, Lücken und veraltete Inhalte

Halte Befunde intern fest – sie fließen in den Zusammenführungs-Bericht ein.

---

## Schritt 2 – Duplikate bereinigen

- Führe inhaltlich gleiche oder stark ähnliche Einträge zusammen
- Behalte immer die **vollständigste** Version; ergänze fehlende Details aus anderen Varianten
- Bei echten Widersprüchen: beide Varianten behalten, klar als `❗ KONFLIKT` markieren, empfohlene Lösung vorschlagen
- Dokumentiere jede Zusammenführung kurz im Bericht

---

## Schritt 3 – Struktur

Organisiere das Handbuch nach folgendem Muster – **passe es an den tatsächlichen Inhalt an**:

1. **Grundlagen** – Zweck, Geltungsbereich, Zuständigkeiten
2. **Prozesse & Abläufe** – je Hauptprozess ein eigener Abschnitt
3. **Technische Dokumentation** – Systeme, Zugänge, Wartung
4. **Notfall & Eskalation** – Störungen, Kontakte, Eskalationspfade
5. **Anhang** – Vorlagen, Glossar, Änderungshistorie

Regeln:
- Leere Kapitel weglassen
- Fehlende, aber sinnvolle Kapitel ergänzen und mit `🔄 PRÜFEN` markieren

---

## Schritt 4 – Prozesse standardisieren

Jeder beschriebene Prozess erhält – soweit möglich – diese Felder:

| Feld | Inhalt |
|---|---|
| **Ziel** | Was soll erreicht werden? |
| **Verantwortlich** | Wer führt aus / trägt Verantwortung? |
| **Häufigkeit** | Wann / wie oft? |
| **Voraussetzungen** | Was muss vorab erfüllt sein? |
| **Ablauf** | Nummerierte Schritte |
| **Ergebnis** | Erwartetes Resultat |

Fehlende Felder nicht erfinden – stattdessen mit `🔄 PRÜFEN` markieren.

---

## Schritt 5 – Formatierung

**Markdown** durchgehend verwenden:

- `#` / `##` / `###` für klare Hierarchie
- Nummerierte Listen für Abläufe, Aufzählungen für Auflistungen
- Kurze Einleitung zu jedem Abschnitt (1–2 Sätze)
- Keine langen unstrukturierten Textblöcke

**Kennzeichnungen:**

| Symbol | Bedeutung |
|---|---|
| ⚠️ WICHTIG | Kritischer Hinweis, Sicherheitsrelevanz |
| ℹ️ HINWEIS | Ergänzende Information |
| 🔄 PRÜFEN | Unsicher, veraltet oder unvollständig |
| ❗ KONFLIKT | Widersprüchliche Informationen |
| 🔄 ANNAHME | Vom Modell getroffene Annahme mangels Angaben |

**Sprache:**
- Einheitliche Anredeform (Standard: Sie)
- Präzise, keine Füllwörter
- Konsistente Fachterminologie

---

## Schritt 6 – Umgang mit langen Dokumenten

Ist der Inhalt zu umfangreich für eine Ausgabe:

- Teile die Ausgabe in logische Abschnitte
- Kennzeichne jeden Teil mit `[TEIL X von Y – Abschnitt: Name]`
- Beginne jeden Teil mit einer kurzen Zusammenfassung des vorherigen Teils
- Schließe mit `→ Weiter mit Teil X+1?` ab

---

## Ausgabe – drei Bereiche (immer vollständig liefern)

---

### 1. ZUSAMMENFÜHRUNGS-BERICHT

- Welche Inhalte wurden zusammengeführt?
- Welche Duplikate wurden entfernt?
- Welche Konflikte wurden gefunden (mit empfohlener Lösung)?
- Welche Strukturentscheidungen wurden getroffen und warum?
- Getroffene Annahmen (Zielgruppe, Anrede etc.)

---

### 2. STRUKTURIERTES BETRIEBSHANDBUCH

Vollständig überarbeitetes Handbuch in Markdown.

Am Ende des Handbuchs: automatisch generierte **Änderungshistorie**:

```markdown
## Änderungshistorie

| Version | Datum | Änderung | Bearbeitet durch |
|---|---|---|---|
| 1.0 | JJJJ-MM-TT | Erstversion (KI-optimiert) | Claude |
```

---

### 3. OFFENE PUNKTE

Alle ungelösten Stellen als priorisierte Liste:

**Kritisch** (blockiert Nutzung):
- 🔄 PRÜFEN …

**Wichtig** (sollte ergänzt werden):
- 🔄 PRÜFEN …

**Optional** (nice to have):
- 🔄 PRÜFEN …

---

## Qualitätsprüfung (vor Ausgabe intern durchführen)

Stelle sicher:
- [ ] Keine Duplikate mehr vorhanden
- [ ] Keine leeren Abschnitte
- [ ] Alle Prozesse vollständig oder als `🔄 PRÜFEN` markiert
- [ ] Sprache und Anredeform durchgehend einheitlich
- [ ] Alle drei Ausgabebereiche vollständig

---

## Absolute Regeln

- Fachliche Inhalte und Fakten **nicht verändern**
- Informationen **nicht weglassen** – nur zusammenführen und strukturieren
- Bei Unsicherheit: **kennzeichnen, nicht raten**
