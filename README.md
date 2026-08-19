# Mam-on Elementary School Data Portal

A single-page portal (SF1 learner profiles, schedules, grades, health/SBFP,
inventory, and a submission tracker) for Mam-on Elementary School.

## What was fixed in this pass
- **Login was being skipped entirely.** The `main-app` screen had no
  `hidden` class and `login-screen` did, so the dashboard loaded straight
  away regardless of whether anyone signed in. Swapped so `login-screen`
  shows first and `main-app` only appears after `handleLogin()` succeeds.
- **Removed the plaintext admin/principal credentials that were printed
  directly on the public login screen** (`jasper / admin123`,
  `eric / 12345`). Anyone who opened the page could read them without
  even trying to log in.

## Important limitation to know before you publish this
This file has **no server or database** — every learner record, grade,
and password lives in a JavaScript array inside the HTML itself. That
means:
- The login screen only gates the *UI*. Anyone who opens "View Page
  Source" in a browser can still read the full student list, health
  status entries, and the faculty username/password list, logged in or not.
- GitHub Pages (the free way to host a static site on GitHub) **always
  publishes the site publicly** — even a private repo's Pages site is
  public unless your school is on a paid GitHub Enterprise Cloud plan
  with the private-Pages feature turned on.
- Nothing entered while using the app is saved anywhere — refreshing the
  page resets everyone back to the sample data baked into the file.

**Before this goes anywhere near a public URL**, I'd strongly recommend
replacing the real-looking learner names, LRNs, and health/BMI entries
with placeholder data, and changing the faculty passwords — a portal
with children's health and academic records shouldn't be reachable by
anyone who happens to find the link or opens dev tools. If what's in
here now is real student data, keep the repo **private** and don't turn
on GitHub Pages until it's been scrubbed or moved behind real
authentication.

## Publishing to GitHub (once you're comfortable with the above)
1. Create a new repository on github.com (e.g. `mamon-es-portal`).
2. Upload `index.html` (rename kept as `index.html` so GitHub Pages
   serves it automatically) to the repo — either drag-and-drop on the
   GitHub website, or from a terminal:
   ```
   git init
   git add index.html README.md
   git commit -m "Initial portal upload"
   git branch -M main
   git remote add origin https://github.com/<your-username>/mamon-es-portal.git
   git push -u origin main
   ```
3. In the repo, go to **Settings → Pages**, set Source to the `main`
   branch, root folder, and save.
4. The live site appears at `https://<your-username>.github.io/mamon-es-portal/`
   after a minute or two.

## Real data persistence (next step, not done yet)
If you want changes made in the portal to actually be saved (instead of
resetting on every refresh), the two realistic options are:
- **Browser-only storage** (`localStorage`) — quick to add, but data
  stays on that one device/browser and isn't shared between users.
- **A real backend** (small database + API, e.g. via a free service like
  Supabase or Firebase) — needed if multiple teachers/staff should see
  the same live data from different computers.

Happy to build either one — just let me know which fits how the school
actually uses this.
