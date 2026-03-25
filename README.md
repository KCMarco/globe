# Globe mit [cobe](https://github.com/shuding/cobe)

Ja — ich habe dir cobe hier direkt eingebaut.

## Was jetzt im Repo ist

- `index.html`: Standard-Globe-Variante als einfacher Startpunkt.
- `globe-transparent.html`: Transparente Variante (gut für Embeds auf farbigem Hintergrund).

## So testest du es lokal

```bash
python3 -m http.server 4173
```

Dann im Browser öffnen:

- `http://localhost:4173/index.html`
- `http://localhost:4173/globe-transparent.html`

> Hinweis: Bitte über einen lokalen Server öffnen (nicht per `file://`), damit das Verhalten in allen Browsern konsistent ist.

## In deine Seite einbauen

Du kannst den relevanten `<canvas>` + `<script>` Block aus einer der HTML-Dateien übernehmen.

Wenn du möchtest, passe ich dir im nächsten Schritt auch Marker, Farben, Rotationsgeschwindigkeit oder Größe exakt auf dein Branding an.
