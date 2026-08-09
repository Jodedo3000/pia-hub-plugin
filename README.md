# PiA Hub Agent Plugin

Psychotherapie-Ausbildungskompetenz als installierbare Agent Skills, nach dem offenen [Agent-Plugins-Standard 1.0](https://agent-plugins.org). Aus der Methodik des [PiA Hub](https://piahub.netlify.app), einem deutschsprachigen Wissens- und Trainings-Hub für Psychotherapeut:innen in Ausbildung (PiA, altes Recht, PsychThG vor 2020).

**Status: Experiment (v0.1).** Dieses Plugin ist ein früher Versuch, Fachmethodik portabel zu machen, statt sie an eine einzelne App zu binden. Feedback ist willkommen.

## Was drin ist

| Skill | Was er kann | Beispiel-Prompt |
|---|---|---|
| `fallkonzeption` | Führt Schritt für Schritt durch eine verhaltenstherapeutische Fallkonzeption (SORKC, Makroanalyse, Ziele, Interventionen) | „Führe mich durch eine Fallkonzeption für meinen anonymisierten Übungsfall" |
| `patienten-simulation` | Erzeugt fiktive Patient:innen nach Protokoll und spielt ein Erstgespräch mit verdeckten Informationen, danach strukturiertes Feedback | „Simuliere eine Patientin für ein Erstgespräch, Schwierigkeitsgrad mittel" |
| `pruefungs-coach` | Stellt MC-Fragen im Stil des PiA-Hub-Trainers (Fallvignetten, Erklärung zu jeder Option, Lern-Tipp) und generiert neue im selben Format | „Stell mir fünf Prüfungsfragen zu Diagnostik und Klassifikation" |
| `ausbildungs-navigator` | Beantwortet Fragen zum Ausbildungsweg nach altem Recht (PT1/PT2, Bausteine, Kostenlogik, Prüfung) | „Erkläre mir den Unterschied zwischen PT1 und PT2" |

## Installation

Das Paket folgt dem Agent-Plugins-Standard (Root-`plugin.json`) und trägt zusätzlich ein Claude-Code-Manifest (`.claude-plugin/plugin.json`), dasselbe Repo läuft also in beiden Welten.

### Claude Code

Zwei Befehle in einer laufenden Sitzung:

```
/plugin marketplace add Jodedo3000/pia-hub-plugin
/plugin install pia-hub@pia-hub-marketplace
```

Der erste Befehl meldet dieses Repository als Bezugsquelle an, der zweite installiert das Plugin daraus. Beim Installieren fragt Claude Code nach dem Geltungsbereich, „user" heißt in allen Projekten verfügbar. Falls die Zusammenfassung dazu auffordert, danach `/reload-plugins` ausführen.

Anschließend stehen die vier Skills bereit, mit dem Plugin-Namen als Präfix:

```
/pia-hub:fallkonzeption
/pia-hub:patienten-simulation
/pia-hub:pruefungs-coach
/pia-hub:ausbildungs-navigator
```

Du kannst sie auch einfach beschreiben statt aufrufen. Wer nach einer SORKC-Analyse fragt, bekommt den passenden Skill automatisch.

**Nur einen einzelnen Skill, ohne Plugin-Installation:**

```
git clone https://github.com/Jodedo3000/pia-hub-plugin.git
mkdir -p ~/.claude/skills
cp -r pia-hub-plugin/skills/fallkonzeption ~/.claude/skills/
```

Der Skill heißt dann `/fallkonzeption`, ohne Präfix, und gilt in allen Projekten. Für ein einzelnes Projekt nimmst du `.claude/skills/` im Projektverzeichnis. Zum reinen Ausprobieren ohne Installation genügt `claude --plugin-dir ./pia-hub-plugin`.

### ChatGPT und Codex

Noch nicht im OpenAI Plugins Directory gelistet, die Installation läuft deshalb lokal. Praktischerweise liest die ChatGPT-Desktop-App dieselbe `.claude-plugin/marketplace.json` mit, die auch Claude Code nutzt.

1. Repository klonen: `git clone https://github.com/Jodedo3000/pia-hub-plugin.git`
2. ChatGPT-Desktop-App öffnen, in den Work-Mode wechseln oder Codex wählen.
3. Den geklonten Ordner als Arbeitsverzeichnis öffnen und **Plugins** aufrufen. Im Codex CLI öffnet `/plugins` denselben Browser.
4. Installieren, dann eine neue Unterhaltung starten. Die Skills laden erst in einer frischen Sitzung.

Nach einem `git pull` die Desktop-App neu starten, damit die aktualisierten Dateien greifen.

### VS Code, GitHub Copilot und Cursor

- **VS Code / GitHub Copilot:** Befehl „Agent Plugins: Install Plugin From Source" und die URL dieses Repos angeben.
- **Cursor:** unterstützt den offenen Standard, Repo über die Plugin-Einstellungen einbinden.

## Wichtige Grenzen

- **Ausbildungswerkzeug, keine Gesundheitsversorgung.** Die Skills richten sich an Fachpersonen in Ausbildung. Sie geben keine Behandlungsempfehlungen an Laien und ersetzen weder Supervision noch Selbsterfahrung noch fachliche Prüfung.
- **Keine echten Patientendaten.** Übungsfälle sind fiktiv; reale Fälle gehören anonymisiert in die Supervision, nicht in einen KI-Chat.
- **Keine Risiko-Szenarien.** Die Patientensimulation erzeugt bewusst keine Szenarien mit akuter Suizidalität oder Fremdgefährdung. Der [Simulator des PiA Hub](https://piahub.netlify.app) deckt genau das ab, mit geprüfter Sicherheitslogik und evaluiertem Feedback. In einem fremden Host-Modell können wir dieses Sicherheitsverhalten nicht garantieren, deshalb liefern wir es dort nicht aus.
- **Host-Modell-Vorbehalt.** Die Skills steuern das Modell, in dem sie laufen, können dessen Antworten aber nicht garantieren. Vom Host generierte Prüfungsfragen sind, anders als die geprüfte Fragenbank im Hub, nicht redaktionell geprüft und werden entsprechend gekennzeichnet.

## Hintergrund

Der PiA Hub behält seine redaktionell und teils zweistufig (KI plus Fachperson) geprüften Inhalte, die autorierten Simulator-Fälle und die geprüfte Fragenbank auf der Plattform. Dieses Plugin verpackt die Methodik darüber: wie eine gute Fallkonzeption geführt wird, wie ein Übungsfall aufgebaut ist, wie lehrreiches Frage-Feedback aussieht. Erstellung KI-unterstützt, redaktionelle Verantwortung beim PiA Hub.
