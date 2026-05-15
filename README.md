# Travel Explorer

> We went, so you know where to go.

A single-page travel guide featuring curated city cards, detailed destination guides, a budget calculator, packing checklist, weather reference, and currency converter — all in pure HTML/CSS/JS with no build step or dependencies.

**[Live Site](https://jyeong7913.github.io/claude1/)**

![Travel Explorer Preview](screenshot.png)

---

## Features

- **City cards** — 12 destinations with hero images, country badges, and at-a-glance summaries
- **Destination modal** — 7-tab detail view per city: Overview, Itinerary, Food, Transport, Costs, Safety, Photo Spots
- **Featured guides strip** — curated highlight cards on the dark-background section
- **Budget calculator** — per-city cost breakdown with adjustable trip length
- **Currency converter** — cross-rate conversion through USD for all featured destinations
- **Weather reference** — typical monthly climate stats by city
- **Packing checklist** — categorised checklist that persists across browser sessions via `localStorage`
- **Trip planner** — user-built itinerary entries saved to `localStorage`
- **Enquiry form** — contact form that saves submissions locally (no backend)
- **Responsive layout** — mobile hamburger nav, fluid grid cards, smooth-scroll anchors

---

## Tech Stack

| Layer | Choice |
|---|---|
| Markup | Plain HTML5 |
| Styling | Vanilla CSS with custom properties |
| Logic | Vanilla JavaScript (ES6+), no frameworks |
| Fonts | Google Fonts (Playfair Display + Inter) via CDN |
| Images | Unsplash CDN URLs |
| Persistence | `localStorage` only — no backend |
| Build | None — zero build step |

---

## Running Locally

```bash
python -m http.server 8080
```

Then open `http://localhost:8080` in your browser. You can also open `index.html` directly as a file.

---

## Project Structure

The entire application is a single file:

```
index.html                (~1400 lines, three contiguous blocks)
  <style>                 All CSS; custom properties on :root
  <body>                  Static nav + footer; dynamic content injected by JS
  <script>                All application logic; no external JS deps
```

### Data layer (top of `<script>`)

| Constant | Purpose |
|---|---|
| `CITIES` | Array of 12 city objects with `name`, `country`, `heroImage`, `itinerary`, `food`, `transport`, `costBreakdown`, `safetyTips`, `photoSpots` |
| `WEATHER_DATA` | Typical climate stats keyed by city name |
| `FX` | Indicative exchange rates vs USD |
| `PACKING` | Categorised arrays for the packing checklist |

### Page sections

All sections are anchor-linked: `#home`, `#guides`, `#cities`, `#tools`, `#weather`, `#safety`, `#enquiry`.

---

## Adding a New Destination

1. Add an entry to the `CITIES` array in `index.html` with all required fields — it auto-renders in city cards, dropdowns, and the budget calculator.
2. To also feature it in the guides strip, add its index to the `featured` array in `renderGuides()`.

---

## Deployment

Pushes to `main` automatically deploy to GitHub Pages via the workflow at [`.github/workflows/deploy.yml`](.github/workflows/deploy.yml).

---

## License

MIT
