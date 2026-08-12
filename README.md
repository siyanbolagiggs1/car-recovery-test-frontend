# Car Recovery — Customer Tracking Map

Customer-facing live map for the [car-recovery-backend](../car-recovery-backend) location-sharing
feature. The real production app already owns driver signup/login/share (its own screens, not
this repo) — this repo is just the one piece it was missing: the page a customer lands on to watch
the driver's live position. See `car-recovery-backend/README.md` for the full project status,
architecture, deployed URLs, and API reference.

**Deployed:** `https://car-recovery-test-frontend.onrender.com` (Render Static Site)

## Pages

- `track.html` — customer-facing live map (Leaflet/OpenStreetMap), reads `?token=` and optional
  `?backend=` query params, no login required. On load, grabs the customer's own browser location
  (`enableHighAccuracy: true`) and posts it to the backend as the ETA destination. Renders the
  driver as a 🚗 marker and the destination as a 📍 marker, draws the OSRM-computed route as a blue
  polyline, and fits the map to both markers on first load (not just a tight zoom on the driver) so
  the destination pin doesn't end up outside the visible viewport. Shows the ETA in the status pill
  when present — absent if no destination is set yet, or if the location falls outside the
  backend's OSRM coverage area.

## Run locally

```
python -m http.server 5500
```
Then open `http://localhost:5500/track.html?token=...`. No build step — plain static HTML/JS.

## Notes

- Points at the deployed backend (`https://car-recovery-backend.onrender.com`) by default,
  editable via the `?backend=` query param.
- `_redirects` still has a Render rewrite rule for the old path-style link (`/track/{token}`);
  per `car-recovery-backend`'s README that style proved unreliable on Render and was abandoned in
  favor of the query-param style (`track.html?token=...`) this page actually expects — the rule is
  effectively dead and can be deleted whenever this repo gets cleaned up further.
- Previously this repo also held `index.html`/`signup.html`/`login.html`/`driver.html` as a
  reference implementation of the driver-side flow. Those were removed — the real production app
  already implements driver signup/login/share itself; `track.html` was the only piece it needed
  from here. If you need to see how the driver side was reference-implemented, check this repo's
  git history before this commit.
