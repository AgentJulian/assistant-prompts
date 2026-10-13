# Telegram & Bot einrichten – Schritt für Schritt

Für den KI-Assistenten brauchen wir einen Telegram-Bot. Das ist der „Absender", über den Julian seine Nachrichten bekommt und dem er seine Notizen schickt. Keine Sorge – „Bot anlegen" klingt technisch, ist aber nur ein Chat mit einem Telegram-Assistenten, der alles für dich erledigt.

**Dauer:** ca. 15 Minuten · **Kosten:** kostenlos

---

## Teil 1: Telegram installieren (macht Julian)

1. **App Store** (iPhone) bzw. **Play Store** (Android) öffnen
2. Nach **Telegram** suchen
3. **Installieren** / **Laden** antippen
4. App öffnen → **Telefonnummer eingeben** (seine ganz normale Nummer, die darf er hier benutzen – anders als bei WhatsApp passiert hier nichts mit der Nummer)
5. Den **SMS-Code** eingeben, der ankommt
6. Vornamen eingeben – fertig

> Julians normales WhatsApp bleibt völlig unberührt. Telegram ist eine zusätzliche App daneben.

---

## Teil 2: Den Bot anlegen (macht Victoria)

Der „BotFather" ist der offizielle Telegram-Bot, mit dem man eigene Bots erstellt. Du schreibst ihm einfach wie einer Person.

1. In Telegram oben auf die **Lupe** (Suche) tippen
2. `BotFather` eingeben
3. Das Ergebnis mit dem **blauen Haken** antippen (offizieller Account – wichtig, es gibt Nachahmer)
4. Unten auf **Start** tippen (oder `/start` schreiben)
5. `/newbot` schreiben und senden
6. BotFather fragt nach dem **Namen** → eingeben: `Alpenfieber Assistant`
   *(Das ist der Anzeigename, den Julian im Chat sieht.)*
7. BotFather fragt nach dem **Benutzernamen** → der muss einzigartig sein und auf `bot` enden, z. B.:
   `alpenfieber_assistant_bot`
   *(Falls vergeben, probier eine Variante wie `alpenfieber_ai_bot`.)*
8. BotFather antwortet mit einer Nachricht, die einen **Token** enthält – eine lange Zeichenkette wie
   `8123456789:AAHxyz...`
   **Diesen Token kopieren und sicher speichern** (z. B. gleich in den Passwortmanager). Mit ihm verbindest du den Bot später in Zapier.

> Den Token behandeln wie ein Passwort – wer ihn hat, kann den Bot steuern.

---

## Teil 3: Julian startet den Chat (macht Julian)

Ein Bot darf niemandem schreiben, der ihn nicht zuerst angeschrieben hat. Deshalb muss Julian einmal den Chat öffnen:

1. In Telegram oben auf die **Lupe** tippen
2. Den Bot-Benutzernamen eingeben (z. B. `alpenfieber_assistant_bot`)
3. Den Bot antippen → unten auf **Start** tippen

Ab jetzt darf der Bot ihm schreiben. Dieser eine Chat ist später beides: Hier bekommt Julian den Morgen-Digest und die Erinnerungen, und hier schickt er seine Notizen hin.

---

## Teil 4: Julians Chat-ID holen (macht Victoria oder Julian)

Zapier muss wissen, an wen der Bot schreiben soll. Dafür braucht es Julians persönliche **Chat-ID** (eine Zahl).

1. In Telegram oben auf die **Lupe** tippen
2. `userinfobot` eingeben
3. Den Account **@userinfobot** antippen → **Start**
4. Er antwortet sofort mit einer Zahl bei **Id** (z. B. `123456789`)
5. **Diese Zahl notieren** – sie kommt in Zapier in jeden Sende-Schritt als „Chat ID"

> Wichtig: Das muss **Julian** auf seinem Telegram machen, denn es ist seine persönliche ID. Macht er es nicht selbst, bekommst du deine eigene ID statt seiner.

---

## Fertig – das hast du jetzt

- [ ] Telegram auf Julians Handy installiert
- [ ] Bot „Alpenfieber Assistant" angelegt
- [ ] Bot-Token sicher gespeichert
- [ ] Julian hat den Bot-Chat mit „Start" geöffnet
- [ ] Julians Chat-ID notiert

Mit **Token** und **Chat-ID** kannst du in Zapier die Telegram-Verbindung herstellen (steht im Zapier-Bauplan, Schritt 0a) und in jedem Sende-Schritt Julian als Empfänger eintragen.

---

## Häufige Stolpersteine

| Problem | Lösung |
|---|---|
| Mehrere „BotFather" in der Suche | Nur der mit **blauem Haken** ist echt |
| Benutzername wird abgelehnt | Ist schon vergeben – Variante mit `_ai_` oder Zahl probieren, muss auf `bot` enden |
| Bot schreibt Julian nicht | Julian hat „Start" noch nicht gedrückt – Teil 3 nachholen |
| Token verlegt | BotFather öffnen → `/mybots` → Bot wählen → „API Token" → neu anzeigen |
| Falsche Chat-ID | Julian muss @userinfobot selbst anschreiben, nicht Victoria |

---

*Stand: 12.10.2026 · gehört zum Zapier-Bauplan und der Checkliste*
