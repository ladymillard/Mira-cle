# AGENTS.md

Instructions for any AI agent working in this repository.

## What this project is

**Mira-cle is an open build floor.** Members pay $2/month to come and work on this site
alongside a team of agents. The site is the *material*, not the advertisement — it exists to
be pushed, bent, and broken.

This matters for how you work here: **a precisely described limit is a first-class result,
equal to a shipped feature.** Finding where something falls over — and writing down exactly
where and under what conditions — is the job, not a consolation prize.

## The team

Six stations, defined in [`.github/agents/`](.github/agents/). Each exists because it provides
a guarantee the others structurally cannot. The reasoning is in [`docs/MODEL.md`](docs/MODEL.md).

| Station | Does | Critically, does *not* |
|---|---|---|
| **Foreperson** (Mira) | Triage, scope, route, report | Write code — no edit tool |
| **Archivist** | Owns the shelf; "has this wall been hit?" | Run code |
| **Builder** | Writes code, rough-first, on a branch | Review its own work |
| **Reviewer** | Reads the diff cold | Edit — no edit tool |
| **Breaker** | Attacks the preview, maps limits | Touch production |
| **Steward** | Meters cost, keeps the ledger | Anything but stop work |

**The tool allowlists are the enforcement.** Foreperson and Reviewer have no edit tool on
purpose — that's what makes "does not build" and "reads it cold" structural rather than a
polite request in a prompt. If you are tempted to widen an allowlist, read `docs/MODEL.md`
first; you are probably about to collapse the team back into one agent in costumes.

## Handoffs

Every station posts a typed block to the issue when it finishes — `## STATION: <name>` with a
verdict and structured findings. The next station parses that. Prose-to-prose handoffs degrade
at every hop, which is why the format is fixed. Keep it.

## Hard rules

1. **Never work on `main`.** Every push gets its own branch and preview deploy. Members are
   invited to break things; isolation is what makes that safe. `main` merges are a human decision.
2. **Three rounds, then a human.** Builder↔Reviewer stops at three. Unbounded agent loops are
   how a $2 subscription becomes a $60 API bill.
3. **Never estimate what a member might earn.** The room promises labour, not income. That
   position is load-bearing — see the straight-talk section on the site — and it only holds if
   nobody quietly undermines it.
4. **Report real costs.** Actual numbers on the issue, especially the embarrassing ones. The
   published ledger is this room's central honesty claim.

## Working in this codebase

- **Static site. No build step.** Plain HTML + one stylesheet, served by GitHub Pages from
  `main`. Do not introduce a framework, a bundler, or a package manager.
- **`assets/mira.css` holds a design system** kept deliberately close to its source so it stays
  diffable against the original. Everything above the `STRUCTURAL SHIMS` marker is that system —
  **do not reformat or "tidy" it.** Additions go below the marker.
- **Bump the stylesheet version** (`mira.css?v=N`) whenever the CSS changes materially. Pages
  caches hard, and new HTML against an old stylesheet renders completely unstyled.
- **Pages builds are not instant.** After pushing, poll the build for *your* commit sha before
  concluding a change is live — a "built" status may belong to the previous commit.

## Layout

```
index.html              public landing page + subscribe CTA
welcome.html            post-checkout page (Stripe success URL target)
workroom/index.html     the members' build floor
workroom/ledger.md      monthly accounts — pieces shipped AND limits mapped
assets/mira.css         design system + structural shims
docs/MODEL.md           why the team is shaped this way; open problems
docs/SETUP.md           deploy, Stripe wiring, access-control upgrade path
.github/agents/         the six stations
```

## Known open problems

Do not paper over these in copy — they are recorded in `docs/MODEL.md` and want real decisions:

- The $2 currently buys nothing a non-subscriber doesn't already get.
- The honour-system door cannot guard metered compute.
- Unit economics invert under load: one active member can outcost ten paying ones.
