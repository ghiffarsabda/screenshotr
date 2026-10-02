# screenshotr

A Chrome extension that turns any webpage or web app into a **high-quality SVG screenshot**.

Instead of a flat PNG, screenshotr captures the rendered page and produces a resolution-independent SVG you can zoom into forever, embed on a retina site, drop into a design doc, or print without pixelation.

## Why SVG

Raster screenshots break down the moment you scale them. SVG screenshots stay crisp at any zoom, stay small when the page is mostly flat color and text, and are trivial to post-process — recolor, annotate, or diff as plain text.

## Features

- **Vector output** — exports `.svg`, not `.png`.
- **Full-page capture** — grabs the entire scrollable page, not just the viewport.
- **Region select** — drag to capture a single element or a custom area.
- **High fidelity** — preserves layout, gradients, borders, shadows, and web fonts.
- **Text stays text** — copyable, searchable, and selectable in the exported file.
- **One-click copy** — copy the SVG markup or download the file.
- **No server** — everything runs locally in the browser; nothing is uploaded.

## Install (development)

1. Clone the repo:
   ```bash
   git clone https://github.com/ghiffarsabda/screenshotr.git
   cd screenshotr
   ```
2. Open `chrome://extensions` in Chrome.
3. Enable **Developer mode** (top right).
4. Click **Load unpacked** and select this folder.

## Usage

1. Open the page you want to capture.
2. Click the screenshotr icon in the toolbar.
3. Choose **Full page** or **Select region**.
4. Preview the result, then **Download SVG** or **Copy SVG**.

## How it works

1. A content script measures the page and serializes the rendered DOM.
2. Computed styles are inlined so the output does not depend on external CSS.
3. DOM nodes, text, borders, and gradients are mapped to SVG primitives.
4. Raster-only assets (images, canvas, video frames) are embedded as base64 inside `<image>` tags.
5. The assembled SVG is offered for download or clipboard copy.

Everything happens client-side in an isolated extension context — no network calls, no telemetry.

## Project structure

```
screenshotr/
├── manifest.json      # Extension manifest (MV3)
├── src/
│   ├── background/    # Service worker
│   ├── content/       # DOM capture + serialization
│   ├── popup/         # Toolbar UI
│   └── export/        # DOM -> SVG conversion
├── assets/            # Icons and styles
└── README.md
```

## Roadmap

- [ ] Full-page capture
- [ ] Region / element selection
- [ ] Text preserved as vector `<text>`
- [ ] Copy-to-clipboard
- [ ] Optional PNG fallback

## Contributing

Issues and pull requests are welcome. Keep changes small and focused.

## License

MIT
