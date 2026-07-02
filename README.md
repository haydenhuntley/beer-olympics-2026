# 🇺🇸 Beer Olympics 2026 🦅

An interactive, USA-themed web app for the family Beer Olympics tournament — hosts the
schedule, live standings, championship bracket, and full game rules. Fireworks included. 🎆

**7 teams · 5 games · round robin → top-4 championship bracket (best 2 of 3).**

---

## 🚀 Quick start

### Option A — just open it (local mode)
Double-click **`index.html`**. It works immediately. Scores save on *that one device*
(browser localStorage). Great for testing or if one phone/laptop runs the whole event.

### Option B — live sync across everyone's phones (recommended for game day)
Everyone sees scores & bracket update in real time. Takes ~3 minutes to set up a **free**
Firebase project:

1. Go to <https://console.firebase.google.com> → **Add project** (name it anything, disable
   Google Analytics to keep it simple).
2. In the left menu: **Build → Realtime Database → Create Database**.
   - Pick a location, then choose **Start in test mode** (fine for a family weekend).
   - > ⚠️ Test mode lets anyone with the link read/write. That's intended here so relatives
     > can update scores without logins. It auto-expires in ~30 days — perfect for the event.
3. Add a **Web app**: Project Overview → the **`</>`** (web) icon → register app.
   Firebase shows you a `firebaseConfig = { ... }` object.
4. Copy those values into **`firebase-config.js`** (in this folder). The important one is
   **`databaseURL`** — make sure it's filled in (it ends in `firebasedatabase.app`).
5. Reload the app. The pill at the bottom should turn green: **"Live · synced to all devices."**

---

## 🌐 Putting it online (so family can open a link)

The repo is already on GitHub. Easiest free host is **GitHub Pages**:

1. Push these files to the `main` branch (see below).
2. On GitHub: **Settings → Pages → Source: Deploy from a branch → `main` / root → Save.**
3. Wait ~1 min. Your app is live at
   `https://<your-username>.github.io/beer-olymics-2026/`
4. Text that link to the family. Everyone with it sees the same live tournament.

```bash
git add .
git commit -m "Beer Olympics 2026 app"
git push
```

*(Alternatives: drag the folder onto [netlify.com/drop](https://app.netlify.com/drop) or
run `npx serve` locally.)*

---

## 🎮 How to run the tournament

- **Schedule tab:** tap the winning team of each match. Scores are optional. Each round is
  a single game type (Round 1 = Flip Cup, Round 2 = Beer Pong, etc.) so you set up one game
  at a time.
- **Standings tab:** updates automatically. Top 4 are highlighted — they make the bracket.
  Ties break by head-to-head, then a dart-off (see below).
- **Bracket tab:** once you have results, the top 4 seeds auto-populate. #1 vs #4 and #2 vs #3,
  best 2 of 3. Pick each game and tap the winner; the final and champion fill in automatically
  (with fireworks 🎆).
- **Rules tab:** every game's rules, including the shortened Beer Pong and new Pictionary.
- **Reset:** bottom of the page → **admin / reset** → wipes all scores/bracket for everyone.

### Tiebreakers
Seeding order is **wins → head-to-head → dart-off**. Head-to-head is automatic. If teams are
still tied and you run the dart-off, you can record it manually — see
`state.seedTiebreak` in `index.html` (higher number = better; a small UI hook is in place).

---

## 📁 Files
| File | What it is |
|------|-----------|
| `index.html` | The entire app (UI, schedule data, logic, fireworks). Self-contained. |
| `firebase-config.js` | Paste your Firebase keys here for live sync. Optional. |
| `README.md` | This file. |
| `Beer Olympics 2025.pdf` | Last year's reference. |

## 🏈 The 2026 teams
Hayden & Maddie · Jordan & Paul · Jill & Jack · Emma & Bennett · Amy & Nick · Andrea & John · Lily & Will

*NO FOUL PLAY AND EVERYONE MUST HAVE FUN!* 🇺🇸
