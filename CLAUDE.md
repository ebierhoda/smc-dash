# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

`smc-dash` is a static digital signage dashboard for the Strand Moslem Council (SMC) Jaamia Masjid community center. It displays prayer times, announcements, donations, expense stats, and community impact metrics on a rotating carousel.

## Running Locally

No build process — open `index.html` directly in a browser, or serve it with any static file server:

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

Deployment is via Vercel (static hosting). `vercel.json` sets `Cache-Control: no-store` on all routes.

## Architecture

The entire application lives in a single file: **`index.html`** (~22KB, embedded CSS + JS).

### Layout

- **Sidebar (400px)**: SMC logo, live clock/date, daily prayer times, alert banner
- **Main area**: 4-slide auto-rotating carousel (20s interval), with manual tab navigation and progress dots

### Carousel Slides

1. **Announcements** — upcoming community events
2. **Donations** — Ablution Project fundraising progress bar
3. **Stats** — monthly expense breakdown (Chart.js doughnut chart)
4. **Community** — Zakat impact metrics

### Data

All data is hardcoded as JSON inside a `<script type="application/json" id="dashboard-data">` block within `index.html`. This includes:

- 12 months of prayer times (used to compute next prayer dynamically)
- Events list
- Donation totals (`raised` / `goal`)
- Monthly expense categories

### Key Runtime Behaviors

- Clock updates every second (12-hour format)
- Prayer times are dynamically selected based on the current date and time
- Chart.js renders the expense doughnut on the Stats slide
- The layout is designed for 1920×1080 displays and uses CSS `transform: scale()` to fit other resolutions

### Dependencies (all via CDN)

- Tailwind CSS
- Chart.js 4.4.0
- Google Fonts: Inter
- Material Symbols Outlined (icons)
