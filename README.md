# Star Wars Random Facts — Collibra Dashboard Widget

A self-contained single-file web application that demonstrates how to embed custom **HTML**, **CSS**, and **JavaScript** inside a [Collibra](https://www.collibra.com) Dashboard widget.

---

## What it does

Fetches a random entry from the public [SWAPI](https://swapi.info) (Star Wars API) on every page load and lets the user cycle through additional random facts with a button click. The displayed fact can come from any of six categories: Films, People, Planets, Species, Starships, or Vehicles.

| Feature | Details |
|---|---|
| Random on load | Picks a random category and item automatically |
| Next fact button | Fetches another random entry on demand |
| Dark / Light theme | Toggle between space-black and warm-parchment palettes |
| Animated starfield | Canvas-based perspective warp — active in dark mode only |
| Responsive layout | Fixed viewport height; fact card scrolls internally |
| Response caching | Each category list is fetched once per session |

---

## Embedding in a Collibra Dashboard

Collibra Dashboards support an **HTML widget** that accepts arbitrary HTML markup. Because the widget renders inside an `<iframe>`, a fully self-contained file — with all styles and scripts inlined — works without any external hosting.

### Step-by-step

1. **Open** your Collibra instance and navigate to a Dashboard (or create a new one).
2. **Add widget** → choose **Embed Widget** from the widget picker.
3. **Open the widget configuration editor** (/resources/images/PATH-TO-FILE-swapi.html).
4. **Save** the widget. The app renders immediately inside the dashboard tile.

### Tips

- **Sizing** — The layout uses `height: 100vh`, so it fills whatever height the widget frame is given. Drag the widget border to resize; the card reflows automatically.
- **No backend required** — All API calls go directly from the browser to `https://swapi.info`. No Collibra server-side configuration is needed.
- **CORS** — `swapi.info` returns permissive CORS headers, so browser fetch requests work without a proxy.
- **Content Security Policy** — If your Collibra instance enforces a strict CSP, you may need to add `https://swapi.info` to the `connect-src` allowlist via your platform or network configuration.

---

## Local development

Open the file directly in a browser — no build step, no dependencies, no server required:

```bash
# Any of these work:
open swapi.html
xdg-open swapi.html
python3 -m http.server 8080   # then visit http://localhost:8080/swapi.html
```

---

## API reference

Data is sourced from [swapi.info](https://swapi.info) — a free, open, read-only Star Wars API.

| Endpoint | Content |
|---|---|
| `/api/films` | All six episodic films with opening crawl text |
| `/api/people` | Characters with physical attributes and film appearances |
| `/api/planets` | Worlds with climate, terrain, population, and orbital data |
| `/api/species` | Species classification, language, lifespan, and coloring |
| `/api/starships` | Vessel specs: crew, hyperdrive, cost, cargo capacity |
| `/api/vehicles` | Ground and air vehicles with comparable stats |

---

## Collibra Dashboard — HTML widget overview

The HTML widget is the primary escape hatch for custom UI inside Collibra Dashboards. Key characteristics:

- Renders in a sandboxed `<iframe>` — full DOM isolation from the host page.
- Supports inline `<style>` and `<script>` blocks as well as `<link>` and `<script src>` tags pointing to external CDN resources.
- Can read the Collibra REST API using `fetch()` with the session cookie forwarded by the browser (same-origin), enabling widgets that display live Collibra data alongside third-party content.
- Widget content is stored in the Dashboard configuration and travels with the Dashboard when exported/imported.

---

## File structure

```
swapi/
└── swapi.html    # Single self-contained application
```

All HTML, CSS, and JavaScript live in one file for maximum portability inside the Collibra widget editor.

---

## License

This project is provided as a reference example. The Star Wars data is served by [swapi.info](https://swapi.info) under their terms of use. Star Wars is a trademark of Lucasfilm Ltd.
