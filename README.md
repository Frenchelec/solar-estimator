# Solar Estimator — App Deployment & Install Guide

One codebase, installs everywhere: iPhone, Android, and desktop (Chrome/Edge). Works fully offline once installed — no signal needed on site.

## Files

```
solar-estimator-app/
├── index.html            the app (all logic inside)
├── manifest.webmanifest  makes it installable
├── sw.js                 offline cache (service worker)
├── icons/                app icons (home screen / desktop)
└── README.md             this guide
```

## Step 1 — Host it (one-off, ~5 minutes)

Installable apps must be served over **HTTPS**. Easiest free options:

**Netlify Drop (recommended, no account setup needed beyond signup):**
1. Go to https://app.netlify.com/drop
2. Drag the whole `solar-estimator-app` folder onto the page
3. You get a URL like `https://french-solar.netlify.app` — that's your app address. You can rename the site in Site settings.

**Alternatives:** Cloudflare Pages or GitHub Pages work the same way (upload the folder, get an HTTPS URL).

Send the URL to your staff — that's the whole rollout.

## Step 2 — Staff install the app

**iPhone / iPad (field staff):**
1. Open the URL in **Safari**
2. Tap the **Share** button (square with arrow)
3. Tap **Add to Home Screen** → **Add**
4. A "Solar Quote" icon appears — opens full-screen like a native app, works offline

(The app shows this hint automatically the first time it's opened on an iPhone.)

**Android (field staff):**
1. Open the URL in **Chrome**
2. Tap the **Install** button in the app header (or Chrome menu → *Add to Home screen / Install app*)

**Desktop (estimators):**
1. Open the URL in **Chrome** or **Edge**
2. Click the **install icon** in the address bar (monitor with down-arrow), or the **Install** button in the app header
3. It opens in its own window and appears in the Start menu / Dock

## Updating the app later

1. Edit `index.html` (rates, defaults, etc.)
2. In `sw.js`, bump the version: `solar-estimator-v1` → `solar-estimator-v2`
3. Re-upload the folder to your host
4. Staff get the update automatically next time they open the app with internet (may take one extra open)

## Field-use notes

- **Quotes survive interruptions** — inputs are saved on-device automatically; taking a phone call or switching apps won't lose the quote. Use **Reset to defaults** to start fresh.
- **Share summary** (phones) opens the native share sheet — text or email the quote to the customer on the spot.
- **Print / Save PDF** is for desktop/browser use (hidden in the installed iPhone app, where iOS doesn't support printing — use Share instead).
- **Sun/moon button** toggles light mode — much more readable in direct sunlight.

## Key defaults (July 2026, all editable in-app)

- Electricity import: $0.38/kWh (NZ avg ~40.6c incl GST, MBIE Feb 2026)
- Buyback: $0.10/kWh (market range 8–23c)
- Battery: $1,050/kWh ex GST (market avg ~$1,219 incl GST)
- Single-phase warning now triggers at >5 kW (many EDBs cap single-phase export at 5 kW/phase — check your local network)
- $/W tiers are ex GST; the residential 12 kW+ tier ($1.65/W ex = ~$1.90 incl) is ~30% above the April 2026 market average ($1.42/W incl) — review for competitiveness on large jobs. Edit tiers in `index.html`, function `suggestPerW()`.
