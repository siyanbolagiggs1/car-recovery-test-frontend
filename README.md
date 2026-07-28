# Car Recovery — Test Frontend

Reference/test frontend for the [car-recovery-backend](../car-recovery-backend) API — a
driver location-sharing feature for a car recovery company's website. **This is not the
real production frontend**; it exists to exercise and demo the backend. See
`car-recovery-backend/README.md` for the full project status, architecture, deployed
URLs, and API reference — this file only covers what's specific to this repo.

**Deployed:** `https://car-recovery-test-frontend.onrender.com` (Render Static Site)

## Pages

- `index.html` — nav hub linking the pages below
- `signup.html` / `login.html` — create/retrieve a driver `api_key`; on success, saves it to `localStorage` and auto-redirects to `driver.html`
- `driver.html` — pre-fills the saved API key and backend URL; share/stop location, shows the live shareable tracking link
- `track.html` — customer-facing live map (Leaflet/OpenStreetMap), reads `?token=` and optional `?backend=` query params, no login required

## Run locally

```
python -m http.server 5500
```
Then open `http://localhost:5500/`. No build step — plain static HTML/JS.

## Notes

- Pages point at the deployed backend (`https://car-recovery-backend.onrender.com`) by default, editable via the "Backend URL" field on each page.
- A Render "Redirects/Rewrites" rule was tried to make `/track/{token}` (the raw path-style link the backend's API returns) resolve directly here; it proved unreliable on Render and was abandoned — the working link is always the query-param style (`track.html?token=...`) that `driver.html` actually displays.
