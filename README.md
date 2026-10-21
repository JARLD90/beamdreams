# beamdreams.art

Beta site for Beam Dreams. Static HTML, zero build, deployed by Cloudflare Pages from this repo
(same architecture as cuedup.art).

## Pages
- `/` → redirects to `/beta/`
- `/beta/` landing + sign-up gate (Formspree) · `/beta/about` · `/beta/start` · `/beta/changelog`
- `/beta/feedback` · `/beta/report` (bug, with screenshots) · `/beta/thanks`

## One-time setup (owner)
1. **GitHub**: create an empty repo `JARLD90/beamdreams`, then from this folder:
   `git remote add origin git@github.com:JARLD90/beamdreams.git && git push -u origin main`
2. **Cloudflare**: deployed as a static-assets Worker (the current form of Pages) from this folder:
   `wrangler deploy` (after `wrangler login`). `wrangler.jsonc` carries the custom domains
   `beamdreams.art` + `www.beamdreams.art`; they attach once the zone's nameservers point at
   Cloudflare (kenneth.ns.cloudflare.com, molly.ns.cloudflare.com). Live preview:
   https://beamdreams.jamie-roderick.workers.dev
3. **Formspree**: create three forms (Sign-ups, Feedback, Bug reports) and paste their IDs:
   - `beta/index.html` → `SIGNUP_FORM`
   - `beta/feedback.html` → form `action`
   - `beta/report.html` → form `action` (enable file uploads on that form)
4. **Email**: Cloudflare → Email Routing → forward `support@beamdreams.art` to your inbox.
5. When the hosted beta is live, set `APP_URL` / `TESTFLIGHT_URL` in `beta/index.html`; until then
   the page collects sign-ups and promises an invite.

## Release flow
Bump `BETA_VERSION` in `beta/index.html`, add a section to `beta/changelog.html`, commit, push,
then `wrangler deploy` from this folder (live in seconds).
