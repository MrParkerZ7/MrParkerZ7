# CLAUDE.md — MrParkerZ7 Profile

## What this repo is

This is the **GitHub profile repository** (`MrParkerZ7/MrParkerZ7`). Its only
real content is `README.md`, which renders on the profile page at
github.com/MrParkerZ7. There is no application code.

## README structure

| Section | What it is |
|---------|-----------|
| Header | Name, LinkedIn/Medium badges, profile-view counter |
| 🧰 Things I Code With | Static shields.io badges (languages, frameworks, cloud/devops) |
| 🧑‍💻 Repositories | Authorship donut (`assets/authorship.svg`) + 4-column repo table |
| 📊 GitHub Stats | Streak card + live top-languages donut, equal height |
| 📈 Activity Graph | github-readme-activity-graph line graph |

## 🧑‍💻 Repositories section — how it's generated

The authorship chart and table are a **hardcoded snapshot** of live GitHub
data. They do NOT auto-update — they must be regenerated when repo counts
change.

### Classification rules
- **AI-Written** — a public, non-fork repo whose commits carry a
  `Co-Authored-By: Claude` trailer (built with Claude Code). Detected by
  scanning each repo's latest 100 commits for the trailer (case-insensitive).
- **Manually-Written** — public, non-fork, no Claude trailer found.
- **Forks** — public repos where `isFork = true` (excluded from authorship).
- **Private** — `isPrivate = true`. **Counted in the donut, never listed**
  (the table's Private column is intentionally empty — owner's request).

### Current snapshot (last refresh: 2026-06-07)
- AI-Written **25** · Manually-Written **61** · Forks **6** · Private **23**
- Total **115** (donut center reads "ALL REPOS")
- Note: the profile repo `MrParkerZ7` itself classifies as AI-Written
  (its commits carry the Claude trailer).

### How to refresh (counts + table)
1. Pull live data (needs `gh` authed as MrParkerZ7 with `repo` scope):
   - `gh repo list MrParkerZ7 --limit 1000 --json name,primaryLanguage,isFork,isPrivate`
2. For each public non-fork repo, scan commits for the trailer:
   - `gh api "repos/MrParkerZ7/<name>/commits?per_page=100"` → match
     `(?i)co-authored-by:\s*claude` in any `commit.message`.
3. Regenerate `assets/authorship.svg` and the repo table from the counts.
4. Empty/uninitialized repos return HTTP 409 — treat as Manual.

## assets/authorship.svg — the donut

Hand-authored SVG (not an external service) so it never 404s and renders
crisp. Effects: per-slice gradients, rounded segment caps, soft drop-shadows,
layered dark card. Verified to render in Blink (Edge headless) — the same
engine GitHub uses for inline `<img>` SVGs.

Design constants (tokyonight palette):
- Card bg `#1a1b27`-ish gradient; slice colors: AI `#2D7DD2`→`#8ab4ff`,
  Manual `#2E8B57`→`#a6e26b`, Forks `#8A2BE2`→`#c9a8ff`, Private slate
  `#566079`→`#aab2c6`.
- Ring is thin (thickness 30, radius 116) so the small Forks/Private slices
  read as proper arcs, not floating blobs. Gaps are slice-proportional.

To preview an edited SVG without committing:
`msedge --headless=new --disable-gpu --screenshot=out.png --window-size=660,380 file:///<abs-path>/assets/authorship.svg`

## 📊 GitHub Stats services

- Streak: `github-readme-streak-stats.herokuapp.com` (theme `tokyonight`)
- Languages: `github-profile-summary-cards.vercel.app` `repos-per-language`
  card (chosen over `github-readme-stats`, whose shared instance is
  chronically rate-limited / 503).
- Both sized by a shared `height` so they align.

## Conventions

- Theme everywhere: **tokyonight** dark.
- Branch: `main`. Commit messages end with the `Co-Authored-By: Claude`
  trailer (which is also what makes a repo count as AI-Written).
- Disposable temp files use the `🚫` prefix and must be deleted before commit.
- A self-updating alternative for the authorship chart (a scheduled GitHub
  Action that re-runs the scan and redraws the SVG) has been discussed but
  not yet implemented.
