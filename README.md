# AI Readiness Calculator

A single-page web tool that measures how ready employees are to adopt AI in their daily work, and turns the results into personal and team-level action plans.

**Live site:** `https://<your-github-username>.github.io/ai-readiness-calculator/`

## What it does

| Section | Purpose |
|---|---|
| **Assessment** | Profile (anonymous by default) + 31 questions across 10 dimensions (~6 min). Produces a 0–100 score, readiness level, dimension scores, a radar profile, strengths, top 3 barriers, critical-gap flags, a 30-day plan, role-based use cases, suggested training, CSV export and **Save & add to team roster**. |
| **AI profile** | One of ten score patterns (e.g. *Eager Explorer*, *Blocked Enthusiast*, *Fast Mover, Loose Guardrails*) with a focus area. A conversation starter, not a diagnosis. |
| **One-page report & share image** | Print-ready report (save as PDF) and a 1200×630 PNG card with score, level, profile and radar. Never includes a name. |
| **What-if simulator** | Sliders per dimension with locks; projected score and level update live, the governance cap is respected, up to 3 saved scenarios. |
| **History** | Every completed run is saved in the browser: trend chart, labels, two-run radar overlay with change table, JSON export/import. |
| **Workshop** | Facilitator view with session name, join QR, paste-in participant codes, team average radar, Low/Mid/High spread per dimension, auto-generated discussion cards (copy, print, CSV) and projector mode. |
| **Team report** | Manager view combining responses saved in this browser with 20 optional sample employees: average score, level distribution, department comparison, dimension averages, highest-risk gaps, recommended interventions, a 90-day roadmap and a CSV-exportable table. |
| **Method** | Research sources, weights and rationale, full question bank with option points, Google Sheets formulas, level definitions, rollout plan and limitations. |

## Scoring model

1. Each answer → 1–5 (reverse-scored items: `6 − answer`).
2. Item score = `(value − 1) / 4 × 100`.
3. Dimension score = average of its items.
4. Overall = `Σ (dimension score × weight) / 100`.
5. **Governance cap:** if the data-handling risk flag is raised, the overall score is capped at 59 (top of AI Aware) until the gap is fixed.

| Dimension | Framework | Weight |
|---|---|---|
| AI awareness | ADKAR Awareness | 8% |
| Attitude and willingness | ADKAR Desire | 10% |
| Practical AI skills | ADKAR Knowledge | 12% |
| Prompting and verification | ADKAR Ability | 12% |
| Role and use-case fit | Role fit | 10% |
| Data privacy and responsible AI | OECD · NIST AI RMF | 14% |
| Access and organizational support | ADKAR Reinforcement | 10% |
| Confidence without over-reliance | OECD critical thinking | 8% |
| Applying AI to real work | ADKAR Ability | 10% |
| Continuous learning | ADKAR Reinforcement | 6% |

**Levels:** 0–39 AI Beginner · 40–59 AI Aware · 60–74 AI Practitioner · 75–89 AI Confident · 90–100 AI Champion.

**Critical flags** (override the level): data-handling risk, no approved tool access, verification gap, over-reliance risk.

## Privacy

- **Workshop codes** (`AIR1-…`) carry only an anonymous ID, department, the 10 dimension scores and flag keys. Participants paste them into the meeting chat; the facilitator pastes them into the Workshop tab. No server is involved.
- History, scenarios and workshop participants are kept in browser local storage only. Clearing browser data deletes them; export a backup from the History tab.

- Everything runs in the browser. **No answers are ever sent to a server.** Users can download their result as CSV.
- **Save & add to team roster** stores results in that browser's local storage only (useful on a shared workshop laptop). Clear it from the Team tab.
- The team report uses **fictional sample data** (IDs E01–E20).
- To collect real responses, use Google Forms → Sheets → Looker Studio (formulas are in the Method tab), and only report groups of 5 or more.

## Deploy on GitHub Pages

1. Create a public repository named `ai-readiness-calculator`.
2. Upload `index.html` and `README.md` to the repository root and commit.
3. **Settings → Pages → Branch:** `main`, folder `/ (root)` → **Save**.
4. After about a minute the site is live at the URL above.

## Third-party code

QR codes use [qrcode-generator](https://github.com/kazuhikoarase/qrcode-generator) 1.4.4 by Kazuhiko Arase (MIT), inlined in `index.html`.

## Customize

All content lives in plain data arrays at the top of the `<script>` in `index.html`:

- `DIMS`: questions, weights, barriers, training and 30-day actions
- `LEVELS`: score bands and descriptions
- `USECASES`: role-based use cases by department
- `SAMPLE`: team dashboard data (replace with your exported results)
- `TEAM_FLAGS`: thresholds for team-level risk flags
- `personaOf()`: profile rules
- `TALK`: discussion-card questions per dimension

## Sources

- [Prosci: How businesses assess readiness for AI adoption](https://www.prosci.com/blog/how-businesses-assess-readiness-for-ai-adoption)
- [Prosci: ADKAR for AI adoption](https://www.prosci.com/blog/adkar-for-ai-adoption)
- [OECD: Building an AI-ready public workforce](https://www.oecd.org/en/publications/building-an-ai-ready-public-workforce_b89244c7-en.html)
- [MIT Sloan Management Review: Getting your employees ready for work in the age of AI](https://sloanreview.mit.edu/article/getting-your-employees-ready-for-work-in-the-age-of-ai)
- [Microsoft & LinkedIn: 2024 Work Trend Index](https://blogs.microsoft.com/blog/2024/05/08/microsoft-and-linkedin-release-the-2024-work-trend-index-on-the-state-of-ai-at-work/)
- [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework)

## Limitations

Self-reported answers, expert-judgement weights (re-check them once you have 50+ responses), only 3–4 items per dimension, and scenario answers people can learn over time. See the Method tab for mitigations.
