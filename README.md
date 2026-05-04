# Timer

https://cldsouth.github.io/autotimer
Minimal countdown timer. Runs in the browser, installable as a PWA.

## Usage

- **Set duration** — type `MMSS` or `HHMMSS` and press Start
- **Tap / Space** — reset to full duration (blue flash)
- **⋯ button** — pause or change duration
- Timer auto-restarts when it hits zero (red flash)

## Install as PWA

Open the URL in Chrome or Brave → install icon in the address bar → runs fullscreen with no browser UI.

## Files

| File | Purpose |
|------|---------|
| `index.html` | App |
| `manifest.json` | PWA config |
| `sw.js` | Service worker (offline support) |

## Android / iOS paketi (Capacitor)

Bu repo, mobil paketleme için Capacitor yapılandırmasını içerir.

```bash
npm install
npx cap add android
npx cap add ios
npx cap sync
```

Açmak için:

```bash
npx cap open android
npx cap open ios
```
