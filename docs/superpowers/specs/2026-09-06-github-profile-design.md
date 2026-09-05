# GitHub Profile README — Design Spec

**Date:** 2026-09-06 · **Owner:** Jay Rathod (`Jaraxxxx`) · **Repo:** `Jaraxxxx/Jaraxxxx`

## Goal
Replace the default README template with a "state of the art" **hybrid** profile: terminal-flavoured intro + restrained animated widgets, positioned for a broad audience (recruiters, builder community, personal brand).

## Decisions (approved in conversation)
- **Vibe:** Hybrid (D) — terminal intro + stats/streak/snake widgets, no trophy shelf.
- **Positioning:** Balanced (D); employer (Swiggy) named inside the `whoami` block only, not in the headline.
- **Snake animation:** approved; auto-updates via GitHub Actions cron every 6h + manual dispatch + push trigger.
- **Contact links:** LinkedIn (`linkedin.com/in/jaraxxxx`), LeetCode (`leetcode.com/u/jaraxxxx`), Gmail (`jay.m.rathod.01@gmail.com`).
- **LeetCode stats card:** included (default toggle).
- **Push rights:** user pre-authorized direct push to `main`.

## Layout (top → bottom)
1. **Header** — capsule-render waving gradient (`0d1117→1f6feb`), "JAY RATHOD", desc "AI agent tooling · LLM infrastructure".
2. **Typing SVG** — JetBrains Mono, GitHub-green (`3FB950`), 4 rotating phrases.
3. **`~ $ whoami`** — console block: role @ Swiggy, focus areas, prev-life tags, blinking cursor.
4. **⚡ now building** — table of the 6 pi-ecosystem repos with verified one-liners (from repo READMEs).
5. **🧰 stack** — skillicons, 2 rows: `ts,python,go,java,cpp` / `kubernetes,docker,aws,terraform,grafana,githubactions`.
6. **📊 metrics** — GitHub stats + streak side by side (light/dark via `<picture>`), LeetCode card centered below.
7. **🐍 contributions** — snake SVG via `<picture>` (dark/light variants from `output` branch).
8. **📮 connect** — for-the-badge shields: LinkedIn · LeetCode · Gmail.
9. **Footer** — capsule-render waving gradient, no text.

## Widget endpoints (all verified HTTP 200 on 2026-09-06)
| Widget | URL |
|---|---|
| capsule-render | `https://capsule-render.vercel.app/api?...` |
| typing SVG | `https://readme-typing-svg.demolab.com?...` |
| GitHub stats | `https://github-readme-stats-sigma-five.vercel.app/api?...` (mirror; official instance was rate-limited 503) |
| Streak | `https://streak-stats.demolab.com?...` |
| LeetCode | `https://leetcode-stats-six.vercel.app/api?username=jaraxxxx` |
| Skill icons | `https://skillicons.dev/icons?i=...` |
| Snake | `https://raw.githubusercontent.com/Jaraxxxx/Jaraxxxx/output/github-contribution-grid-snake{-dark,}.svg` (after first workflow run) |

## Failure behaviour
- All widgets are plain `<img>` — a dead service degrades to alt text; rest of profile unaffected.
- Snake goes stale if Actions fails; profile still renders (404 image = blank).
- No secrets, no keys, all services free.

## Out-of-README polish (in scope)
- Repo descriptions + topics for the 6 pi-ecosystem repos and the profile repo (via `gh api`, `repo` scope).
- Pin 4 repos: `pi-usage-dashboard`, `forge`, `pi-extensions`, `Hybrid_Recommender_System` (GraphQL attempt; manual fallback).
- Profile bio — manual UI step (token lacks `user` scope); suggested text provided to user.

## Non-goals
- No trophy shelf, no blog-feed widget, no visitor counter, no Spotify/wakatime.

## v3 rework (2026-09-06, user feedback)
- **Professional + project-focused** (GitSkins philosophy: portfolio-first, real work forward).
- Removed `github-readme-stats` card — shared instance quota-dead on live page ("PAT_1" error card). Metrics = streak + LeetCode side by side. Self-hosted deploy (with own PAT) is the known path back if wanted.
- Removed quote-of-the-day widget (fluff/fragile).
- Typing SVG lines now lead with flagship project + role (no generic "pi and stuff" phrasing).
- New **🚀 featured project** spotlight (pi-usage-dashboard) between whoami and projects table; "now building" renamed "🛠 projects"; "snake says hi" renamed "📈 contributions".
- whoami block made professional: role line + `ls ./current-focus` (flagship first).
- Trophy + activity-graph still excluded (402 quota on shared instances).
