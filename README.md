# TimeBack — setup guide

A to-do list where each task counts down instead of up. Works on desktop and phone, synced through one GitHub repo, no server required. Anyone can "log in" with just a name — no password — which just decides which folder their tasks live in.

## 1. Create the repo

1. Go to github.com → **New repository**
2. Name it e.g. `timeback-app`
3. Public is fine (no private data concerns here)
4. Click **Create repository**

## 2. Create a personal access token

1. Go to github.com → click your profile photo → **Settings**
2. Scroll to **Developer settings** (bottom of left sidebar)
3. **Personal access tokens** → **Fine-grained tokens** → **Generate new token**
4. Name it `timeback`
5. Under **Repository access**, choose **Only select repositories** → pick `timeback-app`
6. Under **Permissions** → **Repository permissions** → set **Contents** to **Read and write**
7. Generate the token and **copy it somewhere safe** — GitHub only shows it once

## 3. Upload the app files

Upload these into the repo root:
- `index.html`
- `manifest.json`
- `icon.svg`
- `sw.js`

Then go to repo **Settings → Pages** → Source: **Deploy from a branch** → Branch: `main`, folder `/ (root)` → Save.

GitHub gives you a URL like `https://yourusername.github.io/timeback-app/`.

## 4. Open it and connect sync (once per device)

1. Open the GitHub Pages URL
2. You'll land on a login screen — type any name and tap **Continue**. This creates your own task list.
3. Tap the sync icon (top right) → **Setup sync**
4. Enter:
   - GitHub username
   - Repo name → `timeback-app`
   - Branch → `main`
   - Token → the one from step 2
5. Save — your tasks now sync to `user/<yourname>/tasks.json` in the repo

Repeat step 4 on your other device (same repo/token), then log in with the **same name** there to see the same task list.

## 5. Install it like an app

- **Android/Chrome:** open the URL → menu → **Add to Home screen**
- **iPhone/Safari:** open the URL → Share button → **Add to Home Screen**
- **Desktop (Chrome/Edge):** open the URL → address bar → install icon → **Install**

## Notes

- **No password / no real security.** Typing a name just tells the app which folder to read/write. Anyone who knows a token could see any user's folder in this repo. That's expected here since privacy wasn't a requirement.
- **Logout** clears the "current user" from that device's browser, showing the login screen again. It doesn't delete any data.
- **Theme toggle** (sun/moon icon) switches light/dark and remembers your choice per device.
- **Sync logic:** every change saves locally instantly (works offline). ~1.5s after a change it pushes to GitHub if online. On login/app open it pulls the latest version first; if both devices changed things while offline, the most recently edited version wins.
