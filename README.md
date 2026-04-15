# Clue: Springfield Deduction Engine

A real-time deduction tracker for **Simpsons Clue** — with constraint propagation, probability analysis, board map, show tracking, and optimal suggestion recommendations.

## Features

- **Knowledge Matrix** — auto-propagates card constraints after every suggestion
- **Probability Analysis** — grayscale heatmap showing which cards are most likely the solution
- **Board Map** — visual room layout with distance tracking and exact roll-based reachability
- **Show Tracker** — logs which cards you've shown to whom and recommends re-showing the same card to minimize info leakage
- **Optimal Suggestions** — recommends what to suggest next, balanced by info value and travel distance

## Deploy to GitHub Pages

```bash
# 1. Create a new repo on github.com (e.g. "clue-tracker"), then:

git init
git add .
git commit -m "initial commit"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/clue-tracker.git
git push -u origin main

# 2. Go to Settings → Pages → Source: "Deploy from a branch" → Branch: main → / (root) → Save
# 3. Your site will be live at: https://YOUR_USERNAME.github.io/clue-tracker/
```

## Deploy to Vercel

```bash
# Option A: Link your GitHub repo to Vercel (auto-deploys on push)
# Option B: Use Vercel CLI:
npm i -g vercel
vercel
```

## Usage

1. Open `index.html` in any browser (works fully offline after first font load)
2. **Setup** — enter players, pick your character, starting room, and tap your cards
3. **Log Suggestion** — after each suggestion, log responses and track your shown cards
4. **Board** — enter your dice roll to see which rooms you can reach
5. **Analysis** — watch the probability grid narrow as you play

## Customization

Edit the arrays at the top of `index.html` to use different characters, weapons, or rooms:

```javascript
const SUS = ['Homer','Marge','Bart','Lisa','Waylon Smithers','Krusty'];
const WPN = ['Plutonium Rod','Slingshot','Necklace','Saxophone','Extendo Glove','Poisoned Doughnut'];
const RMS = ['Krusty Loose Studios','Burns Manor',...];
```
