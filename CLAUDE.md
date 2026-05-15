# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Running the Site

This is a zero-build project — open `index.html` directly in a browser, or serve it with Python:

```powershell
python -m http.server 8080
```

Then visit `http://localhost:8080`. There is no build step, no package.json, and no framework.

## Architecture

The entire application lives in a single `index.html` file (~1400 lines). It is structured in three contiguous blocks:

1. **`<style>`** — all CSS, using CSS custom properties (`--gold`, `--dark`, `--white`, etc.) defined on `:root`
2. **HTML body** — static nav + footer; all dynamic content (city cards, guides, modal) is injected by JS at page load
3. **`<script>`** — all application logic, with no external JS dependencies

### Data layer (top of `<script>`)

Three constant objects drive all dynamic content:

| Constant | Purpose |
|---|---|
| `CITIES` | Array of 12 city objects — each has `name`, `country`, `heroImage`, `itinerary`, `food`, `transport`, `costBreakdown`, `safetyTips`, `photoSpots` |
| `WEATHER_DATA` | Object keyed by city name with typical climate stats |
| `FX` | Indicative exchange rates vs USD for the currency converter |
| `PACKING` | Object of categorized arrays for the packing checklist |

**To add a new destination:** add an entry to `CITIES` with all required fields; it auto-renders in city cards, dropdowns, and the budget calculator. To also show it in the `#guides` featured strip, add its index to the `featured` array in `renderGuides()` (line ~1345).

### Page sections

All sections are anchor-linked (`#home`, `#guides`, `#cities`, `#tools`, `#weather`, `#safety`, `#enquiry`). Content for `#guides` and `#cities` is DOM-injected by `renderGuides()` and `renderCities()` on init.

### Modal

`openModal(idx)` receives a `CITIES` index and dynamically builds 7 tabs (Overview, Itinerary, Food, Transport, Costs, Safety, Photo Spots) from the city object. The modal is a single reusable `<div id="modalBackdrop">` in the HTML.

### Persistence

Three `localStorage` keys are used — no backend:

| Key | Used by |
|---|---|
| `packingChecklist` | Checkbox state across sessions |
| `itineraryEntries` | User-built itinerary entries |
| `travelEnquiries` | Submitted enquiry form data |

Enquiry forms do **not** send data to a server; they only save to `localStorage` and show a success banner.

### Currency converter

Rates in `FX` are hardcoded vs USD. To update rates, edit the `FX` object directly — the converter uses cross-multiplication through USD.
