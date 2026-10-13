# Übergabe-Protokoll: KI-Assistent Alpenfieber Events

**Erstellt von:** Victoria · **Für:** Julian (Betrieb & Pflege) · **Stand:** 12.10.2026

Dieses Dokument ist die zentrale Anlaufstelle. Es sagt, was das System tut, wo was liegt, was schon steht und was noch zu tun ist. Für den Alltag brauchst du nur Teil 1–4. Teil 5 (Technik-Anhang) ist für den Fall, dass jemand etwas anpassen muss.

---

## 1. Was das System ist – in drei Sätzen

Ein KI-Assistent, der Julian den Rücken freihält: Er liest morgens das Postfach und schickt eine priorisierte To-do-Liste, verwandelt Anrufe und Notizen automatisch in Trello-Karten und Kalender-Deadlines, beantwortet Event-Anmeldungen und räumt abends die Boards auf. Er läuft über **Zapier** (die Maschine), **Claude** (das Gehirn, das versteht und priorisiert) und **Telegram** (der Chat, über den Julian alles bekommt und seine Notizen hineinschickt). Niemand muss etwas manuell hoch- oder runterladen – alles läuft im Hintergrund.

---

## 2. Die fünf Bausteine auf einen Blick

| | Baustein | Wann | Was Julian davon hat |
|---|---|---|---|
| 1 | Morgen-Digest | werktags 7:30 | priorisierte To-do-Liste per Telegram |
| 2 | Anruf-Pipeline | nach jedem Anruf | Aufgaben + Deadlines automatisch angelegt |
| 3 | Notizen | jederzeit per Telegram | Notiz wird zu Trello-Karte / Termin |
| 4 | Anmeldungen | wenn Event-Mail kommt | Auto-Antwort + Teilnehmerliste + Nachfass-Karte |
| 5 | Tagesabschluss | werktags 17:30 | Review, was erledigt/offen ist, Boards aufgeräumt |

---

## 3. Status – was steht, was fehlt noch

> Felder zum Abhaken. Beim Übergabe-Termin gemeinsam durchgehen und aktualisieren.

**Konten & Zugänge**
- [ ] Zapier-Konto (Bezahl-Plan) angelegt, auf Firmenkreditkarte
- [ ] Anthropic/Claude-Konto + API-Key hinterlegt, Guthaben aufgeladen
- [ ] OpenAI-Konto + API-Key (für Whisper) hinterlegt, Guthaben aufgeladen
- [ ] Outlook mit Zapier verbunden
- [ ] Trello mit Zapier verbunden
- [ ] OneDrive mit Zapier verbunden
- [ ] Telegram-Bot „Alpenfieber Assistant" angelegt, Token hinterlegt
- [ ] Julian hat Bot-Chat gestartet, Chat-ID notiert

**Grundgerüst**
- [ ] Trello-Listen angelegt (Inbox, Heute, Diese Woche, Nachfassen, Erledigt)
- [ ] OneDrive-Ordner angelegt (Anrufe, Anrufe-Roh, Vorlagen, Teilnehmer, Prompts)
- [ ] Prompt-Dokument in OneDrive/Assistent/Prompts/ abgelegt
- [ ] Anmeldebestätigung-Vorlage abgelegt und von Julian freigegeben
- [ ] Zweithandy mit Auto-Upload nach OneDrive eingerichtet

**Die fünf Bausteine (je: gebaut / getestet / scharf)**
- [ ] Zap 3 – Notizen
- [ ] Zap 2 – Anruf-Pipeline
- [ ] Agent 1 – Morgen-Digest
- [ ] Zap 4 – Anmeldungen
- [ ] Agent 5 – Tagesabschluss

**Inhalte von Julian**
- [ ] Wer-ist-wer-Liste geliefert (als Knowledge hinterlegt)
- [ ] Aktuelle Events + Termine geliefert
- [ ] Prio-1-Themen festgelegt
- [ ] Einwilligungssatz für Anrufe festgelegt

---

## 4. Betrieb im Alltag (für Julian)

**Was du selbst tust**
- Anruf aufnehmen: vor dem Abheben die Aufnahme am Zweithandy starten, auf Lautsprecher telefonieren, zu Beginn den Einwilligungssatz sagen. Den Rest macht der Assistent.
- Notiz loswerden: dem Bot „Alpenfieber Assistant" in Telegram schreiben (Text oder Sprachnachricht). Die Karte entsteht automatisch.
- Morgens: den Digest lesen. Antwortest du darauf, werden daraus direkt neue Aufgaben.

**Wenn etwas komisch läuft – erste Hilfe**

| Symptom | Was tun |
|---|---|
| Kein Digest am Morgen | In Zapier den Agenten-Verlauf öffnen: roter Lauf? Meist ist eine App-Verbindung abgelaufen → Apps → betroffene Verbindung → „Reconnect" |
| Bot schreibt nicht | Hat Julian den Bot-Chat mit „Start" geöffnet? Chat-ID in Zapier korrekt? |
| Anruf wird nicht verarbeitet | Liegt die Aufnahme wirklich im OneDrive-Ordner „Anrufe-Roh"? Datei unter 25 MB? |
| Assistent sortiert/schreibt komisch | Kein Technik-Fehler: Das Prompt-Dokument in OneDrive anpassen und den Text in den Agenten/Zap kopieren |
| Doppelte Karten | Im Prompt die Regel „vor dem Anlegen auf Duplikate prüfen" schärfen |

**Das Prompt-Dokument ist die eine Stellschraube.** Es liegt in OneDrive unter `Assistent/Prompts/`. Darin steht in Klartext, wie der Assistent priorisiert, formuliert und entscheidet. Das darf jeder anpassen, der schreiben kann – kein Technikwissen nötig. Nach einer Änderung den Text in die Zapier-Agenten/Zaps kopieren (siehe Technik-Anhang).

**Laufende Kosten (grob):** Zapier-Abo ~30–50 €/Monat · Claude wenige € · Whisper unter 1 € · Telegram kostenlos. Zahlungen laufen über die Firmenkreditkarte.

---

## 5. Technik-Anhang (für spätere Anpassungen)

**Die Dokumente (alle in OneDrive unter `Assistent/`):**

| Datei | Inhalt |
|---|---|
| `agent_prompt_julian.md` | Der komplette Prompt – Rolle, Regeln, Formate. Die „Quelle der Wahrheit" |
| `zapier_bauplan.md` | Schritt für Schritt, wie jeder Zap/Agent aufgebaut ist |
| `telegram_einrichtung.md` | Wie Telegram + Bot angelegt werden |
| `checkliste_ki_assistent.md` | Alle Zugänge und Inhalte, die gebraucht werden |
| `ki_assistent_ablauf.html` | Das visuelle Schaubild des Gesamtablaufs |

**Architektur in einem Satz:** Auslöser (Zeitplan / Anruf / Telegram / E-Mail) → Zapier sammelt Daten aus Outlook, Trello, Kalender, OneDrive → Claude verarbeitet (gibt strukturiertes JSON zurück) → Zapier verteilt die Ergebnisse zurück an Trello, Kalender, OneDrive und Telegram.

**Wichtige Prinzipien, die man nicht brechen sollte:**
- **Claude gibt immer JSON zurück, keinen Fließtext.** Nur so lassen sich die Felder (Titel, Fälligkeit …) einzeln weiterverwenden. Wenn ein Zap plötzlich abbricht, ist meist das JSON kaputt → im Prompt „ohne Einleitung, ohne Backticks" schärfen.
- **Zwei Sicherheitsfilter nie entfernen:** der Absender-Filter in Zap 3 (nur Julians Chat-ID wird verarbeitet) und der Anmeldungs-Filter in Zap 4 (nur echte Anmeldungen lösen eine Auto-Antwort aus).
- **Prompt-Änderungen:** Datei in OneDrive ändern → den betroffenen Textblock in die Agent-Konfiguration bzw. den Claude-Schritt in Zapier kopieren → einmal testen (Zap auf „Off", „Test step") → wieder scharf schalten.

**Modelle:** Claude Sonnet für die Verarbeitung, Whisper (OpenAI) für die Transkription von Anrufen und Sprachnachrichten.

**Falls das System ganz übernommen/umgezogen werden soll:** Alle Zugänge liegen im Firmen-Passwortmanager (nicht an Victorias Person gebunden). Ein technischer Nachfolger arbeitet sich am besten über `zapier_bauplan.md` ein und baut Baustein für Baustein nach.

---

## 6. Kontakt & Wissensübergabe

- **Aufgebaut von:** Victoria
- **Empfohlene Übergabe:** gemeinsamer Termin (~1 Std.), in dem Status-Checkliste (Teil 3) durchgegangen und die Zugänge an Julian/Firma übertragen werden
- **Offene Entscheidungen zum Zeitpunkt der Übergabe:** *(hier beim Termin ergänzen – z. B. ob später auf Plaud Note umgestellt wird, ob WhatsApp doch noch dazukommt)*

---

*Dieses Protokoll aktuell halten: bei jeder größeren Änderung Datum oben anpassen und die Status-Checkliste nachziehen.*
