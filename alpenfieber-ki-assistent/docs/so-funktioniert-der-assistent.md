# So funktioniert der Assistent – alle Abläufe erklärt

Dieses Dokument erklärt in einfacher Sprache, was der Assistent kann, was in jedem Moment passiert, und was du selbst tun musst. Kein Technikwissen nötig.

**Stand:** 12.10.2026

---

## Das Grundprinzip in einem Bild

Der Assistent besteht aus drei Teilen, die zusammenarbeiten:

- **Zapier** = die Maschine. Sie wacht auf, holt Daten und schiebt Ergebnisse weiter. Sie denkt nicht selbst.
- **Claude** = das Gehirn. Es liest, versteht, priorisiert und entscheidet. Es handelt nicht selbst.
- **Telegram** = der Chat. Hier bekommst du alles und schickst deine Notizen hin.

Jeder Ablauf folgt immer demselben Muster:

> **Etwas löst aus → Zapier sammelt Infos → Claude versteht und entscheidet → Zapier verteilt das Ergebnis → du siehst es in Telegram, Trello oder im Kalender.**

Dazu arbeitet er mit deinen Programmen: **Outlook** (Mail + Kalender), **Trello** (deine To-do-Liste) und **OneDrive** (Ablage).

---

## Was der Assistent kann – und was nicht

**Er kann:**
- Dir morgens sagen, was heute wichtig ist
- E-Mails nach Dringlichkeit sortieren und die liegengebliebenen hervorheben
- Aus Anrufen automatisch Aufgaben und Termine machen
- Deine Notizen (getippt oder gesprochen) in Aufgaben verwandeln
- Fristen automatisch in den Kalender eintragen
- Event-Anmeldungen beantworten und niemanden vergessen
- Abends aufräumen und zeigen, was erledigt ist

**Er kann nicht (bewusst so):**
- E-Mails, Karten oder Termine löschen – er legt nur an und verschiebt
- Fremde Leute anschreiben – nur die eine freigegebene Anmeldebestätigung
- Entscheidungen für dich treffen – er bereitet vor, du entscheidest
- Zuhören, ohne dass du die Aufnahme startest – Anrufe nimmst du aktiv auf
- Raten, wenn etwas unklar ist – dann fragt er im Digest unter „Zum Klären" nach

**Grundhaltung:** Lieber einmal zu viel eine Karte anlegen als etwas vergessen. Nichts geht verloren.

---

## Ablauf 1: Der Morgen-Digest

**Wann:** Jeden Werktag um 7:30 Uhr, automatisch.

**Was im Hintergrund passiert:**
1. Zapier wacht um 7:30 auf
2. Es liest dein Outlook-Postfach (ungelesene + seit über 5 Tagen unbeantwortete Mails)
3. Es liest dein Trello-Board (was heute fällig oder überfällig ist)
4. Es liest deinen Kalender (Termine heute)
5. Claude sortiert alles nach Wichtigkeit und schreibt eine kurze Liste
6. Du bekommst sie als Telegram-Nachricht

**Was du tust:** Nur lesen. Und wenn dir dabei etwas einfällt, antworte einfach auf die Nachricht – daraus wird automatisch eine neue Aufgabe (siehe Ablauf 3).

**Beispiel, das du morgens bekommst:**
> ☀️ *Guten Morgen, Montag, 13.10.*
> *Heute wichtig:*
> 1. ⚠️ Angebot Müller GmbH – wartet seit 6 Tagen auf Antwort
> 2. Roadbook Lappland fertigstellen – fällig heute
> 3. Tatjana wegen Kontingent zurückrufen
> *Termine heute:* 📅 14:00 Call mit Jens

**Grenze:** Er entscheidet nicht, *ob* du etwas tust – er legt es dir nur sortiert vor.

---

## Ablauf 2: Die Anruf-Pipeline

**Wann:** Nach jedem Anruf, den du aufnimmst.

**Was du tust:**
1. Vor dem Abheben die Aufnahme am Zweithandy starten
2. Auf Lautsprecher telefonieren (sonst hört das Zweithandy nur dich)
3. Zu Beginn den Einwilligungssatz sagen (z. B. „Ich zeichne das kurz für meine Notizen auf, okay?")

**Was danach von allein passiert:**
1. Die Aufnahme lädt sich automatisch in OneDrive hoch
2. Whisper schreibt das Gespräch in Text um
3. Claude liest das Gespräch und zieht heraus: Aufgaben, Zusagen, Fristen, offene Punkte
4. Für jede Aufgabe entsteht eine Trello-Karte
5. Für jede Frist entsteht ein Kalendereintrag
6. Die Zusammenfassung landet in OneDrive
7. Du bekommst eine kurze Telegram-Bestätigung

**Beispiel:** Du telefonierst mit einem Partner. Er sagt: „Ich schick dir das Roadbook bis Donnerstag, und gib mir die Teilnehmerzahl für Lappland durch." Nach dem Auflegen hast du – ohne irgendetwas zu tippen – zwei Trello-Karten und eine Kalender-Deadline für Donnerstag.

**Wichtig:**
- Reine Infos ohne Aufgabe (z. B. „die Broschüre ist beim Drucker") werden nur abgelegt, nicht als Karte angelegt – damit dein Board nicht zumüllt.
- Aufnahme muss unter 25 MB bleiben (bei Mono + niedriger Qualität ca. 50 Minuten).

**Grenze:** Ohne Lautsprecher fehlt die Gegenseite. Und du musst die Aufnahme selbst starten – das ist der eine Handgriff, der bleibt.

---

## Ablauf 3: Notizen unterwegs

**Wann:** Immer, wenn dir etwas einfällt.

**Was du tust:** Dem Telegram-Bot „Alpenfieber Assistant" schreiben – getippt oder als Sprachnachricht. Ganz formlos, so wie du denkst.

**Was von allein passiert:**
1. Deine Nachricht kommt bei Zapier an (Sprachnachrichten werden vorher in Text umgewandelt)
2. Claude erkennt: Ist das eine Aufgabe, eine Idee oder eine Frage?
3. **Aufgabe** → Trello-Karte, bei Frist auch ein Kalendereintrag
4. **Idee** → Trello-Karte mit Label „Idee", ohne Frist
5. **Frage** → er antwortet dir direkt (z. B. „Was steht heute noch an?")
6. Du bekommst eine kurze Bestätigung

**Beispiel:**
> Du schreibst: „hotel gardasee wegen kontingent anschreiben bis mi"
> Antwort: „✓ Angelegt: Hotel Gardasee wegen Kontingent anschreiben – fällig Mi"

Im Hintergrund ist die Karte in Trello und die Deadline im Kalender – du hast nur einen Satz getippt.

**Grenze:** Je klarer deine Notiz, desto besser die Karte. Ist etwas unklar, legt er sie trotzdem an und fragt im nächsten Digest nach.

---

## Ablauf 4: Event-Anmeldungen

**Wann:** Wenn eine Anmeldung zu einem Alpenfieber-Event per Mail reinkommt.

**Was von allein passiert:**
1. Zapier erkennt die neue Mail
2. Claude prüft: Ist das wirklich eine Anmeldung? (kein Newsletter, kein Spam)
3. Wenn ja: Der Assistent antwortet mit deiner Bestätigungsvorlage, mit eingesetztem Namen
4. Die Person kommt in die Teilnehmerliste (OneDrive)
5. Es entsteht eine „Nachfassen"-Karte mit Frist in 3 Tagen

**Was du tust:** Nichts – außer die Vorlage einmal vorab freigeben. Später nur noch nachfassen, wenn die Karte dich daran erinnert.

**Der wichtige Punkt:** Die „Nachfassen"-Karte entsteht **immer**, auch wenn die automatische Antwort rausging. So geht kein Kontakt verloren, selbst wenn jemand nicht zurückschreibt.

**Grenze:** Er schreibt ausschließlich diese eine, von dir freigegebene Antwort. Alles andere beantwortest du selbst.

---

## Ablauf 5: Der Tagesabschluss

**Wann:** Jeden Werktag um 17:30 Uhr, automatisch.

**Was von allein passiert:**
1. Zapier vergleicht: Was war heute früh offen, was ist jetzt erledigt?
2. Erledigte Karten wandern nach „Erledigt"
3. Offene Karten werden auf morgen umdatiert
4. Claude schreibt dir eine kurze Abend-Übersicht

**Beispiel:**
> ✓ *Feierabend-Check, 13.10.*
> Erledigt heute: 4 von 6
> Bleibt offen (morgen): Angebot Müller GmbH · Roadbook Lappland
> Morgen als Erstes: Angebot Müller GmbH

**Was du tust:** Nur lesen. Du gehst mit einem aufgeräumten Board und klarem Kopf raus.

---

## Wenn mal was nicht läuft

| Du merkst … | Das ist meist … | Zu tun |
|---|---|---|
| Kein Digest am Morgen | eine abgelaufene App-Verbindung | in Zapier: Apps → betroffene neu verbinden |
| Bot meldet sich nicht | Chat nicht gestartet / falsche ID | Bot in Telegram mit „Start" öffnen |
| Anruf wird nicht verarbeitet | Aufnahme nicht hochgeladen / zu groß | prüfen, ob sie in OneDrive liegt, < 25 MB |
| Er sortiert/schreibt seltsam | der Prompt braucht Feinschliff | Prompt-Dokument in OneDrive anpassen |

Das Prompt-Dokument in OneDrive ist die Stellschraube für sein Verhalten – da steht in Klartext, wie er denkt. Das darf jeder ändern, der schreiben kann.

---

## Zusammengefasst: dein Teil vs. sein Teil

| Deine Aufgabe | Macht der Assistent |
|---|---|
| Aufnahme vor dem Anruf starten | Anruf auswerten, Aufgaben + Termine anlegen |
| Notizen in Telegram schicken | daraus Karten & Deadlines machen |
| Digest morgens/abends lesen | priorisieren, erinnern, aufräumen |
| Anmeldevorlage einmal freigeben | Anmeldungen beantworten & nachhalten |
| Bei Unklarheit kurz antworten | nachfragen statt raten |

Alles andere läuft im Hintergrund.

---

*Gehört zum Übergabe-Protokoll. Bei Fragen zum Aufbau: Zapier-Bauplan. Zum Verhalten ändern: Prompt-Dokument in OneDrive.*
