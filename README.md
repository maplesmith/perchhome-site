# perchhome-site

Redirect-only site for `perchhome.app`, published with GitHub Pages.

Perch Home's landing, privacy, terms, and support pages moved to
[maplesmith.dev/perch-home](https://maplesmith.dev/perch-home/) so that one site serves the whole
app family instead of a domain per app (maplesmith/perchhome#349). This repository now holds four
redirect stubs at the original paths:

| Old path   | New location                                  |
| ---------- | --------------------------------------------- |
| `/`        | `https://maplesmith.dev/perch-home/`          |
| `/privacy` | `https://maplesmith.dev/perch-home/privacy/`  |
| `/terms`   | `https://maplesmith.dev/perch-home/terms/`    |
| `/support` | `https://maplesmith.dev/perch-home/support/`  |

## Why stubs rather than a real redirect

GitHub Pages serves static files and cannot issue a 301. Each stub uses `<meta http-equiv="refresh">`
with a `rel="canonical"` link and a `location.replace()` fallback, and renders a readable page with a
visible link if both fail. That matters most for `/privacy`: Apple re-checks the privacy policy URL
on the live App Store listing, and a 404 there is a review problem.

## Do not retire this domain yet

Two independent reasons, either one sufficient:

1. **The backend still lives here.** Perch Home's production backend is `https://api.perchhome.app`
   (see `EXPO_PUBLIC_BACKEND_BASE_URL` in the app repo). That subdomain is not part of the site
   move, so the registration has to persist for as long as the backend uses the hostname,
   regardless of anything below. Retiring the domain would take a backend and App Attest change
   first.
2. **Old builds request these paths.** `https://perchhome.app/privacy` is compiled into every
   Perch Home build already in the wild, and those installs keep requesting it indefinitely. Apple
   also re-checks the privacy URL on the live listing.

So keep `perchhome.app` registered and these stubs published. Moving to a real 301 later means
moving the domain off GitHub Pages to a host that can serve redirects.

The files under `assets/` are no longer referenced by any page here. They are kept rather than
deleted in case anything external still links to them.
