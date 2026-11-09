# DUET – Digital Key Card Generator

Digitale Codekarten für Codenames Duett. Die physischen Wortkarten bleiben auf dem Tisch, diese App ersetzt nur die geheime Codekarte.

Eine einzige Datei (`index.html`), reines HTML/CSS/JS, kein Server, keine Abhängigkeiten, funktioniert offline.

## Benutzung

1. Spieler 1 tippt auf **🎲 Neuen Seed generieren** und teilt den Seed (z. B. `DUET-8K4M-P7X2-Q9LW`).
2. Beide geben denselben Seed ein. Bindestriche, Leerzeichen und Gross-/Kleinschreibung spielen keine Rolle.
3. Spieler 1 wählt **A**, Spieler 2 wählt **B**, dann **Codekarte anzeigen**.

Gleicher Seed ergibt immer dieselbe Mission. Die zwei Seiten passen nach der Duett-Logik zusammen (je 9 Agenten, 3 Attentäter, 13 neutrale Felder).

URL-Vorbelegung: `index.html?seed=DUET-8K4M-P7X2-Q9LW&player=A` füllt Seed und Rolle im Setup vor. Die URL enthält keine Karteninfos.

## Privatsphäre

Die Karte wird beim Perspektivwechsel, bei „Verbergen“ und beim Verlassen des Tabs verborgen. Nichts wird gespeichert oder geloggt. Der Schutz gilt dem versehentlichen Einsehen, nicht gegen Leute, die den Quellcode lesen.

## Tests

`index.html?test=1` generiert 10.000 Seeds und prüft alle Regeln. Der Generator ist von der Oberfläche getrennt und exportiert sich bei Ausführung ohne `document` per `module.exports`, lässt sich also auch in Node testen.

Algorithmus: Seed-Normalisierung → FNV-1a-Hash → Mulberry32 → Fisher-Yates über die 25 gemeinsamen Kategorien (Details im Kommentar in `index.html`).

## Hosting (Docker)

```sh
docker build -t duet .
docker run -d --restart unless-stopped -p 8080:8080 duet
```

Für „Seed kopieren“ per Zwischenablage-API braucht es HTTPS, also einen Reverse Proxy mit TLS davor.
