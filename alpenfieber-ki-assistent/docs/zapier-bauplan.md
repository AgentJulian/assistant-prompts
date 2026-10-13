# Zapier-Bauplan: KI-Assistent für Julian

Stand: 12.10.2026 · Version 2.0 (Telegram) · Gehört zu `agent_prompt_julian.md` und der Checkliste

---

## Vorab: Zwei Bauweisen, und wann welche

Zapier kennt zwei Arten von Bausteinen. Der Unterschied entscheidet, wie du jeden der fünf Teile baust:

| | **Zap** (klassisch) | **Agent** |
|---|---|---|
| Aufbau | feste Kette: Schritt 1 → 2 → 3 | ein Textfeld mit Anweisungen + Werkzeuge |
| Verarbeitet | **ein** Ereignis pro Lauf | kann mehrfach nachschauen, sammeln, kombinieren |
| Claude | eigener Schritt „Anthropic (Claude)" | eingebautes Modell |
| Gut für | Anruf, Notiz, Anmeldung | Digest, Tagesabschluss |

**Die Regel dahinter:** Ein Zap ist eine gerade Linie – super, wenn genau ein Ding reinkommt (ein Anruf, eine Notiz, eine Mail). Sobald etwas *viele* Dinge einsammeln und abwägen muss (alle offenen Mails + alle fälligen Karten + alle Termine), wird ein Zap unhandlich. Dafür ist der Agent gebaut.

**Deshalb der Plan:** Zap 2, 3, 4 als klassische Zaps mit Claude-Schritt. Baustein 1 und 5 als Agent. Der Prompt bleibt in beiden Fällen derselbe Text – nur das Feld, in das du ihn einfügst, heißt anders.

---

## Was Telegram gegenüber WhatsApp spart

- **Keine Templates, keine Meta-Genehmigung.** Der Bot sendet jederzeit, sobald Julian ihn einmal mit `/start` angeschrieben hat. Das 24-Stunden-Fenster und die drei Utility-Templates aus der alten Version entfallen komplett.
- **Keine zweite Telefonnummer, keine Prepaid-SIM.**
- **Kostenlos.** Telegram-Bots kosten nichts.
- **Ein Chat in beide Richtungen.** Derselbe Bot-Chat ist Ausgang (Digest, Bestätigungen) und Eingang (Julians Notizen).

---

## Reihenfolge des Bauens

0. **Telegram-Bot anlegen** (5 Min, siehe Schritt 0b)
1. **Zap 3 (Notizen)** – der kleinste, zum Prinzip verstehen
2. **Zap 2 (Anrufe)** – der wertvollste
3. **Agent 1 (Morgen-Digest)** – der sichtbarste
4. **Zap 4 (Anmeldungen)**
5. **Agent 5 (Tagesabschluss)**

Jeden Baustein fertig testen, bevor der nächste anfängt.

---

## Schritt 0a: Zapier vorbereiten (einmalig, ca. 20 Min)

**Apps verbinden** (links „Apps" → „Add connection"):

- [ ] Microsoft Outlook (Julians Konto) – E-Mail **und** Kalender
- [ ] Trello
- [ ] Microsoft OneDrive
- [ ] Anthropic (Claude) – braucht API-Key von console.anthropic.com
- [ ] OpenAI – für Whisper (Sprachnachrichten + Anruf-Transkription), API-Key von platform.openai.com
- [ ] Telegram – Bot-Token aus Schritt 0b

**Ordner anlegen** (linke Leiste → „Folders"): `Assistent Julian` – da kommen alle fünf Bausteine rein.

**Namensschema:** `01_Morgen-Digest`, `02_Anrufe`, `03_Notizen`, `04_Anmeldungen`, `05_Tagesabschluss`.

**Anthropic-Key holen:** console.anthropic.com → Konto anlegen (Firmen-Mail!) → Settings → API Keys → „Create Key" → kopieren → in Zapier bei der Anthropic-Verbindung einfügen. Guthaben aufladen (20 $ reichen für Monate).

---

## Schritt 0b: Telegram-Bot anlegen (einmalig, ca. 5 Min)

1. In Telegram den Kontakt **@BotFather** öffnen (offizieller Telegram-Bot zum Bot-Erstellen).
2. `/newbot` schicken.
3. Anzeigename eingeben: **Alpenfieber Assistant**
4. Benutzername eingeben (muss auf `bot` enden): z. B. `alpenfieber_assistant_bot`
5. BotFather antwortet mit einem **Token** (lange Zeichenkette wie `8123456789:AAH...`). Den sicher speichern – mit dem verbindest du Telegram in Zapier.
6. **Julian startet den Chat:** Er sucht den Bot-Benutzernamen in Telegram, öffnet den Chat und drückt **Start** (bzw. schickt `/start`). Erst danach darf der Bot ihm schreiben.
7. **Julians Chat-ID holen** (brauchst du als Empfänger in Zapier): Einfachster Weg – in Telegram **@userinfobot** anschreiben, der nennt die numerische ID. Diese ID trägst du in jedem Sende-Schritt als „Chat ID" ein.

---

## Zap 3: Notizen (der Einstieg)

**Was er tut:** Julian schreibt dem Bot „hotel gardasee wegen kontingent bis mi" → Trello-Karte + Kalendereintrag + kurze Bestätigung.

| # | App | Event | Konfiguration |
|---|---|---|---|
| 1 | Telegram | New Message (in Bot-Chat) | der Bot aus Schritt 0b |
| 2 | Filter by Zapier | Only continue if… | Absender-ID = Julians Chat-ID. **Nicht weglassen** – sonst reagiert der Bot auf Fremde |
| 3a | Filter/Paths | Audio oder Text? | nur wenn Sprachnachricht → 3b |
| 3b | OpenAI | Create Transcription (Whisper) | Audiodatei aus Schritt 1, Sprache `de` |
| 4 | Anthropic (Claude) | Send Message | Model: Sonnet · Prompt: siehe unten |
| 5 | Trello | Create Card | Board „Julian", Liste „Inbox" |
| 6 | Filter by Zapier | Only continue if… | Feld „faelligkeit" ist nicht leer |
| 7 | Outlook | Create Event | Titel `DEADLINE: {Titel}`, Erinnerung 120 Min vorher |
| 8 | Telegram | Send Message | an Julians Chat-ID: `✓ Angelegt: {Titel} – fällig {faelligkeit}` |

**Was in Schritt 4 (Claude) ins Nachrichtenfeld kommt:**

Aus `agent_prompt_julian.md` die Blöcke `<rolle>`, `<kontext>`, `<aufgabe_3>`, `<regeln_trello>`, `<regeln_deadlines>`, `<beispiel_notiz>` – und darunter:

```
Heutiges Datum: {{Zapier: heutiges Datum}}
Nachricht von Julian: {{Schritt 1: Message Text / bzw. Schritt 3b: Transkript}}

Antworte AUSSCHLIESSLICH mit diesem JSON, ohne Einleitung, ohne Backticks:
{"typ":"aufgabe|idee|frage","titel":"...","beschreibung":"...","faelligkeit":"JJJJ-MM-TT oder leer","antwort":"..."}
```

> **Der wichtigste Trick im ganzen Bauplan:** Claude muss **JSON** zurückgeben, keinen Fließtext. Nur dann kannst du in Schritt 5–8 einzelne Felder (`titel`, `faelligkeit`) gezielt in Trello und Kalender einsetzen. Gilt für jeden Zap hier.

**Test:** Zap auf „Off" lassen, „Test step" bei jedem Schritt einzeln. Julian schickt dem Bot eine Testnotiz. Prüfen: Kommt sauberes JSON? Landet die Karte in „Inbox"? Wird „bis mi" korrekt in ein Datum umgerechnet? Kommt die Bestätigung im Telegram-Chat an?

---

## Zap 2: Anruf-Pipeline (der wertvollste)

**Was er tut:** Anruf endet → Aufnahme landet in OneDrive → Whisper transkribiert → Claude zieht Aufgaben und Fristen raus → alles landet automatisch, wo es hingehört.

| # | App | Event | Konfiguration |
|---|---|---|---|
| 1 | OneDrive | New File in Folder | `Assistent/Anrufe-Roh/` |
| 2 | OpenAI | Create Transcription (Whisper) | Datei aus Schritt 1, Sprache `de`, Format `text` |
| 3 | OneDrive | Upload File | Transkript als `.md` in `Assistent/Anrufe/` |
| 4 | Anthropic (Claude) | Send Message | Model: Sonnet · Prompt: siehe unten |
| 5 | Looping by Zapier | Create Loop From Text | Aufgabenliste aus Schritt 4 aufteilen |
| 6 | Trello | Create Card | pro Durchlauf eine Karte, Liste „Inbox" |
| 7 | Filter by Zapier | Only continue if… | Karte hat eine Frist |
| 8 | Outlook | Create Event | `DEADLINE: {Titel}` |
| 9 | Telegram | Send Message | an Julians Chat-ID, Text nach `<format_anruf>` + OneDrive-Link |

**Was in Schritt 4 ins Nachrichtenfeld kommt:**

`<rolle>`, `<kontext>`, `<aufgabe_2>`, `<regeln_trello>`, `<regeln_deadlines>`, `<beispiel_anruf>` – und darunter:

```
Heutiges Datum: {{Zapier: heutiges Datum}}
Transkript: {{Schritt 2: Transkript-Text}}

Antworte AUSSCHLIESSLICH mit diesem JSON:
{"gespraechspartner":"...","zusammenfassung":"...","aufgaben":[{"titel":"...","beschreibung":"...","faelligkeit":"JJJJ-MM-TT oder leer"}],"nur_info":["..."]}
```

**Warum Schritt 5 (Looping):** Ein Anruf erzeugt meist mehrere Aufgaben. Der Looping-Baustein sorgt dafür, dass Schritt 6–8 für **jede** Aufgabe einmal laufen. Alles unter `nur_info` wird bewusst ignoriert – die vierte Route aus dem Diagramm.

**Wichtig zu Whisper:** Audiodatei max. 25 MB. Recorder im Zweithandy auf Mono + niedrige Bitrate (64 kbit/s m4a) stellen → ~50 Min passen rein. Und: Zweithandy nimmt nur per Lautsprecher beide Seiten auf.

**Test:** Eine kurze Testaufnahme mit zwei erfundenen Aufgaben und einer Frist in den Ordner legen. Prüfen: zwei Karten? Eine Deadline? Reine Info **nicht** als Karte? Bestätigung im Telegram?

---

## Agent 1: Morgen-Digest

Hier kein Zap, sondern ein **Agent** – er schaut an drei Stellen nach und wägt ab.

**Anlegen:** Agents → New Agent → Name `01_Morgen-Digest`

**Trigger:** Schedule → Every Day → 7:30 Uhr → „Weekends: off"

**Instructions:** aus `agent_prompt_julian.md` die Blöcke `<rolle>`, `<kontext>`, `<aufgabe_1>`, `<prioritaetsregeln>`, `<regeln_trello>`, `<verhaltensregeln>`, `<format_digest>`

**Tools** (im Anweisungstext per `/` einfügen):

- Outlook → *Find Emails* (ungelesen + älter als 5 Tage unbeantwortet)
- Trello → *Find Cards* (Board „Julian", fällig heute oder überfällig)
- Outlook → *Find Events* (heute)
- Trello → *Move Card* (fällige Karten nach „Heute")
- Telegram → *Send Message* (an Julians Chat-ID)

**Knowledge:** die Wer-ist-wer-Liste, sobald Julian sie geliefert hat. Sonst leer.

**Test:** über „Agent Preview" manuell auslösen. Prüfen: alte unbeantwortete Mails mit ⚠️ oben? Max. 10 Punkte? Format wie in `<format_digest>`? Kommt der Digest im Telegram-Chat an?

**Erst nach drei sauberen Testläufen** den Zeitplan aktivieren.

---

## Zap 4: Anmeldungen

| # | App | Event | Konfiguration |
|---|---|---|---|
| 1 | Outlook | New Email | Posteingang, ggf. auf Ordner/Betreff eingrenzen |
| 2 | Anthropic (Claude) | Send Message | Erkennt: Anmeldung ja/nein + Name + Event |
| 3 | Filter by Zapier | Only continue if… | `ist_anmeldung` = ja |
| 4 | OneDrive | Get File Contents | `Assistent/Vorlagen/anmeldung_bestaetigung.md` |
| 5 | Outlook | Send Email | Vorlage mit eingesetztem Namen, an den Absender |
| 6 | OneDrive / Excel | Add Row | `Assistent/Teilnehmer/{Event}.xlsx` |
| 7 | Trello | Create Card | `Nachfassen: {Name} – {Event}`, Liste „Nachfassen", fällig +3 Tage |

**Prompt für Schritt 2:**

```
<rolle> + <kontext> + <aufgabe_4>

E-Mail von: {{Schritt 1: From}}
Betreff: {{Schritt 1: Subject}}
Text: {{Schritt 1: Body}}

Antworte AUSSCHLIESSLICH mit JSON:
{"ist_anmeldung":"ja|nein","name":"...","event":"...","begruendung":"..."}
```

> **Vorsicht bei Schritt 3:** Der Filter ist die einzige Bremse zwischen dem Zap und dem Postfach. Lieber zu streng – im Zweifel „nein", dann landet die Mail normal im Postfach und Julian sieht sie im Morgen-Digest.

**Test:** Von einer privaten Adresse eine Test-Anmeldung schicken. Und einmal eine Nicht-Anmeldung – der Filter muss sie stoppen.

---

## Agent 5: Tagesabschluss

**Anlegen:** Agents → New Agent → `05_Tagesabschluss`

**Trigger:** Schedule → werktags 17:30

**Instructions:** `<rolle>`, `<kontext>`, `<aufgabe_5>`, `<verhaltensregeln>`, `<format_abschluss>`

**Tools:** Trello *Find Cards* · Trello *Move Card* (nach „Erledigt") · Trello *Update Card* (offene Karten auf morgen umdatieren) · Telegram *Send Message*

**Test:** manuell auslösen, prüfen ob aufgeräumt wird und das Review kurz bleibt.

---

## Notiz-Eingang ab Tag 1 (ohne Zapier)

Schon bevor Zap 3 steht, kann Julian Notizen loswerden: E-Mail an die Trello-Board-Adresse (Betreff = Kartentitel). Funktioniert sofort. Sobald Zap 3 läuft, ist der Telegram-Bot der bequemere Weg.

---

## Testregeln (für alle Bausteine gleich)

1. Zap/Agent bleibt auf **Off**, solange getestet wird
2. Jeden Schritt einzeln testen, nicht den ganzen Zap auf einmal
3. Immer mit **echtem** Material testen, nie mit Zapiers Beispieldaten
4. Nach dem Scharfschalten die ersten drei Tage täglich in den Verlauf schauen
5. Fehler in der Ausgabe = fast nie ein Zapier-Problem, sondern der Prompt → in OneDrive anpassen, in Zapier einfügen

---

## Wenn etwas nicht läuft

| Symptom | Ursache | Lösung |
|---|---|---|
| Claude-Schritt bricht ab | Antwort war kein sauberes JSON | im Prompt schärfer: „ohne Einleitung, ohne Backticks" |
| Bot schreibt Julian nicht | Julian hat `/start` noch nicht gedrückt, oder falsche Chat-ID | Chat starten lassen, ID mit @userinfobot prüfen |
| Karte wird angelegt, Termin nicht | Feld `faelligkeit` war leer | so gewollt – Filter greift korrekt |
| Nur eine Karte statt mehrerer | Looping-Schritt fehlt/falsch | Schritt 5 in Zap 2 prüfen |
| Zap läuft gar nicht | App-Verbindung abgelaufen | Apps → Verbindung → „Reconnect" |
| Bot reagiert auf Fremde | Absender-Filter fehlt | Schritt 2 in Zap 3 nachrüsten – dringend |
| Sprachnachricht wird nicht verstanden | Whisper-Schritt fehlt/Datei zu groß | Schritt 3b prüfen, Audio < 25 MB |

---

*Version 2.0 · 12.10.2026 · ersetzt die WhatsApp-Version*
