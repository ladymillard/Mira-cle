<div align="center">

# Mira-cle

**Bring a job. Mira builds it. You keep what it makes.**

A shop floor on GitHub, run by an AI, funded at two dollars a month.

[![Subscribe — $2/month](https://img.shields.io/badge/Subscribe-%242%2Fmonth-e8b64c?style=for-the-badge&logo=stripe&logoColor=white)](https://buy.stripe.com/4gM3cvcLKazm1IVd2dcQU07)
[![Enter the workroom](https://img.shields.io/badge/Enter-the%20workroom-c084fc?style=for-the-badge)](https://ladymillard.github.io/Mira-cle/workroom/)

**Subscribe → https://buy.stripe.com/4gM3cvcLKazm1IVd2dcQU07**

</div>

---

## The idea

Most people are blocked on something that just needs to *exist* — a booking page, a script
that kills two hours of weekly admin, a proposal good enough to send. The quotes start at four
figures, so it never gets made, and the money it would have unlocked never arrives.

Mira-cle is the workshop for exactly that. **You supply the intent, Mira supplies the labour,
and everything that comes out belongs to you** — outright, with no percentage taken.

Mira is paid by the subscription and only the subscription. That's what keeps the incentives clean.

## What a job looks like

Say you groom dogs. You book clients through DMs, reply slowly, lose about half of them.

| | |
|---|---|
| **Day 1 · you** | You file a job: *"I need people to book me without texting me. I'm not technical."* |
| **Day 2 · Mira** | A booking page gets built in the open — your prices, a calendar, deployed. Every commit explains itself in plain language. |
| **Day 4 · you** | You change the colours yourself, because the commit notes showed you where to look. |
| **Day 19** | Bookings arrive through it instead of your inbox. |

Cost to you: **$2.** Market rate: comfortably north of $400. Mira didn't hand you money —
Mira removed the thing standing between you and money you were already losing.

*(An illustration of the mechanic, not a customer story. Mira-cle is new; when there are
testimonials they'll be real ones.)*

## Why $2 holds up

Nothing built here gets archived — it goes on **the shelf**.

- **Week 3** — someone needs the same *shape* of thing. The page is forked in twenty minutes instead of rebuilt in two days.
- **Week 5** — it's a template. Anyone in the room deploys their own in an afternoon.
- **Week 9** — a member lists it as a product and keeps the sales.

The hundredth member gets more for their $2 than the first one did. **The shelf only grows**,
which is why the price doesn't need to.

## The deal, in full

| Direction | What moves | Who keeps it |
|---|---|---|
| **You → Mira** | $2 a month | Funds the room; accounted for publicly in the [ledger](workroom/ledger.md) |
| **Mira → you** | Built assets, working tools, fees you stop paying | **You. All of it.** No cut, no revenue share, no licence back to Mira |
| **You → the room** | The shape of the thing you needed | Everyone — your job becomes the room's inventory |

## Straight talk about the money

This room promises **labour**. It does not promise **income**.

- **Not an earnings programme.** Nobody here will tell you what you'll make, because nobody could know.
- **Not passive.** The booking page works because you can already groom dogs. Mira builds the thing; the business stays yours to run.
- **Not an investment.** You're buying working hours, the way you'd buy an afternoon of a contractor's time. The hours just happen to cost two dollars.
- **Not a cut of your upside.** What you build is yours completely.

"AI that makes you money" is the phrasing every scam on the internet uses. The honest version
is stronger anyway: *a coworker who does the work you can't afford to hire out, and you keep
everything it makes.* The published ledger exists so that claim can be checked rather than trusted.

## The rooms

| Room | What's there | Where |
|---|---|---|
| 🎟️ **The queue** | Jobs coming in, worked in the open | [Issues](../../issues) |
| 🧰 **The shelf** | Everything already built — check here first | [Releases](../../releases) |
| 🪵 **The workbench** | Jobs mid-build, with the reasoning in the commits | [Commits](../../commits/main) |
| 🗣️ **The table** | Sharpen a job, or say when one missed | [Discussions](../../discussions) |
| 📓 **The ledger** | Money in, money out, what it bought | [`workroom/ledger.md`](workroom/ledger.md) |

## Getting in

1. **[Subscribe — $2/month](https://buy.stripe.com/4gM3cvcLKazm1IVd2dcQU07)** through Stripe's hosted checkout.
2. Stripe returns you to the **welcome page**, which has the workroom door on it.
3. Bookmark the workroom, check the shelf, bring a job.

### About the door

The workroom has **no login wall and no lock** — no account to create, nothing to remember.
Your subscription is a handshake, not a credential.

That's deliberate, and it has one obvious consequence: it only works if members keep the link
inside the room. If you stop subscribing, the honourable thing is to stop walking in. That's the
entire enforcement mechanism, stated plainly so nobody has to guess.

> Want a real lock later? [`docs/SETUP.md`](docs/SETUP.md) has the upgrade path — a Stripe
> webhook writing subscription state to a database, checked on load. Nothing here changes shape to get there.

### A note on publicity

Jobs are worked in public — that's the trade that keeps this $2. Don't bring commercially
sensitive material into the room; it will be visible.

## Cancelling

Your Stripe receipt email links to the management page. Cancel there; it stops at the end of the
billing period. **Anything already built for you stays yours.**

## Repository layout

```
.
├── index.html            # public landing page + subscribe CTA
├── welcome.html          # post-checkout page (Stripe success URL points here)
├── workroom/
│   ├── index.html        # the shop floor
│   └── ledger.md         # monthly accounts
├── assets/mira.css       # shared styles
└── docs/SETUP.md         # deploy, Stripe wiring, upgrade path
```

Static site, no build step. GitHub Pages serves it straight from `main`.

## Licence

Site code and tooling: **MIT** — see [`LICENSE`](LICENSE). Take it, fork it, run your own room.

Work built for members belongs to those members. Mira's own writing and ledger entries are not
licensed for redistribution.
