# AGENTS.md

## Project overview

This is a dependency-free static PWA. The application is intentionally kept small: `index.html` contains the UI, CSS, schedule data, and client-side behavior; `manifest.webmanifest` describes the installable app; `sw.js` handles caching; and Cloudflare Pages serves the repository root.

## Working conventions

- Keep the app vanilla HTML, CSS, and JavaScript unless a task explicitly requires a new dependency.
- Preserve the existing IBM Plex Sans and IBM Plex Mono typography, theme variables, responsive behavior, and accessible button semantics.
- Keep schedule data in the `SUBJECTS` and `DATA` constants in `index.html`.
- Use minutes after midnight for event times and Monday-Friday day indexes (`1`-`5`).
- Keep cache entries and `CACHE_NAME` in `sw.js` synchronized when adding or renaming app-shell files.
- Use relative paths so the app works from a Cloudflare Pages deployment and a local static server.
- Avoid unrelated formatting or refactoring in the single-file application.

## Validation

There is no build system or automated test suite. Before completing a change:

1. Serve the repository with `py -m http.server 8080` or another static HTTP server.
2. Open the app in a browser and check both list and timetable views.
3. Check the browser console for errors.
4. When changing the PWA shell, verify service-worker registration and a reload while offline.
5. For schedule changes, check the affected day, current/next status, and timetable layout.

## Deployment

Cloudflare Pages deploys the repository root with:

```powershell
npx wrangler pages deploy .
```

Do not commit generated Wrangler output, credentials, or local browser data.
