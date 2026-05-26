# sknauss7.github.io

User-pages site for Kynoss Studios. Hosts Apple App Site Association
(`apple-app-site-association`) for Universal Link resolution across
the Kynoss apps.

## Contents

- **`apple-app-site-association`** — Apple AASA file. iOS reads this
  at `https://sknauss7.github.io/apple-app-site-association` (no
  extension, served as JSON) when an app installed on the device
  declares the `applinks:sknauss7.github.io` entitlement. The file
  lists every Kynoss app's bundle ID + the URL path components that
  app handles.

## Adding a new app

1. Update the `appIDs` array on the existing details block OR add a
   new details block if the app handles a distinct path prefix.
2. Each app's `components` array lists URL paths it claims. iOS
   matches longest-prefix.
3. Commit + push to `main`. GitHub Pages picks up the change in
   ~30 seconds.

## Verify

```bash
# Should return 200 + the JSON body, no redirect.
curl -I https://sknauss7.github.io/apple-app-site-association
curl https://sknauss7.github.io/apple-app-site-association | jq .

# Apple's swcutil should accept it without warnings on a real device.
sudo swcutil verify -d sknauss7.github.io
```

The path-component fallback HTML (shown when an iOS device taps the
Universal Link without the app installed) lives in the per-app
support repo (e.g. `KynossStudiosSupport`), not here.

## Current apps

- **Rusti** (`KynossStudios.Rusti`) — Sprint 5b open-link Challenge
  Mode invitations under `/KynossStudiosSupport/rusti/challenge/*`.
  Fallback HTML at `https://sknauss7.github.io/KynossStudiosSupport/rusti/challenge/index.html`.
