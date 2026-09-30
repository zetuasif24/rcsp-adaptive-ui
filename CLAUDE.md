# CLAUDE.md — RCSP (Rural Community Service Portal)

Repository: `rcsp-adaptive-ui`
Thesis: *Adaptive Low-Bandwidth User Interface for Web Applications in Rural Environments*

## 1. Prototype vs. research contribution

- **RCSP is the experimental platform, not the contribution.** Keep it small.
- **The contribution** is the real-time, network-aware adaptive UI approach and its controlled evaluation against a conventional baseline.
- Always keep this distinction in code comments, docs, commit messages and thesis-facing text.
- Never invent results or unsupported novelty claims. Every claim must trace to implementation evidence or logged experiment data.

## 2. Stack (fixed; do not change without approval)

- Frontend: React + Vite + Tailwind CSS
- Backend: Django + Django REST Framework (Gunicorn, WhiteNoise)
- Database: PostgreSQL
- Local: Docker Compose (production-like settings) for all benchmark runs
- Hosted: Render free web service (Django serves the built React app, same origin) + Neon free PostgreSQL. Free tier only; no paid services.
- UI language: English only.

## 3. Scope

**Pages (7):** Home, Services, Service Details, Announcements, Application, Search, Profile. Plus a participant consent screen.

**Categories:** Health, Education Support, Agricultural Assistance, Social Assistance, Identity/Documentation Information. All content is clearly marked prototype/demo data. Images are generated placeholders.

**Models:** `User`, `Service`, `Announcement`, `Application` (status: PENDING → PROCESSING → APPROVED/REJECTED), plus research-only `RunLog` and `UsabilityResponse` in a `metrics` app. Add no other models without a clear application or research need.

**Excluded:** new protocols, infrastructure work, backend optimization as the main variable, native apps, AI/ML bandwidth prediction, payments, maps, messaging, social feed, chatbots, enterprise features.

## 4. Conventional vs. adaptive comparison (core requirement)

- Two conditions, same functionality, same backend, same database, same content, same tasks:
  - **Conventional:** normal loading, no network-aware behavior. Frozen baseline, tagged `baseline-v1` before adaptive work begins. Never removed or altered afterwards except for bug fixes that are documented.
  - **Adaptive:** network-aware resource and UI adaptation.
- One build, runtime flag: `?mode=conventional|adaptive`; `?profile=fast|moderate|slow|very-slow` forces a profile for testing.
- Adaptive code is code-split and loaded only in adaptive mode, so its cost is measurable.
- Adaptation must change actual resource/network behavior (image variants, lazy loading, deferral, request reduction, font loading), not only styling.
- The adaptive version must not become a different application.

## 5. Adaptive engine

Pipeline: `NetworkDetector → NetworkProfile → AdaptiveEngine → AdaptationRules → ResourceManager/UI Controller → UI`

- Detection: active probe (small fixed-size request; measures throughput and RTT) is the primary signal. `navigator.connection` is a secondary hint only (Chromium-only). An inline script in `index.html` applies the last known profile before first paint.
- Profiles: Fast, Moderate, Slow, Very slow. Thresholds and per-profile actions live in a documented JSON config (`AdaptationRules`), configurable until the experimental protocol is finalized.
- Modular and independently testable. Every decision is logged with its inputs (probe result, API hint, profile chosen, actions applied).
- Probe requests and bytes are logged separately and counted as adaptive-mode overhead.

| Profile | Behavior |
|---|---|
| Fast | Full-size images, normal loading |
| Moderate | 800w WebP, native lazy loading below the fold, non-critical content deferred |
| Slow | 480w images, all below-fold lazy, smaller list page sizes, system font, no animations |
| Very slow | Text-first, images on tap, no web fonts, search on submit |

## 6. Research measurement requirements

- **Performance:** FCP, page load time, data transferred, HTTP/API request count. Collected with `PerformanceObserver`/Resource Timing in the page and cross-checked with Playwright/CDP (HAR).
- **Usability:** task completion time, task success rate, perceived responsiveness, SUS and/or Likert items.
- **Networks:** 2G, 3G, 4G, Wi-Fi via Playwright + Chrome DevTools Protocol `Network.emulateNetworkConditions`. Profiles are defined in one versioned config file. Candidate values (finalize with supervisor): 2G ≈ 280/256 kbps, 800 ms RTT; 3G ≈ 1.6 Mbps/750 kbps, 300 ms RTT; 4G ≈ 9 Mbps, 170 ms RTT; Wi-Fi unthrottled.
- **Performance runs:** 7 pages × 2 modes × 4 networks × 30 cold-cache runs, each in a fresh browser context, discarding a warm-up run. Benchmarks run locally (Docker Compose). A smaller warmed-up confirmation run on the hosted instance is reported as secondary.
- **Usability study:** within-subjects, order counterbalanced, controlled 2G/3G profile, planned 30–40 participants, moderated on a lab machine with fixed throttling. Consent screen required. Ethics/supervisor approval required before data collection.
- **Fairness:** equivalent functionality, same data, same network profile for paired comparisons, repeated trials, documented browser/device/OS/environment, identical compression and cache headers for both modes. Do not tune the adaptive version on final results.
- **Data handling:** raw results are preserved and exported to CSV in `experiments/raw/` after every session. Analysis outputs go to `experiments/analysis/`. Raw data is never overwritten by analysis.
- **Reporting:** report medians, IQR, effect sizes and nonparametric tests. State limitations explicitly (emulated throttling, free-tier hosting, sample size).

## 7. Repository layout

```
rcsp/
├── frontend/src/{components,pages,adaptive,hooks,context,services,assets}
│   └── adaptive/{NetworkDetector,AdaptiveEngine,AdaptationRules,ResourceManager}.js
├── backend/{config,users,services,announcements,applications,metrics,api}
├── docs/{research,architecture,wireframes,experiments}
├── experiments/{config,raw,analysis}
├── CLAUDE.md
└── README.md
```

## 8. Coding conventions

- Small, reusable components; no dead code or speculative features.
- Frontend: functional components and hooks, Tailwind utilities, no extra UI libraries without approval.
- Backend: DRF serializers/viewsets, validation in serializers, environment-based settings (no secrets in Git), Django admin for demo data.
- Image variants (original, 800w WebP, 480w, 240w) are generated at seed time, not on the fly.
- Authentication: Django session auth with CSRF (same origin).
- Commits: small and descriptive; suggested milestones are architecture, scaffolding, backend APIs, baseline UI, integration, `baseline-v1` tag, network detection, adaptive engine, resource optimization, instrumentation, experiment setup.

## 9. Testing expectations

- Backend: unit tests for models, serializers and API endpoints.
- Adaptive engine: unit tests for profile classification and rule selection using fixed inputs.
- Frontend: component tests for both modes; the same task must pass in both.
- End to end: Playwright tests for each usability task in both modes.
- Instrumentation: verify metrics are logged with mode, profile and adaptation decisions before running any experiment.
- Run all tests before reporting a step complete.

## 10. Do not add without approval

Alternative stack; large enterprise features; AI/ML prediction; native apps; payment, mapping, messaging, social or chatbot features; changes to the research question or hypotheses; removal of the conventional baseline; functionally incomparable versions; unlogged or unexplainable adaptation logic; backend optimization as an experimental variable; paid services.

**Quality rule:** Does it support RCSP functionality? Does it support a fair adaptive-vs-conventional experiment? Can its effect be measured and explained? If not, do not add it.

## 11. Working method

- Work in controlled phases; ask before major architectural changes.
- Keep adaptation rules configurable and documented.
- After each major step, report: files changed, what was implemented, tests run, assumptions made, and the next recommended step.
- Current phase: scaffolding (React/Vite/Tailwind, Django/DRF, PostgreSQL config, env vars, Git, docs). No adaptive behavior yet. Verify frontend and backend run.
