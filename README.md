# Tanking App

Tanking App is a mobile-friendly Progressive Web App (PWA) with payload and fuel calculators, timers, a local flight log and an interactive caution and warning reference for the Bell 214B and 214ST. Rune Kyndal created the original application. This repository is Jeremy Whiting's maintenance fork. [Original project](https://github.com/RuneKyndal/tanking)

> **Aviation safety.** Use the app for familiarisation and as a secondary reference. For flight planning, loading, navigation and abnormal or emergency actions, use the approved Rotorcraft Flight Manual and applicable supplements for the specific aircraft, approved checklists, operator procedures and aircraft instruments. Presets, reserve values, warning colours and procedure text in the app are unverified for your operation.
>
> For U.S.-registered (N-rego) aircraft operating in Australia, follow the applicable FAA requirements and Australian flight rules. For Australian-registered (VH-rego) aircraft, follow the applicable CASA requirements. [FAA 14 CFR § 91.9 — flight manual and operating limitations](https://www.ecfr.gov/current/title-14/chapter-I/subchapter-F/part-91/subpart-A/section-91.9) · [FAA 14 CFR § 91.703 — U.S.-registered aircraft operating overseas](https://www.ecfr.gov/current/title-14/chapter-I/subchapter-F/part-91/subpart-H/section-91.703) · [CASA Part 91 — general operating and flight rules](https://www.casa.gov.au/rules/regulatory-framework/casr/part-91-casr-general-operating-and-flight-rules)

## Features

- **Useful payload.** Estimates remaining payload in pounds by subtracting empty aircraft weight, crew and gear, and entered fuel from the selected maximum gross weight. It performs no centre-of-gravity or loading-envelope check. **The payload display labelled “LITERS” applies a pounds-to-kilograms factor. Do not use it as a volume.**
- **Fuel estimates.** Shows estimated remaining fuel, total and reserve-adjusted endurance, range and time to bingo from entered fuel, selected burn rate, ground speed and distance. The flight view estimates fuel burn from elapsed time. The app’s fixed reserve is a calculation assumption. Check actual fuel with approved aircraft methods.
- **Refuel and Aeronet worksheets.** Refuel Calc estimates uplift or defuel and converts fuel mass to volume using an assumed Jet A density. Aeronet converts manually entered start and end quantities and totals up to five fuel receipts for manual entry elsewhere.
- **Flight timers and log.** Records engine and flight times with an aircraft registration, groups saved entries by date and exports CSV or plain text. Settings and saved logs live in the browser on that device. Export logs before clearing site data or moving to another browser, device or site address.
- **Device GPS and display.** With location permission and a usable fix, the flight view can show ground speed and point toward up to three temporary marked positions. Dark mode and screen wake lock are available where supported. The UH-60 button plays an Easter egg video.
- **Caution and warning panel.** Setup opens an interactive Bell 214B/214ST panel reference with a simulated lamp test and reference text. Use the approved checklist for any actual caution or warning. [Tanking App manual](manual.html) · [Panel manual](caution_manual.html)

## Run locally

Install Git and Python 3, then run these commands on your computer. The app is static HTML, CSS and JavaScript and runs without a build step or a backend.

```bash
git clone https://github.com/jezalinko/tanking-Rune-.git
cd tanking-Rune-
python3 -m http.server --bind localhost 8000
```

Open [http://localhost:8000/index.html](http://localhost:8000/index.html). Keep the server running while testing online and press **Ctrl+C** to stop it. Use the local server to test the service worker. For testing on another device, use an HTTPS deployment. [Service worker requirements](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API/Using_Service_Workers)

## Install on a phone or tablet

Open the app’s deployed HTTPS URL while online. Confirm the URL in the repository’s **Settings → Pages** if using GitHub Pages.

1. **iPhone or iPad.** In Safari, choose **Share → Add to Home Screen** and enable **Open as Web App** if shown.
2. **Android.** In Chrome, open the menu and choose **Install app** or **Add to Home screen → Install**, depending on the browser version.
3. Launch the installed app while online. Allow location access if you want to test GPS. Open the manual and caution panel, then disconnect and reopen the app and those pages to check that they load on your device.

## Offline use and updates

The service worker tries to cache the app and its bundled pages and assets on first load. For later requests it tries the network first and falls back to a cached copy when the request fails. A slow connection can delay loading. An uncached page or asset may be unavailable offline, and a browser can clear or evict cached files.

Use **Setup → Update App** with a reliable connection. It clears the offline cache and reloads from the server. Once it finishes, reopen the app and verify offline access again. [Service worker source](sw.js)

## Source layout

| File | Role |
| --- | --- |
| `index.html` | Main screens, inline styles and JavaScript for calculators, timers, logging, GPS, display and updates. |
| `manual.html` | In-app user guide. |
| `caution.html`, `caution_manual.html` | Interactive panel reference and its guide. |
| `manifest.json`, `tank.png` | Home screen launch settings and app icon. |
| `sw.js` | Service worker registration target and offline cache logic. |
| `rickroll.mp4` | Video for the UH-60 button. |
| `CNAME` | Inherited GitHub Pages custom-domain entry. Check it against the fork’s Pages settings before publishing. |

## Maintenance and attribution

Keep Rune Kyndal’s attribution and Git history intact. Make changes on a branch, review the diff, test locally and use a pull request into the fork’s `main` branch. Before releasing changes to calculations, warnings or procedure text, have them independently checked against the approved documents for the applicable aircraft and operation.

The reviewed upstream and fork trees contain no separate license file. The original manual invites forks and modifications. Check the applicable permissions before redistributing the app or its bundled material. [Original repository](https://github.com/RuneKyndal/tanking) · [Original manual source](https://github.com/RuneKyndal/tanking/blob/main/manual.html)

*In memory of Rune. Thanks for the code and the laughs.*