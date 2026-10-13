# KI-Assistent für Julian – Was wir brauchen

Stand: 12.10.2026 · Kanal: Telegram

---

## Zugänge von Julian

- [ ] **Outlook** (E-Mail + Kalender) – der Assistent liest, priorisiert, antwortet
- [ ] **Trello** – zentrale To-do-Liste
- [ ] **OneDrive / Microsoft-Konto** – Ablage für Transkripte, Regeln, Vorlagen, Teilnehmerlisten
- [ ] **Telegram** – Julian installiert die App, startet den Bot „Alpenfieber Assistant" mit /start
- [ ] **Firmenkreditkarte** – Zapier-Abo, Claude-Guthaben (Anthropic), Whisper-Guthaben (OpenAI)

---

## Noch zu besorgen / einzurichten

- [ ] **Zweithandy** zum Aufnehmen der Anrufe (Recorder-App mit Auto-Upload in OneDrive)
- [ ] **Telegram-Bot** anlegen über @BotFather (5 Min, macht Victoria)
- [ ] *(später optional: Plaud Note statt Zweithandy)*

---

## Inhalte von Julian

- [ ] **Wer-ist-wer-Liste** – Team, wichtigste Kunden und Partner, je ein Satz
- [ ] **Aktuelle Events + Termine**
- [ ] **Freigabe der Anmeldebestätigung** (Entwurf liegt vor)
- [ ] **Prio-1-Themen** – welche Absender/Themen immer ganz oben stehen
- [ ] **Einwilligungssatz für Anrufaufnahme** (Pflicht in DE/CH)
- [ ] **Uhrzeiten bestätigen** – Morgen-Digest 7:30, Tagesabschluss 17:30

---

## Wichtig

- Keine Passwörter per Mail oder Chat – gemeinsam an Julians Rechner verbinden, er loggt sich selbst ein
- Termin einplanen: ca. 1 Stunde
- Alle Zugänge danach in den Firmen-Passwortmanager

---

## Was durch Telegram einfacher wird (gegenüber WhatsApp)

- **Keine zweite Telefonnummer / Prepaid-SIM** nötig
- **Keine Meta-Verifizierung, keine Firmenunterlagen**
- **Keine Nachrichten-Templates und keine Genehmigung** – der Bot sendet jederzeit
- **Kostenlos**

Einziger Unterschied für Julian: Er bekommt die Assistent-Nachrichten in Telegram, nicht in WhatsApp. Einmal App installieren und Bot starten, danach läuft es wie ein normaler Chat.

**Kein Whisper-Problem mehr offen:** Whisper transkribiert sowohl die Anrufaufnahmen vom Zweithandy als auch Julians Sprachnachrichten an den Bot. Läuft über ein OpenAI-Konto (API-Key), Kosten im Cent-Bereich.

---

## Ablauf des Agenten

**Auslöser → Daten sammeln → Claude verarbeitet → verteilen**
(Trello · Outlook-Kalender · Telegram · OneDrive)

---

## Die fünf Bausteine

| | Baustein | Auslöser | Ergebnis für Julian |
|---|---|---|---|
| 1 | Morgen-Digest | werktags 7:30 | priorisierte To-do-Liste per Telegram |
| 2 | Anruf-Pipeline | Aufnahme in OneDrive | Aufgaben + Deadlines automatisch angelegt |
| 3 | Notizen | Telegram an den Bot | wird zu Trello-Karte / Kalendereintrag |
| 4 | Anmeldungen | Event-Mail geht ein | Auto-Antwort + Teilnehmerliste + Nachfass-Karte |
| 5 | Tagesabschluss | werktags 17:30 | erledigt/offen + Boards aufgeräumt |
