# Class Schedule

A small, dependency-free Progressive Web App for viewing a weekly class schedule. It is designed to be quick to load, installable, and usable offline after the app shell has been cached.

## Features

- List and timetable views for Monday through Friday
- Current and next class indicators based on the device's local time
- Subject highlighting from the legend
- Responsive layout for desktop and mobile screens
- Persistent view preference using `localStorage`
- Install prompt when the browser supports PWA installation
- Full timetable view with image export
- Service-worker caching for offline use

## Project structure

- `index.html` - application markup, styles, schedule data, and browser logic
- `manifest.webmanifest` - PWA metadata and icons
- `sw.js` - app-shell and runtime caching
- `icons/` - application icons
- `wrangler.jsonc` - Cloudflare Pages configuration

## Run locally

Because the service worker requires a secure context, use a local HTTP server rather than opening `index.html` directly. For example, with Python installed:

```powershell
py -m http.server 8080
```

Open <http://localhost:8080> in a browser. A recent Chromium, Firefox, or Safari browser is recommended.

## Update the schedule

Edit the `SUBJECTS` and `DATA` constants in the inline script in `index.html`.

- Times are represented as minutes after midnight. For example, `9:30 AM` is `570`.
- `day` uses `1` for Monday through `5` for Friday.
- Each event needs `start`, `end`, `code`, and `room` values.
- Add a subject definition before referencing its code in `DATA`.

If the cached version does not update during local testing, unregister the service worker from the browser's developer tools or change `CACHE_NAME` in `sw.js`.

## Deploy to Cloudflare Pages

Authenticate Wrangler once if needed, then deploy the repository root:

```powershell
npx wrangler login
npx wrangler pages deploy .
```

`wrangler.jsonc` configures the current directory as the Pages build output directory. There is no build step or package installation required.

## License

No license has been specified for this project yet.
