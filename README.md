# Globe mit [cobe](https://github.com/shuding/cobe)

Ja — cobe ist hier direkt eingebaut.

## Dateien im Repo

- `index.html`: Standard-Globe als Startpunkt.
- `globe-transparent.html`: Transparente Variante (ideal für Embeds).

## Lokal testen

```bash
python3 -m http.server 4173
```

Dann im Browser öffnen:

- `http://localhost:4173/index.html`
- `http://localhost:4173/globe-transparent.html`

---

## In **Webflow** einfügen (ohne Build-Tools)

### Option A (empfohlen): Direkt per **Embed**-Element

1. In Webflow Designer auf deiner Seite ein **Embed**-Element hinzufügen.
2. Den folgenden Code komplett einfügen.
3. Veröffentlichen.

```html
<div style="position:relative;width:100%;max-width:620px;margin:0 auto;aspect-ratio:1/1;">
  <canvas id="globe-cobe" style="width:100%;height:100%;display:block;background:transparent;"></canvas>
</div>

<script src="https://cdn.jsdelivr.net/npm/cobe@0.6.1/dist/cobe.umd.min.js"></script>
<script>
  (() => {
    const canvas = document.getElementById('globe-cobe')
    if (!canvas || typeof createGlobe !== 'function') return

    const markers = [
      { location: [52.52, 13.405], size: 0.05 },
      { location: [48.137, 11.575], size: 0.04 },
      { location: [50.1109, 8.6821], size: 0.04 },
      { location: [53.5511, 9.9937], size: 0.04 },
      { location: [40.7128, -74.006], size: 0.05 },
      { location: [35.6762, 139.6503], size: 0.05 },
    ]

    let phi = 0
    let width = 0

    function resize() {
      width = canvas.offsetWidth
      canvas.width = width * window.devicePixelRatio
      canvas.height = width * window.devicePixelRatio
    }

    resize()
    window.addEventListener('resize', resize)

    createGlobe(canvas, {
      devicePixelRatio: window.devicePixelRatio,
      width: width * window.devicePixelRatio,
      height: width * window.devicePixelRatio,
      phi: 0,
      theta: 0.28,
      dark: 0,
      diffuse: 1.2,
      mapSamples: 16000,
      mapBrightness: 6,
      baseColor: [0.85, 0.9, 1.0],
      markerColor: [0.1, 0.4, 1.0],
      glowColor: [0.7, 0.85, 1.0],
      markers,
      onRender(state) {
        state.width = width * window.devicePixelRatio
        state.height = width * window.devicePixelRatio
        state.phi = phi
        phi += 0.004
      },
    })
  })()
</script>
```

### Option B: Seite-weit via **Page Settings**

- Falls du das Script lieber global laden willst, füge
  `<script src="https://cdn.jsdelivr.net/npm/cobe@0.6.1/dist/cobe.umd.min.js"></script>`
  in Webflow unter **Page Settings → Before `</body>`** ein.
- Im Embed bleibt dann nur noch `<canvas>` + Initialisierungs-Script.

## Häufige Probleme in Webflow

- **Nichts sichtbar:** Eltern-Container hat keine Höhe → `aspect-ratio:1/1` oder feste Höhe setzen.
- **Globus unscharf:** `canvas.width/height` nicht auf `devicePixelRatio` skaliert.
- **Script läuft nicht:** Prüfen, ob Code im Embed oder in `Before </body>` sitzt.
- **Mehrere Globen auf einer Seite:** Jede Canvas braucht eine eigene `id`.

Wenn du willst, passe ich dir den Embed-Code direkt für dein konkretes Webflow-Layout an (z. B. 100% Breite in einer bestimmten Section, langsamere Rotation, andere Marker/Farben).
