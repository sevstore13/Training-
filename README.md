# Training Log — PWA

A self-contained, installable workout tracker. Upper/Lower 4-day split with auto-progression,
plate calculator, exercise swaps, RPE logging, deload reminders, bodyweight + volume charts.
All data is saved on your device (no account, no server).

## Files
- `index.html` — the entire app
- `manifest.webmanifest` — install config (name, icon, fullscreen)
- `sw.js` — service worker (offline support)
- `icon-192.png`, `icon-512.png`, `icon-512-maskable.png` — app icons

## Run it locally (test)
A service worker needs to be served over http(s), not opened as a `file://`. From this folder:

    python3 -m http.server 8080

Then open `http://localhost:8080` in your phone's browser (same Wi-Fi, use your computer's
local IP, e.g. `http://192.168.1.20:8080`).

## Put it online (free, ~5 min) — recommended
1. Go to https://app.netlify.com/drop
2. Drag this whole folder onto the page.
3. You get a live URL like `https://your-name.netlify.app`. Done.

(Vercel, Cloudflare Pages, or GitHub Pages all work the same way.)

## Install on your phone
- **iPhone (Safari):** open the URL → Share → "Add to Home Screen."
- **Android (Chrome):** open the URL → menu (⋮) → "Install app" / "Add to Home Screen."

It then launches fullscreen with its own icon, like a native app, and works offline.

## Notes
- First load needs internet (it pulls React + Tailwind from a CDN, then caches them for offline use).
- Data lives in your browser's local storage. Clearing site data / "Erase all content" wipes it.
  If you reinstall to a new phone, the history does **not** transfer — that's the tradeoff of a
  no-account app. Cloud sync would require a backend (next step if you want it).
- This uses the Tailwind "Play CDN," which is fine for personal use. For a published/production app,
  rebuild with a real toolchain (Vite + Tailwind CLI) so styles are compiled, not generated at runtime.

## Turn it into an App Store / Play Store app later
Wrap this with **Capacitor** (`npm i @capacitor/core @capacitor/cli`, `npx cap init`, add iOS/Android
platforms, drop these files in `www/`). ~95% of the code carries over. You'll need an Apple Developer
account ($99/yr) and/or Google Play ($25 once). Only worth it if you plan to distribute it.
