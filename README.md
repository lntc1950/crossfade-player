# Crossfade A/B

Videoplayer, der ein Video abspielt und zwei Tonspuren darunterlegt. Während das Video läuft, kann man zwischen Tonspur A und B crossfaden. Das Bild läuft ununterbrochen weiter.

## Im Browser verwenden

`index.html` im Browser öffnen, oder die GitHub-Pages-Adresse dieses Repos aufrufen. Video und zwei Tonspuren per Drag & Drop laden.

**Tasten:** Leertaste = Play/Pause · A / B = zu Spur A / B faden · X = hin und her · ← → = Fader bewegen

## Als Mac-App starten (Entwicklung)

Voraussetzung: [Node.js](https://nodejs.org) (LTS).

```bash
npm install
npm start
```

## Mac-App bauen

```bash
npm run build:mac
```

Die fertigen Apps liegen danach in `dist/`.

## Wie es funktioniert

- Alles steckt in `index.html` (HTML, CSS und JavaScript in einer Datei). `main.js` ist nur der Electron-Rahmen für die Mac-App.
- Das Video ist die Uhr. Beide Tonspuren werden mit der Web Audio API als Buffer dekodiert und sample-genau gemeinsam gestartet, sodass zwei Versionen desselben Mixes phasengleich bleiben.
- Crossfade-Kurven: Equal Power (−3 dB in der Mitte) oder linear (−6 dB).
- Bei Play, Pause, Spulen und Drift über 120 ms werden die Spuren mit kurzem Declick neu angesetzt.
- Pro Spur: Versatz in ms, Pegelanzeige, Warnung bei abweichender Länge.
- Grenze: Die Audiodateien werden komplett in den Arbeitsspeicher geladen. Für Spots und Clips ist das kein Problem, für Spielfilmlänge in WAV wird es schwer.
