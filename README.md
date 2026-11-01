# 🚌 Fun Bus

A weekly lift-club planner for school runs, shared live between a few families.

## What it does
- Week board (Mon–Sat, AM/PM) starting w/c 2 Nov 2026; each new week starts blank
- Tap a slot to edit: time, driver, which kids, second car, "not needed", "everyone takes their own", "no run"
- "Ask for cover" → anyone can tap **I'll take it**
- Copy last week
- Morning times: each driver's usual departure time, used when they're picked for a morning run
- Share to WhatsApp in the group's usual text format
- Runs-per-family tally and a log of recent changes
- Live: every change shows up on everyone's phone, and it works offline and syncs later
- Installs to the home screen like an app

## Rules it follows
- **Mornings:** always one car, all kids.
- **Evenings:** one or two cars depending on clubs.
- **A child on their own for a late club** is collected by their own parents ("own pickup").

## Privacy
No names or schedules are in this repo. The families and the usual week live in the club's
database, and the board only opens with the club code. The code itself is never stored:
the club's data sits under a hash of it, and the access rules (`firestore.rules`) don't
allow anyone to list clubs. Search engines are asked not to index the site.

## Setting it up
1. **Firebase:** create a free project at console.firebase.google.com, add a **Firestore
   database** (production mode), then add a **Web app** and copy its config values into
   the app folder's `config.js`.
2. **Access rules:** in Firestore → Rules, replace everything with the contents of
   `firestore.rules` and click **Publish**.
3. **GitHub Pages:** repo Settings → Pages → Deploy from a branch → `main`, folder `/ (root)`.
4. **Create the club (once):** open the board, tap "Setting up the club for the first time?",
   choose a club code (three random words work well) and paste the setup text.
5. Share the board link and the code with the other parents. Each phone enters the code once.

The setup text is JSON: `{"families":[{"name","parents":[1–2],"kids":[1–3]}…], "usualWeek":{…}}`.
`usualWeek` is optional; without it the board starts from a simple rota you can edit and
save as the usual week.

## Files
- `index.html`, `robots.txt`: keep the site root empty and unindexed
- the app folder: `index.html` (the whole app), `config.js`, icons and manifest
- `firestore.rules`: database access rules to paste into Firebase
