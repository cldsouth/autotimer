# AutoTimer

[**Live Web Version (PWA)**](https://cldsouth.github.io/autotimer/assets/)

Minimal countdown timer. Runs in the browser, installable as a PWA, and available as a native Android app.

## 🚀 Usage

- **Set duration** — type `MMSS` or `HHMMSS` and press Start.
- **Tap / Space** — reset to full duration (blue flash).
- **⋯ button** — pause or change duration.
- **Auto-restart** — Timer auto-restarts when it hits zero (red flash).

## 📥 Installation

### Web (PWA)
Open the URL in a modern browser (Chrome, Brave, Safari) and select "Add to Home Screen" or "Install App". It runs fullscreen and supports offline usage.

### Android
Download the latest signed APK from the [GitHub Releases](https://github.com/cldsouth/autotimer/releases) page.

---

## 🛠 Development & Native Builds (Capacitor)

This repository includes a Capacitor scaffold for mobile packaging.

### Setup
```bash
npm install
npx cap sync
```

### Android Build & Release
To generate a signed production build:

1.  Ensure your `release-key.jks` is in the `android/app/` directory.
2.  Add your signing credentials to `android/local.properties` (this file is git-ignored for security):
    ```properties
    MYAPP_RELEASE_STORE_FILE=release-key.jks
    MYAPP_RELEASE_STORE_PASSWORD=your_password
    MYAPP_RELEASE_KEY_ALIAS=your_alias
    MYAPP_RELEASE_KEY_PASSWORD=your_password
    ```
3.  Run the build command:
    ```bash
    cd android
    ./gradlew assembleRelease
    ```

The signed APK will be generated at `android/app/build/outputs/apk/release/app-release.apk`.

---

## 📂 File Structure

| File / Folder | Purpose |
|---------------|---------|
| `assets/` | Web application source (HTML, CSS, JS) |
| `android/` | Native Android project (API 37) |
| `manifest.json` | PWA configuration |
| `sw.js` | Service Worker for offline support |
| `capacitor.config.json`| Capacitor bridge settings |

---
*Maintained by [cldsouth](https://github.com/cldsouth)*
