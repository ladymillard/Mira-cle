# The model, thought through

Working document. This is the reasoning behind how Mira-cle runs, including the
parts that don't currently hold up. Written to be argued with.

---

## 1. Why one agent doesn't work

The site currently implies a single AI does everything. That fails on six separate
ceilings, and only the first is about skill:

| Ceiling | What actually happens |
|---|---|
| **Capability** | Frontend, infra, prose, security and review are different jobs. One generalist is mediocre at all of them and knows it about none of them. |
| **Throughput** | One agent is a serial queue. Ten members pushing at once means nine waiting. |
| **Self-review** | An agent reviewing its own diff is the weakest check in software. It shares every blind spot that produced the bug. |
| **Context** | One agent holding the whole project runs out of room and starts forgetting the early decisions — usually the load-bearing ones. |
| **Failure** | One agent stuck is the whole floor stopped. No redundancy, no second opinion. |
| **Cost** | One strong model doing triage, archiving and formatting is paying premium rates for clerical work. |

None of these is fixed by a better prompt. They're fixed by division of labour.

## 2. The team

Six roles. Each earns its place by doing something the others structurally *can't* —
if two roles could be merged without losing a guarantee, they should be.

Per house convention, agents choose their own names. These are stations, not identities.

### Foreperson — *the one you talk to*
Reads your push, decides if it's real, scopes it, routes it, reports back. **Does not build.**
Keeping the coordinator out of the work is what stops it quietly becoming a single agent again.
This is Mira's station.

### Archivist — *owns the shelf and the memory*
Before anything gets built: *has this wall already been hit?* Answers from the shelf.
This is the role that makes "the floor rises" true rather than decorative — without it
the room re-derives the same findings forever and the compounding argument is a lie.
Cheapest model on the team; highest leverage.

### Builder — *writes the code*
Works on a branch, never on main. Builds rough first by default, because the point is
finding the edge, not polish. Can be several in parallel — this is the one role that scales
horizontally.

### Reviewer — *reads the diff cold*
Did not see the build happen and is not told what the Builder intended. That ignorance is the
entire value: it's the only way to catch what the Builder couldn't see. Merging this role into
the Builder destroys the guarantee.

### Breaker — *tries to snap it*
Adversarial. Attacks the preview deploy, not the code — load, malformed input, hostile paths.
On a site whose selling point is "push the limits," this role is the product, not QA overhead.
A limit it finds and documents ships to the shelf as a first-class result.

### Steward — *money and stop conditions*
Meters what each push cost, posts the number on the issue, keeps the ledger, and **kills runs
that exceed budget**. The only role with authority to stop work. Without it, two agents can
ping-pong a fix at $0.40 a round until the month's revenue is gone.

## 3. How a push moves

```
  Push opened on the board (an issue)
        │
  ┌─────▼─────┐
  │ Foreperson│  real? scoped? whose problem?
  └─────┬─────┘
        │ asks
  ┌─────▼─────┐
  │ Archivist │  "wall already mapped in #12 — here's the finding"
  └─────┬─────┘
        ├── known ──► Foreperson closes with the answer.   cost: ~$0
        │
        └── new ───► branch + preview environment opened
                          │
                    ┌─────▼─────┐
                    │  Builder  │  rough, on the branch
                    └─────┬─────┘
                          │
                    ┌─────▼─────┐
                    │  Reviewer │  cold read of the diff
                    └─────┬─────┘
                          │
                    ┌─────▼─────┐
                    │  Breaker  │  attacks the preview
                    └─────┬─────┘
                          │
                  findings ──► back to Builder
                  (bounded: max 3 rounds, then human)
                          │
                    ┌─────▼─────┐
                    │  Steward  │  costs it, posts the number
                    └─────┬─────┘
                          │
                    ┌─────▼─────┐
                    │ Archivist │  writes what was learned to the shelf
                    └─────┬─────┘
                          │
                   member + maintainer decide: merge · park · kill
```

**The bounded loop matters.** Three rounds, then it escalates to a human. Unbounded agent
loops are how you turn a $2 subscription into a $60 API bill overnight.

## 4. What makes it a team rather than costumes

Four things. Without all four it's one agent wearing hats:

1. **Separation of knowledge.** The Reviewer genuinely does not see the Builder's reasoning.
   Enforced by what gets passed, not by instructions.
2. **Typed handoffs.** Each station's output is a structured comment the next station parses —
   verdict, findings, cost, artefacts. Prose-to-prose handoffs degrade every hop.
3. **Shared state in the open.** The issue is the working memory. Any agent, and any member,
   can read the whole history of a push.
4. **One authority to stop.** The Steward. Everything else can only advance work.

## 5. Isolation — mandatory, not optional

Members are explicitly invited to break things. So:

- Every push gets its **own branch and its own preview deploy**.
- The Breaker attacks the preview. Never production.
- `main` is protected. Merges are a human decision.

The current setup has none of this. The first genuine "break it" push would take the live
site down, which would be an entirely self-inflicted wound.

---

## 6. Three things that don't currently hold up

These are model problems, not copy problems. They need decisions.

### 6.1 The $2 buys nothing that isn't already free

The repo is public. The workroom is a public GitHub Pages URL with `noindex` and no lock.
Issues, Discussions and Releases are all public. **A non-subscriber gets everything a
subscriber gets**, so the subscription is a donation with extra steps.

The fix is to be clear about what is actually scarce. It isn't files — it's **the team's
working time**. Reading the shelf can stay free (it's good marketing and costs nothing to
serve). Putting work on the board and having six agents run it is the thing that costs real
money, and that's the thing $2 should buy.

That reframes the product honestly: **you're not buying access to a folder, you're buying a
crew.** But it forces 6.2.

### 6.2 The honour-system door can't survive metered compute

An honour system is fine for guarding documents. It is not fine for guarding a button that
spends money on an API. Once $2 buys agent time, unverified access means anyone can burn the
room's budget.

So the webhook-and-database path in [`SETUP.md`](SETUP.md) stops being a "later" upgrade and
becomes a prerequisite. Stripe webhook → subscription status → the board checks it before
dispatching any agent.

### 6.3 The economics half-close — annual billing is now live

**Fixed as of the move to annual billing.** Per member, per year:

| Line | Monthly ($2 × 12) | Annual ($24 × 1) |
|---|---|---|
| Gross | $24.00 | $24.00 |
| Stripe fees (2.9% + $0.30 per charge) | −$4.30 | **−$1.00** |
| **Net to the floor** | **$19.70** | **$23.00** |
| Effective fee rate | 17.9% | **4.1%** |

Twelve charges means paying the flat 30¢ twelve times. One charge pays it once. Identical price
to the member, **$3.30 more per member per year** on the floor — and at a $2 price point that
flat fee is the dominant cost, not the percentage.

**Still open: compute.** Annual billing fixes the payment rail, not the burn. Against $1.92 per
member per month, a single push across six stations costs somewhere between $0.50 and $10 in
tokens depending on models and rounds. One active member can still outcost ten paying ones, and
**the model still loses money faster the better it works.**

The Steward exists to make this visible and stoppable, but metering is not the same as solving.
The real fix is separating the floor from the fuel: $2/month funds the shelf, the board, the
orchestration and the site; agent compute is either a metered allowance with bring-your-own-key
past it, or BYO-key from the start. Until that lands, treat heavy usage as deliberately
subsidised and say so plainly rather than discovering it in a bill.

### 6.4 Two things the copy may not claim

Standing constraint on all member-facing writing:

1. **Never say members keep or own what gets built.** No "yours to keep," no "no cut, no
   revenue share," no "sell it under your own name."
2. **Never say the agents build *with* the member.** No "alongside Mira," no "you and Mira,"
   no describing an agent as the member's collaborator or pair.

Both were removed from every page on 2026-09-12. `AGENTS.md` carries the rule so it doesn't
creep back in.

**What this costs, stated honestly.** Those two claims were doing most of the work in the
answer to *why would anyone pay?* Stripping them leaves the offer as: a seat inside a
build-in-public project about making AI collaboration practical, plus the shelf it accumulates.
That is true and defensible, but it is a **weaker commercial hook** than ownership was, and the
copy currently leans on curiosity rather than on gain.

Two consequences to decide on:

- **The IP position is now unstated rather than resolved.** The repo is MIT and the floor is
  public, which is what the pages now say. But what happens when a member pushes something
  genuinely valuable is not written down anywhere. Silence is fine while the room is small and
  becomes a dispute the first time it isn't.
- **The reason to subscribe needs to be re-established.** If it isn't ownership and isn't a
  private collaborator, it is access and visibility — which argues for making the shelf
  members-only (open decision 3) so the subscription buys something that can't be read for free.

## 7. Open decisions

1. **What does $2 actually buy** — the floor only (compute BYO), or a metered allowance?
   This is now the binding constraint; annual billing bought headroom, not a solution.
2. ~~**Monthly, annual, or both?**~~ **Decided: annual, $24/year.** Fees drop 17.9% → 4.1%.
3. **Does the shelf stay public** (marketing, and the compounding argument is visible) or go
   members-only (weaker argument, stronger reason to pay)? **Now more pressing** — with the
   ownership claim gone, access is most of what's left to sell.
4. **How many Builders run in parallel**, and does a member pick their crew or does the
   Foreperson route it?
5. **What is the actual IP position** when a member pushes something valuable? Currently
   unstated — see 6.4.
