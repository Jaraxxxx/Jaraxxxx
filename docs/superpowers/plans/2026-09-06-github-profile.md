# GitHub Profile README Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Replace the default README in `Jaraxxxx/Jaraxxxx` with a hybrid terminal+widgets profile and add the snake-animation workflow.

**Architecture:** One public repo, two files: `README.md` (pure markdown/HTML, all widgets as `<img>` to third-party SVG services) and `.github/workflows/snake.yml` (Platane/snk → commits SVGs to `output` branch). No build step, no secrets.

**Tech stack:** GitHub-flavoured markdown + HTML, GitHub Actions, capsule-render / readme-typing-svg / github-readme-stats / streak-stats / leetcode-stats-six / skillicons.dev.

## Global Constraints
- Username: `Jaraxxxx` everywhere (stats, snake, raw URLs).
- Widget URLs must return HTTP 200 before commit (verified in spec table).
- Dark/light themes switched via `<picture>` + `prefers-color-scheme`.
- Snake SVGs live on `output` branch only — profile repo root stays clean.
- Push directly to `main` (user pre-authorized).

---

### Task 1: README.md

**Files:**
- Create: `README.md` (replaces default template)

- [ ] **Step 1: Write README.md** with sections in spec order (header wave → typing SVG → whoami console → now-building table → stack icons → metrics w/ picture-swap + leetcode → snake picture-swap → connect badges → footer wave). Full content: see `README.md` produced by this task — it is committed verbatim.

- [ ] **Step 2: Verify all embedded widget URLs return 200** (curl each URL in the file).
- [ ] **Step 3: Commit** — `git commit -m "feat: state-of-the-art profile README"`

### Task 2: Snake workflow

**Files:**
- Create: `.github/workflows/snake.yml`

- [ ] **Step 1: Write workflow** — triggers: cron `0 */6 * * *`, `workflow_dispatch`, push to `main`; `permissions: contents: write`; Platane/snk/svg-only@v3 → `dist/github-contribution-grid-snake.svg` + `dist/github-contribution-grid-snake-dark.svg?palette=github-dark`; crazy-max/ghaction-github-pages@v4 → `output` branch.
- [ ] **Step 2: Commit + push main.**

### Task 3: Verify + repo metadata

- [ ] **Step 1: Confirm Actions run succeeded** (`gh run list --repo Jaraxxxx/Jaraxxxx`), then `curl -f` both raw snake SVG URLs on `output` branch.
- [ ] **Step 2: Set repo descriptions + topics** for profile repo and the 6 pi-ecosystem repos via `gh api -X PATCH`.
- [ ] **Step 3: Pin repos** via GraphQL `pinnedItems` mutation: `pi-usage-dashboard`, `forge`, `pi-extensions`, `Hybrid_Recommender_System` (fallback: manual UI steps given to user).
- [ ] **Step 4: Report manual steps to user** (profile bio via UI — token lacks `user` scope).
