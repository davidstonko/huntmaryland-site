================================================================================
MDHuntFishOutdoors — huntmaryland-site deployment
================================================================================

Live URL: https://davidstonko.github.io/huntmaryland-site/
Privacy Policy URL (App Store Connect): https://davidstonko.github.io/huntmaryland-site/privacy.html

================================================================================
REPOSITORY LAYOUT
================================================================================

  index.html                               Landing page (MDHuntFishOutdoors, 4 modes)
  privacy.html                             Privacy policy (V2.4.0-accurate, effective 2026-06-10)
  404.html                                 Invite-link fallback for /join/CODE + /trip/CODE
                                           (also doubles as the site 404 page)
  .well-known/apple-app-site-association   Universal Links AASA — REPO ROOT (required)
  docs/join/index.html                     Legacy ?code= invite landing page
  README_DEPLOY.txt                        This file

GitHub Pages must be configured to serve from the REPO ROOT (main branch, /).
Do NOT change it to /docs — that would break the AASA path Apple expects.

================================================================================
V2.4.0 DEPLOY — WHAT'S NEW (2026-06-10)
================================================================================

  1. AASA replaced with the canonical V2.4 version from
     huntmaryland-build/website/.well-known/ — modern appIDs+components
     format, team BAFL96ZCUU, paths:
       /huntmaryland-site/join/*   (Deer Camp / Honey Hole / Group Camp invites)
       /huntmaryland-site/trip/*   (Camp Trip invites)
       /join/*                     (short-form future-compat)
     The previously deployed AASA used the legacy "paths" format with
     /join* ONLY — it did NOT match the /huntmaryland-site/join/CODE
     URLs the app actually generates, so Universal Links were broken
     in production until this deploy.
  2. privacy.html updated to V2.4.0 (Sentry active w/ PII off,
     analytics inactive, EXIF stripping) — contact email switched to
     feedback.mdhuntfishoutdoors@gmail.com.
  3. NEW 404.html — when an invite recipient WITHOUT the app taps a
     path-style invite link, GitHub Pages serves 404.html; it parses
     the code from the path and renders the invite card + App Store
     button. With the app installed, iOS opens the app directly and
     this page is never seen.

CANONICAL SOURCE: the AASA file's source of truth is
huntmaryland-build/website/.well-known/apple-app-site-association.
Never hand-edit the copy here — re-copy from the canonical repo.

================================================================================
DEPLOY FLOW
================================================================================

From your Mac, in this folder (~/Code/huntmaryland-site):

  git add .
  git commit -m "V2.4.0 site update"
  git push

GitHub Pages rebuilds automatically in ~1 minute.

================================================================================
VERIFICATION CHECKLIST (POST-DEPLOY)
================================================================================

  [ ] https://davidstonko.github.io/huntmaryland-site/
      -> MDHuntFishOutdoors branding, 4 mode cards

  [ ] https://davidstonko.github.io/huntmaryland-site/privacy.html
      -> Effective Date June 10, 2026, V2.4.0, feedback email

  [ ] curl https://davidstonko.github.io/huntmaryland-site/.well-known/apple-app-site-association
      -> appIDs+components format, includes /huntmaryland-site/trip/*

  [ ] https://davidstonko.github.io/huntmaryland-site/join/TESTCODE
      -> Invite card showing TESTCODE + App Store button (served via 404.html)

  [ ] https://davidstonko.github.io/huntmaryland-site/trip/TESTCODE
      -> Camp Trip invite card showing TESTCODE

  NOTE: Apple's CDN caches AASA files for up to ~24h (mode=developer
  on-device testing bypasses the cache). Don't panic if Universal
  Links take a few hours to pick up the new file.

================================================================================
FUTURE: CUSTOM DOMAIN (optional)
================================================================================

If you buy mdhuntfishoutdoors.com or similar:
  1. Add domain under Pages settings
  2. Add CNAME DNS record pointing to davidstonko.github.io
  3. GitHub handles HTTPS automatically
  4. Update all privacy.html and AASA URLs to the new domain
     (and the AASA path components, which embed /huntmaryland-site/)
================================================================================
