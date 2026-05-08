Aufgabenstellung:
kannst du mir diesen prompt verbessern? Ich möchte dass mein Handbuch auf redunazen gepürft wird. Die ausführlichkeit soll nicht geändert oder gekürzte werden. Es sollen nur einzelne .md Dateien verändert werden, dass zb. nicht in 3 dateien 3 mal das selbe steht. außerdem ist wichtig, dass wenn etwas nicht richtig dokumentiert wurde, keine annahmen getorffen werden sollen, sondern explizit in den einzlnen nodes, router, switch, firewall, etc.

# Betriebshandbuch-Optimierer – Redundanzbereinigung

## Zweck & Scope

Dieses Prompt analysiert eine Sammlung von `.md`-Dateien (z. B. Netzwerkdokumentation) auf **dateiübergreifende Redundanzen** und bereinigt diese – ohne dabei Inhalte zu kürzen, zu vereinfachen oder durch Annahmen zu ergänzen.

> **Kern-Prinzip**: Gleiche Information steht nach der Überarbeitung genau **einmal** – im semantisch passendsten Dokument. Alle anderen Dokumente verweisen darauf. Inhalte werden **nie** weggelassen oder umformuliert.

---

## Eingabe

Du erhältst eine oder mehrere `.md`-Dateien. Gib sie strukturiert an:

```
[DATEI: dateiname.md]
<Inhalt>

[DATEI: dateiname2.md]
<Inhalt>
```

---

## Schritt 1 – Inventarisierung

Erstelle intern eine Übersicht aller Dateien und ihrer Hauptthemen:

| Datei | Hauptthema | Enthaltene Entitäten (Nodes, Router, Switches, Firewalls, …) |
|---|---|---|

Identifiziere dabei:
- Welche **Entitäten** (Geräte, Systeme, Dienste) in welchen Dateien beschrieben werden
- Welche **Informationsblöcke** (Konfiguration, Zugänge, IP-Adressen, Rollen, Prozesse, …) mehrfach vorkommen

---

## Schritt 2 – Redundanzerkennung (dateiübergreifend)

Prüfe systematisch: Kommt dieselbe Information **wortgleich oder sinngleich** in mehreren Dateien vor?

Kategorisiere jeden Fund:

| Typ | Definition |
|---|---|
| **Vollduplikat** | Identischer Block in ≥ 2 Dateien |
| **Teilduplikat** | Überschneidende Inhalte, leicht unterschiedliche Formulierung oder Detailgrad |
| **Inkonsistenz** | Gleiche Entität, aber widersprüchliche Angaben |

> ⚠️ WICHTIG: Kein Inhalt wird stillschweigend entfernt. Jede Redundanz wird im Bericht dokumentiert und erst nach Entscheidung bereinigt.

---

## Schritt 3 – Bereinigungsregeln

### Vollduplikate
1. Behalte den Block **in der semantisch passendsten Datei** (z. B. Firewall-Regeln → `firewall.md`)
2. Ersetze den Block in allen anderen Dateien durch einen **Querverweis**:
   ```markdown
   → Siehe [`firewall.md#regelwerk`](firewall.md#regelwerk)
   ```
3. Kürze dabei **nichts** – der Querverweis ersetzt nur die Kopie, nicht den Inhalt

### Teilduplikate
1. Führe die vollständigste Version zusammen – **ergänze Details aus allen Varianten**
2. Platziere den zusammengeführten Block in der passendsten Datei
3. In anderen Dateien: Querverweis + ggf. datei-spezifische Ergänzung (z. B. lokale Ausnahme)

### Inkonsistenzen
Markiere mit:
```markdown
❗ KONFLIKT – [Entität/Thema]
- Datei A (`dateiname.md`): [Wert/Aussage A]
- Datei B (`dateiname2.md`): [Wert/Aussage B]
→ Empfehlung: [Welche Version korrekt erscheint und warum – falls erkennbar]
→ Muss manuell geprüft werden.
```
Keine Variante wird kommentarlos überschrieben.

---

## Schritt 4 – Fehlende Dokumentation

> ⚠️ WICHTIG: **Keine Annahmen treffen.** Wenn eine Information fehlt, wird sie **nicht erfunden oder geschätzt**.

Fehlt für eine Entität eine dokumentationspflichtige Information, wird sie **direkt in der Entitätsdokumentation** markiert:

```markdown
## Router: core-rtr-01

| Feld | Wert |
|---|---|
| Hersteller | Cisco |
| Modell | 🔄 NICHT DOKUMENTIERT |
| Management-IP | 10.0.0.1 |
| OS-Version | 🔄 NICHT DOKUMENTIERT |
| Standort | RZ Wien, Rack 3 |
| Verantwortlicher | 🔄 NICHT DOKUMENTIERT |
```

**Granularität**: Die Markierung `🔄 NICHT DOKUMENTIERT` steht **beim konkreten Feld der konkreten Entität** – nicht pauschal im Handbuch. Jeder Router, Switch, Node, Firewall etc. erhält seine eigene Prüfliste.

---

## Schritt 5 – Formatierung (Beibehaltung)

- **Detailgrad bleibt unverändert**: Kein Satz wird vereinfacht, zusammengefasst oder weggelassen
- **Formulierungen bleiben erhalten**: Nur Struktur und Platzierung ändern sich
- Markdown-Formatierung wird beibehalten und ggf. vereinheitlicht (`#`-Hierarchie, Tabellen, Listen)
- Querverweise im Format: `[Dateiname.md › Abschnitt](dateiname.md#anker)`

---

## Ausgabe – drei Bereiche

---

### 1. REDUNDANZBERICHT

Für jede identifizierte Redundanz:

```
[R-001] Vollduplikat – "VLAN-Konfiguration Switch-01"
Betroffen: network.md (Z. 45–67), switches.md (Z. 12–34)
Entscheidung: Verbleibt in switches.md → Querverweis in network.md eingefügt
```

Für jede Inkonsistenz:
```
[K-001] Konflikt – Gateway-IP für VLAN 10
- network.md: 192.168.10.1
- firewall.md: 192.168.10.254
→ Empfehlung: Abgleich mit aktiver Konfiguration erforderlich
```

**Zusammenfassung:**
- Vollduplikate bereinigt: X
- Teilduplikate zusammengeführt: X
- Konflikte offen (manuell zu lösen): X
- Fehlende Dokumentationsfelder markiert: X

---

### 2. ÜBERARBEITETE DATEIEN

Jede veränderte Datei vollständig ausgeben:

```
[DATEI: dateiname.md – überarbeitet]
<vollständiger Inhalt>
```

Unveränd­erte Dateien werden nicht wiederholt – nur mit einem Hinweis:
```
[DATEI: dateiname3.md – unverändert]
```

---

### 3. OFFENE PUNKTE

Gegliedert nach Priorität:

**Kritisch – Konflikte (müssen manuell aufgelöst werden):**
- ❗ [K-001] …

**Wichtig – Fehlende Pflichtfelder je Entität:**
- 🔄 Router `core-rtr-01`: Modell, OS-Version, Verantwortlicher
- 🔄 Firewall `fw-edge-01`: Regelwerk nicht dokumentiert
- 🔄 Switch `sw-access-02`: VLAN-Zuweisung fehlt
- …

**Optional – Strukturelle Empfehlungen:**
- …

---

## Absolute Regeln

| Regel | Erläuterung |
|---|---|
| Kein Inhalt entfernen | Nur Kopien werden durch Querverweise ersetzt |
| Keine Annahmen | Fehlende Infos → `🔄 NICHT DOKUMENTIERT` beim jeweiligen Feld |
| Kein Kürzen | Detailgrad und Formulierungen bleiben identisch |
| Entitätsgranular markieren | Jede Lücke wird dem konkreten Gerät/System zugeordnet |
| Konflikte eskalieren | Widersprüche werden nie stillschweigend aufgelöst |
