================================================================================
MDHuntFishOutdoors — huntmaryland-site deployment
================================================================================

Live URL: https://davidstonko.github.io/huntmaryland-site/
Privacy Policy URL (App Store Connect): https://davidstonko.github.io/huntmaryland-site/privacy.html

================================================================================
REPOSITORY LAYOUT
================================================================================

  index.html                               Landing page (MDHuntFishOutdoors, 4 modes)
  privacy.html                             Privacy policy (V2.2.0-accurate)
  .well-known/apple-app-site-association   Universal Links AASA — REPO ROOT (required)
  docs/join/index.html                     Deer Camp invite landing page
  README_DEPLOY.txt                        This file

GitHub Pages must be configured to serve from the REPO ROOT (main branch, /).
Do NOT change it to /docs — that would break the AASA path Apple expects.

================================================================================
V2.2.0 DEPLOY — WHAT'S NEW (2026-04-18)
================================================================================

  1. Landing page rewritten for 4-mode MDHuntFishOutdoors branding
  2. Privacy policy rewritten to match V2.2.0 reality:
     - Declares the Render backend, opt-in analytics, username accounts
     - Lists Mapbox, Anthropic (AI), NOAA, Maryland DNR data flows
     - EXIF stripping, 30-day account deletion, 90-day analytics retention
  3. AASA moved from /docs/.well-known/ to /.well-known/ (site root)
  4. App Store link now points to real Apple ID 6761347484

================================================================================
TEAM ID — FILLED IN 2026-04-18 (BAFL96ZCUU)
================================================================================

.well-known/apple-app-site-association still has the placeholder BAFL96ZCUU.
You MUST replace it with your Apple Developer Team ID before Universal Links
will work.

  1. Find your Team ID:
     https://developer.apple.com/account -> Membership details -> Team ID
     (10-character alphanumeric, e.g., A1B2C3D4E5)

  2. Edit .well-known/apple-app-site-association and replace:
        "appID": "BAFL96ZCUU.com.davidstonko.huntmaryland"
     with:
        "appID": "YOURTEAMID.com.davidstonko.huntmaryland"

  3. Commit and push. Apple will pick up the change within an hour.

  4. Verify the file serves correctly (no redirect, correct MIME type):
        curl -I https://davidstonko.github.io/huntmaryland-site/.well-known/apple-app-site-association

     Expected: HTTP 200, Content-Type should be application/json or text/plain.

================================================================================
DEPLOY FLOW
================================================================================

From your Mac, in this folder:

  git add .
  git commit -m "V2.2.0 site update"
  git push

GitHub Pages rebuilds automatically in ~1 minute.

================================================================================
VERIFICATION CHECKLIST (POST-DEPLOY)
================================================================================

  [ ] Open https://davidstonko.github.io/huntmaryland-site/
      -> Shows MDHuntFishOutdoors branding, 4 mode cards, real stats

  [ ] Open https://davidstonko.github.io/huntmaryland-site/privacy.html
      -> Matches what you declared in App Store Connect privacy questionnaire

  [ ] curl https://davidstonko.github.io/huntmaryland-site/.well-known/apple-app-site-association
      -> Returns JSON with your real Team ID (not BAFL96ZCUU)

  [ ] Open https://davidstonko.github.io/huntmaryland-site/docs/join/?code=TESTCODE on iPhone
      -> Shows invite card with "TESTCODE" and working App Store button

================================================================================
FUTURE: CUSTOM DOMAIN (optional)
================================================================================

If you buy mdhuntfishoutdoors.com or similar:
  1. Add domain under Pages settings
  2. Add CNAME DNS record pointing to davidstonko.github.io
  3. GitHub handles HTTPS automatically
  4. Update all privacy.html and AASA URLs to the new domain

================================================================================
