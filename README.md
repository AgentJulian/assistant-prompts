[README.md](https://github.com/user-attachments/files/33368340/README.md)
# KI-Assistent – Alpenfieber Events

Ein persönlicher KI-Assistent für Julian (Geschäftsführer, Alpenfieber Events). Er priorisiert E-Mails, verwandelt Anrufe und Notizen automatisch in Aufgaben und Termine, beantwortet Event-Anmeldungen und räumt die Aufgaben-Boards auf.

**Kanal zu Julian:** Telegram · **Stand:** 13.10.2026

---

## Was das ist (und was nicht)

Dies ist ein **No-Code-System**. Es läuft über **Zapier** (die Automatisierungs-Plattform), **Claude** (das KI-Modell, das versteht und priorisiert) und **Telegram** (der Chat zu Julian). Es gibt **keine eigenständige Codebasis** – die Logik lebt in Zapier und in einem Prompt-Dokument. Dieses Repository ist die **Dokumentations- und Übergabe-Quelle**: alles, was man braucht, um das System zu verstehen, zu bauen, zu betreiben und weiterzugeben.

> Hinweis für Entwickler: In den Zapier-Schritten können einzelne JavaScript-Bausteine („Code by Zapier") vorkommen. Die maßgebliche Soll-Architektur ist der No-Code-Aufbau in `docs/zapier-bauplan.md`.

---

## Die fünf Bausteine

| # | Baustein | Auslöser | Ergebnis |
|---|---|---|---|
| 1 | Morgen-Digest | werktags 7:30 | priorisierte To-do-Liste per Telegram |
| 2 | Anruf-Pipeline | Aufnahme in OneDrive | Aufgaben + Deadlines automatisch |
| 3 | Notizen | Telegram an den Bot | Notiz → Trello-Karte / Termin |
| 4 | Anmeldungen | Event-Mail | Auto-Antwort + Teilnehmerliste + Nachfass-Karte |
| 5 | Tagesabschluss | werktags 17:30 | Review + Boards aufgeräumt |

**Architektur in einem Satz:** Auslöser → Zapier sammelt Daten (Outlook, Trello, Kalender, OneDrive) → Claude verarbeitet (gibt strukturiertes JSON zurück) → Zapier verteilt zurück an Trello, Kalender, OneDrive und Telegram. Transkription von Anrufen und Sprachnachrichten über Whisper (OpenAI).

---

## Inhalt dieses Repositories

```
.
├── README.md                     ← diese Datei
├── prompt/
│   └── agent-prompt.md           ← der vollständige Claude-Prompt (Quelle der Wahrheit)
├── docs/
│   ├── so-funktioniert-der-assistent.md   ← Abläufe in Alltagssprache (für Julian)
│   ├── uebergabe-protokoll.md             ← zentrale Übergabe + Status-Checkliste
│   ├── checkliste.md                      ← alle Zugänge & Inhalte
│   ├── telegram-einrichtung.md            ← Telegram + Bot Schritt für Schritt
│   └── zapier-bauplan.md                  ← Soll-Aufbau jedes Zaps/Agenten
└── diagramm/
    └── ablauf.html               ← visuelles Schaubild des Gesamtablaufs
```

---

## Wo anfangen?

- **Du willst verstehen, was das System tut:** `docs/so-funktioniert-der-assistent.md`
- **Du betreibst/pflegst es (Julian):** `docs/uebergabe-protokoll.md`
- **Du baust es in Zapier:** `docs/zapier-bauplan.md` + `docs/checkliste.md` + `docs/telegram-einrichtung.md`
- **Du willst das KI-Verhalten ändern:** `prompt/agent-prompt.md`

---

## Verhalten ändern

Das Verhalten des Assistenten steht in Klartext in `prompt/agent-prompt.md`. Beim Betrieb liegt eine Kopie davon in OneDrive (`Assistent/Prompts/`), die bei Änderungen in die Zapier-Agenten/Zaps kopiert wird. Wer den Prompt ändert, sollte danach hier im Repository dieselbe Änderung nachziehen, damit beides synchron bleibt.

---

## Wichtige Prinzipien

- **Claude gibt immer JSON zurück, keinen Fließtext** – nur so lassen sich die Felder (Titel, Fälligkeit …) in Folgeschritten einzeln verwenden.
- **Zwei Sicherheitsfilter nie entfernen:** der Absender-Filter (nur Julians Telegram-Chat-ID wird verarbeitet) und der Anmeldungs-Filter (nur echte Anmeldungen lösen eine Auto-Antwort aus).
- **Der Assistent löscht nie** – er legt an, verschiebt und erinnert.
- **Anrufaufnahme nur mit Einwilligung** des Gesprächspartners (DE/CH).

---

## Modelle & Dienste

Claude (Anthropic) für die Verarbeitung · Whisper (OpenAI) für Transkription · Zapier als Hub · Telegram als Kanal · Outlook, Trello, OneDrive als Datenquellen/Ziele.

---

*Aufgebaut von Victoria. Dieses Repository aktuell halten: bei jeder Änderung Datum anpassen und die Status-Checkliste im Übergabe-Protokoll nachziehen.*
