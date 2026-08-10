# Ride Check

A single-page web app that tells you whether it's a good day to ride your motorcycle — built around your own thresholds for temperature, wind, rain, ice, fog, and humidity, checked against your actual morning and evening commute windows.

No backend, no accounts, no build step. It's one HTML file that runs entirely in the browser.

## Features

**Commute-aware forecasting**
- Set a home location and an optional work location; morning conditions are checked at home, evening conditions at work (or home, if you didn't set one).
- Configurable commute time windows, with weekends and manually-marked days off automatically skipped.
- A "free ride" check for spontaneous, no-destination rides using the next few hours at your home location.

**Your thresholds, your call**
- Temperature range, max sustained wind, max gust, rain, thunderstorms, snow, ice risk, fog/visibility, and humidity are all individually configurable — each with its own on/off toggle.
- Optional "avoid riding in the dark" check using real sunrise/sunset times, with a darkness gradient overlay on the hourly views.
- Option to hide overnight hours (11pm–5am) from every view.

**Daily and weekly views**
- Hour-by-hour breakdown for the current day, with a ride score, gear suggestions (jacket/gloves) based on the temperature window, and a plain-language summary.
- A 7-day week view with a "best day this week" banner, today highlighted, and a clear "Day Off" vs "Weekend" distinction.
- A "vs yesterday" comparison on today's view, using yesterday's actual recorded weather (not just today's forecast).
- Swipe left/right on the Daily view to move between days.

**Severe weather alerts**
- Active National Weather Service alerts (advisories, warnings) for your home and work locations, shown separately from your personal condition thresholds. US-only; fails quietly elsewhere.

**Ride log**
- Log a ride for the morning and/or evening leg of each day. Logging a morning ride auto-checks the evening leg too (same bike, same day), but either can be corrected independently for one-way days.
- Tracks total days ridden, mornings, evenings, and your current consecutive-commute-day streak (weekends and days off don't break it).

**Built for actually using it**
- Larger text and icons throughout for readability.
- Manual refresh button plus auto-refresh every 30 minutes while the app is open.
- Caches the last successful forecast locally, so the app still shows (clearly marked stale) data if you open it with no signal.
- "Add to Home Screen" ready on iOS — meta tags are set up so it launches full-screen like a native app.
- All preferences, locations, and ride history are stored in the browser's local storage. Nothing is sent to a server except the weather/alerts API calls.

## Tech stack

- Plain HTML + [React](https://react.dev/) and [Babel Standalone](https://babeljs.io/docs/babel-standalone), both loaded from CDN — no build tooling, no `npm install`.
- Weather data from the [Open-Meteo](https://open-meteo.com/) API (no key required).
- Severe weather alerts from the [National Weather Service API](https://www.weather.gov/documentation/services-web-api) (no key required, US only).

## Running it

There's nothing to build. Any static host works:

```bash
# Locally
python3 -m http.server 8000
# then open http://localhost:8000

# Or just open index.html directly in a browser
```

To host it for free with GitHub Pages: push this repo, then enable Pages in the repo settings (Settings → Pages → Deploy from branch → main / root). The app will be available at `https://<username>.github.io/<repo-name>/`.

## Roadmap

- Native iOS app (Swift) port, using this as the reference implementation for the ride-check logic.

## Privacy

Ride Check doesn't have a backend and doesn't collect anything. Your locations, preferences, and ride log live only in your browser's local storage. The only network calls are to Open-Meteo (forecast) and the National Weather Service (alerts), using your saved coordinates.
