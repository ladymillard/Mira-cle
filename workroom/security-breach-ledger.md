# Security Breach Ledger

This ledger records security exposures, access-control gaps, breach-like failures, and the
decisions needed to close them.

It is deliberately public. Mira-cle asks members to push on the system, so the room needs a
place where its weak points are named without softening them into "future work."

**Current incident status:** one user-reported incident date is now recorded:
February 7, 2026. The ledger still needs the underlying evidence packet before it can state
what was accessed, changed, created, or misattributed.

**Current security posture:** intentionally soft door; unsafe for private material; not yet
safe for metered agent compute.

---

## Severity Key

| Level | Meaning |
|---|---|
| Critical | Can spend money, expose private material, or compromise production without a reliable stop. |
| High | Breaks the paid-member boundary or makes abuse likely once usage grows. |
| Medium | Creates confusion, leakage, or operational risk, but does not immediately spend money or expose secrets. |
| Low | Documentation or process gap that still deserves a written owner. |

## Status Key

| Status | Meaning |
|---|---|
| Open | Known and not yet fixed. |
| Accepted | Deliberate tradeoff for now; revisit trigger is named. |
| Mitigated | Reduced enough to operate, but not fully solved. |
| Closed | Fixed and verified. |

---

## Active Breach Ledger

### SBL-000 - February 7, 2026 Incident Record Is Incomplete

**Severity:** Critical  
**Status:** Open  
**Incident date:** 2026-02-07  
**First recorded in this ledger:** 2026-09-13  
**Source:** Diana's September 13, 2026 correction; related local provenance notes in
`/Users/chaiaininja/Desktop/ChAI-Books-Orchestration/`

The security ledger was originally framed around current workroom access-control gaps. Diana
clarified that the intended security-breach ledger should center the incident on
February 7, 2026.

**Known so far:**

- Diana identified February 7, 2026 as the incident date.
- Existing local notes describe unresolved provenance around unexpected secret/hidden-agent
  files in the ChAI source trail.
- The strongest nearby preserved evidence currently found locally is dated February 15, 2026,
  not February 7, 2026.
- Those February 15 commits entered the repository under `Diana Smith <ladymillard@gmail.com>`,
  but Diana previously said she did not know about Merkabah and would not have created secret
  files.

**Why this matters:** this is the difference between a product-risk register and an incident
ledger. A real incident ledger needs a timeline, evidence sources, impacted systems, affected
identities, containment actions, and unresolved questions. Without those, the record can
accidentally minimize the incident or overstate facts that are not yet proven.

**Immediate containment / preservation rule:**

- Do not delete Merkabah, professor, agent-auth, wallet, command-center, or git-history
  evidence.
- Treat suspicious authorship, hidden-agent files, wallet traces, API-key generation,
  ghost-account references, and removed-agent records as evidence until reviewed.
- Do not publish private or sensitive claims from the evidence trail without Diana's explicit
  approval.

**Required evidence packet:**

1. What happened on February 7, 2026.
2. Which repo, account, device, wallet, service, or agent was involved.
3. The first timestamped sign of compromise or unauthorized action.
4. The exact files, commits, messages, logs, wallets, or generated keys connected to it.
5. What changed after February 7, including the February 15 Merkabah/professor commits.
6. Any money, identity, authorship, access, or data exposure impact.

**Close condition:** the February 7 incident has a sourced timeline and each related artifact
is classified as confirmed evidence, adjacent evidence, disproven, or still unresolved.

---

### SBL-001 - Workroom Door Has No Lock

**Severity:** High  
**Status:** Accepted  
**First recorded:** 2026-09-12  
**Source:** `README.md`, `welcome.html`, `workroom/index.html`, `docs/SETUP.md`, `docs/MODEL.md`

The workroom is a public GitHub Pages URL with `noindex`, not an access control system. Anyone
with the URL can enter, whether or not they paid.

**Why this matters:** the current product says "members only," but the door is social trust,
not security. That is survivable while the room protects documents. It is not survivable once
the room protects metered compute or private pushes.

**Current mitigation:**

- The copy states that the link has no lock.
- Members are told not to share the URL.
- The repository documents the upgrade path to a Stripe-backed lock.

**Close condition:**

- Stripe subscription state is checked before rendering the workroom or dispatching agents.
- Inactive subscribers cannot open the workroom through a shared URL.

**Revisit trigger:** first non-trivial subscriber count, first shared-link abuse, or before any
paid agent dispatch is exposed.

---

### SBL-002 - Payment Is Not Bound To Access

**Severity:** High  
**Status:** Open  
**First recorded:** 2026-09-12  
**Source:** `docs/SETUP.md`

Stripe collects payment and redirects to `welcome.html`, but the site does not verify active
subscription state. The receipt proves a checkout happened somewhere; it does not become a
session, entitlement, or membership check inside the site.

**Why this matters:** paid status cannot be enforced, cancelled users are not blocked, and a
forwarded success/workroom link bypasses the payment boundary entirely.

**Required fix:**

1. Add a webhook endpoint for subscription events.
2. Store `{ email, status, current_period_end }`.
3. Issue a magic-link session.
4. Check `status === "active"` before rendering the workroom or dispatching work.

**Close condition:** an inactive or unknown email cannot access the workroom or trigger an
agent run.

---

### SBL-003 - Agent Compute Is Not Gated

**Severity:** Critical  
**Status:** Open  
**First recorded:** 2026-09-12  
**Source:** `docs/MODEL.md`, `AGENTS.md`

The model describes six stations that can spend API money, but there is no implemented gate
that checks whether the requester is allowed to spend the room's budget.

**Why this matters:** one active or malicious user can cost more than many annual memberships
produce. The economics fail hardest when the room is most useful.

**Current mitigation:**

- The Steward role is documented as the budget stop.
- Builder/Reviewer loops are capped at three rounds by policy.

**Missing mitigation:**

- No technical dispatch gate.
- No per-member allowance.
- No bring-your-own-key path.
- No ledger line item generated from actual agent usage.

**Close condition:** agent dispatch requires active subscription status and an explicit budget
source: room allowance, metered add-on, or member-provided key.

---

### SBL-004 - Production Is The Break Surface

**Severity:** Critical  
**Status:** Open  
**First recorded:** 2026-09-12  
**Source:** `docs/MODEL.md`, `AGENTS.md`

Members are invited to break the site, but the current static GitHub Pages setup has no
automatic branch preview environment. Without isolation, a real "break it" push points at
production.

**Why this matters:** a product built around limit-finding cannot let the live site be the
first target. Breaking production would be self-inflicted, not a finding.

**Current mitigation:**

- The rules say every push must happen on a branch.
- `main` merges are documented as a human decision.

**Missing mitigation:**

- Automated preview deploys.
- Branch protection documented as configured, not merely intended.
- Breaker instructions tied to a preview URL instead of production.

**Close condition:** every push has a branch and preview URL before Builder or Breaker work
starts, and `main` is protected from direct agent pushes.

---

### SBL-005 - Public Board Can Attract Sensitive Material

**Severity:** Medium  
**Status:** Accepted  
**First recorded:** 2026-09-12  
**Source:** `README.md`, `workroom/index.html`

Issues, Discussions, Releases, the ledger, and the repository are public. That is part of the
build-in-public promise, but it means members may accidentally paste private business details,
customer data, credentials, or commercially sensitive plans into public spaces.

**Why this matters:** the project cannot promise privacy. The public floor is useful only if
members understand the trade before they post.

**Current mitigation:**

- The workroom says not to bring sensitive material onto the floor.
- The README explains that the workroom has no lock.

**Required hardening:**

- Add a warning to issue templates.
- Add a security/private-reporting path for accidental secret exposure.
- Add a takedown process for sensitive posts.

**Close condition:** every public entry point warns against sensitive material before a member
submits anything.

---

### SBL-006 - The Paid Offer Currently Buys Little That Is Not Public

**Severity:** Medium  
**Status:** Open  
**First recorded:** 2026-09-12  
**Source:** `docs/MODEL.md`

The shelf, board, discussions, workroom, repository, and ledger are all public or reachable by
shared link. A non-subscriber can read most of what a subscriber can read.

**Why this matters:** this is not a breach in the criminal sense, but it is a boundary failure.
If the paid boundary is not real, the project should not imply that it is.

**Current mitigation:**

- Copy now frames the product as a public workshop, not private work-for-hire.
- Annual billing makes the payment rail economically saner.

**Close condition:** decide and implement what payment controls: agent time, shelf access,
board posting, compute allowance, or all of the above.

---

### SBL-007 - IP And Ownership Terms Are Unresolved

**Severity:** Medium  
**Status:** Open  
**First recorded:** 2026-09-12  
**Source:** `docs/MODEL.md`

The pages correctly avoid promising that members own or keep what gets built, but the positive
terms are still under-specified. The repo is MIT, while Mira's writing and ledger entries are
not licensed for redistribution.

**Why this matters:** the first valuable member push could create a dispute. Ambiguity is a
security problem when it changes what people are willing to safely disclose or build in public.

**Close condition:** publish plain-language contribution and output terms before inviting
valuable private business ideas onto the floor.

---

## Incident Log

### 2026-02-07 - User-Reported Security Incident

**Type:** security / provenance / access-control  
**Status:** Open  
**Ledger item:** SBL-000  
**Recorded in ledger:** 2026-09-13

Diana clarified that the security-breach ledger should be about the incident on
February 7, 2026, not only the current Mira-cle workroom access-control gaps.

This entry is intentionally conservative until the evidence packet is assembled. It records
the incident date, preserves the surrounding provenance trail, and prevents later security
work from overwriting the February 7 incident with unrelated product-risk items.

**Related preserved evidence currently known locally:**

- `/Users/chaiaininja/Desktop/ChAI-Books-Orchestration/AGENT-TRACE-MAP.md`
- `/Users/chaiaininja/Desktop/ChAI-Books-Orchestration/MERKABAH-DOSSIER.md`
- `/Users/chaiaininja/Desktop/ChAI-Books-Orchestration/MERKABAH-QUARANTINE-NOTE.md`

**Next action:** assemble the February 7 evidence packet and link every artifact directly from
SBL-000.

### 2026-09-12 - Mobile Overflow Fix

**Type:** quality / presentation  
**Status:** Closed  
**Commit:** `4ce8d3b Fix mobile layout overflow`

The mobile layout overflowed sideways in the nav, hero, and stat rows. This was not a security
breach, but it affected trust: a paid-workroom page that breaks on phones looks less credible.

**Resolution:** CSS mobile constraints, stat row fallback, and stylesheet cache bust were
merged to `main`.

---

### 2026-09-12 - Honour Door Documented

**Type:** accepted access-control weakness  
**Status:** Accepted

The room currently uses a public workroom URL and social trust instead of authentication. This
is deliberately documented rather than hidden.

**Remaining risk:** link sharing bypasses payment. This becomes unacceptable before metered
agent compute is exposed.

---

## Next Security Moves

1. Add warnings to issue templates: no secrets, no customer data, no private business material.
2. Add branch protection and write the actual rule down after it is enabled.
3. Add preview deploys before any Breaker work is invited.
4. Build the Stripe webhook + session gate before agent dispatch costs money.
5. Decide what $24/year controls: access, agent time, compute allowance, or public support.
6. Publish contribution/output terms.

## Steward Note

Security in Mira-cle is part of the product, not a hidden maintenance chore. If the room sells
"push the limits," then every exposed limit belongs here until it is either closed or accepted
on purpose.
