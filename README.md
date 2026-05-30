# 🧠 HireVue Game-Based Assessment Practice

> A faithful, browser-only recreation of the **cognitive & spatial** games used
> in HireVue's game-based assessment battery (the Pymetrics-style tests).
> Built for self-prep: every game is timed, adaptive, scored, and tuned to ramp
> **beyond** the difficulty levels the real assessment is likely to use, so you
> arrive over-prepared.

<p align="center">
  <em>⭐ If this helped you land an interview, please star the repo — it's the only signal that tells me to keep maintaining it.</em>
</p>

---

## ✨ Highlights

- 🧩 **7 games**, each fully self-contained — open any single HTML file and play.
- 🚀 **Zero dependencies, zero build step** — pure HTML / CSS / vanilla JS.
- 📈 **Adaptive difficulty** that pushes past what the real battery exposes.
- 💾 **Personal-best tracking** via `localStorage` — survives reloads, private to your browser.
- ⏱️ **3-minute session clock** matching the real assessment cadence.
- 🌐 **Deployable as a static site** (GitHub Pages, Netlify, S3, anything).

> ℹ️ Personality / emotional games (Portrait, PortraitXT, E-Motions, TeamChat)
> are intentionally omitted — those measure self-report style, not ability,
> and are not improved by practice.

---

## 🎮 Games

| # | Game | Skill measured | Difficulty ramp |
|---|------|----------------|-----------------|
| 1 | 🔢 [Numerosity](src/numerosity/)   | Mental arithmetic, numerical reasoning | 2-pick → 3-pick · `+ − × ÷` · larger operands |
| 2 | 🔡 [DigitSpan](src/digitspan/)     | Short-term & working memory            | Span 3 → 12 · forward + reverse · digits + letters |
| 3 | 🔁 [Flashback](src/flashback/)     | Working memory (n-back)                | 1-back → 4-back · richer shape vocabulary |
| 4 | 🗺️ [Pathfinder](src/pathfinder/)   | Spatial reasoning, planning            | 3×3 → 6×6 grids · more turns and dead-ends |
| 5 | 🧩 [Puzzle](src/puzzle/)           | Visual memory, problem-solving         | 3×3 → 5×5 swap puzzle · shorter memorise window |
| 6 | 💃 [Shapedance](src/shapedance/)   | Visual processing, attention           | 2×2 → 5×5 patterns · rotation-invariant matches |
| 7 | 🎯 [Singularity](src/singularity/) | Attention, visual processing speed     | 9 → 64 shapes · subtler differences, rotation distractors |

---

## 🚀 Quick start

The **recommended** entry point is the single-file SPA at the project root:

```bash
# any static server works
python3 -m http.server 8000
# then open http://localhost:8000/
```

Or just **double-click `index.html`** — it's a self-contained single-page app:
all 7 games live in one file, hash-based routing (no reloads), zero build step.

### 🕹️ Two ways to play

| Mode | Where | Why |
|------|-------|-----|
| 🟢 **All-in-one SPA** (recommended) | [`index.html`](./index.html) | Instant switching between games, shared score sidebar, one tab to keep open. |
| 🔵 **Standalone per-game** | [`src/<game>/index.html`](./src/) | Each game is also a fully self-contained HTML file you can open, link, or embed in isolation. Same logic, same scoring. |

Both modes share the same `localStorage` personal-best storage, so a run
recorded in either mode shows up in the other.

### 🌍 Host on GitHub Pages

1. Push this repo to GitHub.
2. **Settings → Pages → Build from `main` / root**.
3. The root `index.html` is the playable hub. Standalone pages at
   `/src/<game>/` also resolve directly.

---

## ⚙️ How each game works

### 🧰 Common engine
Every game shares the same controls and scoring contract:

- ⏱️ **3-minute total clock** per session (matches the real assessment).
- ⌛ **Per-question timer** sized to the round difficulty.
- 📊 **Adaptive ladder**: a correct answer advances level; a wrong answer or
  time-out keeps you at the same level and regenerates the question. The level
  schedule for each game is hand-tuned to *exceed* what HireVue exposes.
- 🎯 **Scoring**: `points = base × difficulty multiplier × speed bonus`.
  Streaks add a multiplier. Final score, accuracy, max level, and median
  response time are saved to `localStorage` as **personal bests** per game.
- 🔊 **Audio + sound toggle**, keyboard shortcuts where they fit, a back-arrow
  to the hub on every page.

### 🔢 Numerosity
Hexagonal tiles with numbers. A target and operation (`+ − × ÷`) are shown.
Pick the smallest set of tiles whose result equals the target. Two-pick rounds
ramp into three-pick rounds. Multiplication rounds avoid "any pair already
products to the target" distractors so the harder rounds are actually harder.

### 🔡 DigitSpan
Watch a sequence, type it back. Three reveal modes mirror the official test:
**all-at-once**, **one-by-one**, and **first-half-then-second-half**.
Reverse mode is also available — and you should practise it; it loads working
memory much harder than forward recall.

### 🔁 Flashback (n-back)
Shapes flash one at a time. Decide whether the current shape equals the one
shown `n` items earlier. `n` adapts: it climbs after a streak of correct
answers and drops on misses. Targets, lures (`n ± 1`), and decoys are balanced
so you can't game it by always pressing match or always pressing no-match.

### 🗺️ Pathfinder
A grid of road tiles between a green **Start** and red **End**. Click two
tiles to swap them. Build a single unbroken path. Connectivity is verified
strictly — the path must follow each tile's openings, no off-tile cheating.

### 🧩 Puzzle
A generated picture is shown briefly, then scrambled. **Click any two tiles to
swap them.** Correctly-placed tiles glow green. Every shuffle is reachable via
swaps, so no puzzle is ever impossible. Larger grids and shorter memorise
windows ramp the difficulty.

### 💃 Shapedance
One pattern appears multiple times (possibly rotated) among unique distractors.
Select **all** of its copies. Some tiles spin to add noise — ignore motion.

### 🎯 Singularity
Find the one shape that differs. Distractors share form / colour / size /
rotation with the target group, so you can't shortcut on a single feature.
Rotation alone never makes a shape "unique".

---

## 💡 Tips for the real assessment

- 📖 Read the instructions on each game's first screen — the rules differ
  between games and HireVue **will** change small things.
- 🤫 Quiet room, full screen, no notifications. The tests are short and timing
  matters.
- 🎯 Accuracy beats speed up to a point: most ramps demand a sustained streak,
  not bursts.
- 🧠 Practise reverse **DigitSpan** and 3-back+ **Flashback** specifically —
  those two pull the most weight on the overall cognitive score.

---

## 📁 Project layout

```
.
├── index.html         # ⭐ Single-file SPA — all 7 games, hash-routed
├── README.md
├── .gitignore
└── src/
    ├── index.html     # standalone hub (links to per-game pages)
    ├── numerosity/    # standalone, fully self-contained
    ├── digitspan/
    ├── flashback/
    ├── pathfinder/
    ├── puzzle/
    ├── shapedance/
    └── singularity/
```

The root [`index.html`](./index.html) is the **primary entry point** — one
file, all 7 games, smooth hash-based switching (`#hub`, `#numerosity`, …).

The `/src/<game>/` folder keeps each game as a **separately runnable, fully
self-contained HTML file** (same logic, same scoring) — handy for linking,
embedding, or studying one game's source in isolation.

---

## 🤝 Contributing

Issues and PRs welcome — especially:

- 🐛 Bug reports with a reproducible sequence of clicks.
- 🎚️ Difficulty-curve tuning suggestions for any of the 7 games.
- ♿ Accessibility improvements (keyboard nav, contrast, screen-reader labels).

---

## ⭐ Like it?

If this saved you prep time, **please star the repo** — it's the only metric
that tells me people are using it, and it's the only nudge that gets me to
keep maintaining and adding games.

---

## 📜 License

**MIT** — practice freely.
