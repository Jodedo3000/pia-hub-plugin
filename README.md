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

- **VS Code / GitHub Copilot:** Befehl „Agent Plugins: Install Plugin From Source" und die URL dieses Repos angeben.
- **Cursor:** unterstützt den offenen Standard, Repo über die Plugin-Einstellungen einbinden.
- **ChatGPT / Codex:** sobald das Plugin im OpenAI Plugin Directory gelistet ist, über die Plugin-Suche. Bis dahin je nach Client über lokale Marketplace-Konfiguration.
- **Claude Code:** Repo als Marketplace hinzufügen und das Plugin installieren, oder einzelne `skills/*/SKILL.md` in das eigene Skill-Verzeichnis übernehmen.

## Wichtige Grenzen

- **Ausbildungswerkzeug, keine Gesundheitsversorgung.** Die Skills richten sich an Fachpersonen in Ausbildung. Sie geben keine Behandlungsempfehlungen an Laien und ersetzen weder Supervision noch Selbsterfahrung noch fachliche Prüfung.
- **Keine echten Patientendaten.** Übungsfälle sind fiktiv; reale Fälle gehören anonymisiert in die Supervision, nicht in einen KI-Chat.
- **Keine Risiko-Szenarien.** Die Patientensimulation erzeugt bewusst keine Szenarien mit akuter Suizidalität oder Fremdgefährdung. Der [Simulator des PiA Hub](https://piahub.netlify.app) deckt genau das ab, mit geprüfter Sicherheitslogik und evaluiertem Feedback. In einem fremden Host-Modell können wir dieses Sicherheitsverhalten nicht garantieren, deshalb liefern wir es dort nicht aus.
- **Host-Modell-Vorbehalt.** Die Skills steuern das Modell, in dem sie laufen, können dessen Antworten aber nicht garantieren. Vom Host generierte Prüfungsfragen sind, anders als die geprüfte Fragenbank im Hub, nicht redaktionell geprüft und werden entsprechend gekennzeichnet.

## Hintergrund

Der PiA Hub behält seine redaktionell und teils zweistufig (KI plus Fachperson) geprüften Inhalte, die autorierten Simulator-Fälle und die geprüfte Fragenbank auf der Plattform. Dieses Plugin verpackt die Methodik darüber: wie eine gute Fallkonzeption geführt wird, wie ein Übungsfall aufgebaut ist, wie lehrreiches Frage-Feedback aussieht. Erstellung KI-unterstützt, redaktionelle Verantwortung beim PiA Hub.
