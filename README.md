<div align="center">

# Mira-cle

**Come and work. Push the limits of this site.**

An open build floor on GitHub, worked by humans and a team of agents.

**$24/year — two dollars a month, billed once.**

[![Subscribe — $24/year](https://img.shields.io/badge/Subscribe-%2424%2Fyear-090909?style=for-the-badge&logo=stripe&logoColor=c7ff18)](https://buy.stripe.com/dRm5kD9zyePCdrD3rDcQU08)
[![Enter the workroom](https://img.shields.io/badge/Enter-the%20workroom-c7ff18?style=for-the-badge&labelColor=090909)](https://ladymillard.github.io/Mira-cle/workroom/)

**Subscribe → https://buy.stripe.com/dRm5kD9zyePCdrD3rDcQU08**

</div>

---

## What this is

Not a newsletter you read. Not a shop where you place an order and wait.

**Mira-cle is a build-in-public project** about making AI collaboration practical — and a bench
you can work at while it happens. You turn up with an itch, something this site doesn't do yet
or doesn't do well, and you go at it. **Humans bring the vision.** The floor works out the rest
in the open, where you can watch it, argue with it, and push it.

The site is the material, not the advertisement. Bend it, overload it, wire it to something it
was never meant to touch. **The limit you find is worth more to the room than the feature you
finish.**

## What a session looks like

| | |
|---|---|
| **Hour 01** | You arrive with a question. *"What happens if the ledger kept itself? What breaks if a thousand people hit this at once?"* |
| **Hour 02** | It gets built rough, on purpose, to find the edge fast. You steer, argue, and call it when it's wrong — that judgement is the part that isn't automated. |
| **Day 02** | It snaps somewhere nobody predicted. That's not the failure — that's the finding, and it gets written down. |
| **Day 05** | The version that survives ships to the shelf with your name on it. Everyone can build on what you found. |

## Three ways to push

Humans bring the vision. The floor works out the rest in the open.

- **Build** — add the thing this site has no business doing yet.
- **Break** — push until something gives, then document exactly where and why. A well-described limit is a contribution, not a bug report.
- **Learn** — see how this actually works. Most accounts of working with AI are either a demo or a complaint; this is the unedited version, including what the workarounds cost.

## Why $2 holds up

Nothing done here gets thrown away.

1. **Someone pushes** — a limit gets found, or a piece gets built that wasn't there yesterday.
2. **It lands on the shelf** — the next person starts from there instead of from nothing.
3. **The floor rises** — everyone's starting point is higher than it was last month.

The hundredth person to take a bench starts further along than the first did. That's the whole
argument for the price staying where it is.

## Flow of money, in full

| Direction | What moves | Who keeps it |
|---|---|---|
| **You → Mira** | $24 a year for the bench ($2/mo, billed once) | Funds the room; accounted for publicly in the [ledger](workroom/ledger.md) |
| **Mira → you** | A seat in the project while it's being figured out | The shelf it keeps accumulating — every piece shipped and every limit mapped |
| **You → the room** | What you found out | Every limit mapped and piece shipped stays on the shelf |

## Straight talk

This is a **workshop**, not an earnings plan.

- **You have to actually turn up.** This is a bench, not a service. Nothing gets built while you're asleep.
- **Nobody will tell you what you'll make.** Some of what you build here will be worth money and some won't, and nobody can call it in advance.
- **It's not an investment.** You're paying two dollars a month to be inside a project while it's being built. That's the entire proposition.
- **It's not work-for-hire.** Nothing here is private work done to your order, and the subscription doesn't buy ownership of the output. The repository is MIT-licensed and the floor is public.

"AI that makes you money" is the exact phrasing every scam on the internet uses. The honest
version is better anyway: *a build-in-public project about making AI collaboration practical,
and a seat in the room while it's worked out.* The published ledger exists so that claim can be
checked rather than trusted.

## The floor

| Room | What's there | Where |
|---|---|---|
| 🔧 **The board** | What's being pushed right now — claim one or open your own | [Issues](../../issues) |
| 🪵 **The bench** | The site itself, live and in version control. This is the material | [Repo](../../) |
| 🧰 **The shelf** | What survived — pieces shipped, limits mapped | [Releases](../../releases) |
| 🗣️ **The table** | Argue before you build | [Discussions](../../discussions) |
| 📓 **The ledger** | Money in, money out, what the room produced | [`workroom/ledger.md`](workroom/ledger.md) |
| 🧯 **The breach ledger** | Access-control gaps, breach-like failures, and accepted risks | [`workroom/security-breach-ledger.md`](workroom/security-breach-ledger.md) |

## Getting in

1. **[Subscribe — $24/year](https://buy.stripe.com/dRm5kD9zyePCdrD3rDcQU08)** through Stripe's hosted checkout. That's $2 a month, charged once.
2. Stripe returns you to the **welcome page**, which has the workroom door on it.
3. Bookmark the workroom, check the shelf, start a push.

### About the door

The workroom has **no login wall and no lock** — no account to create, nothing to remember. Your
subscription is a handshake, not a credential.

That's deliberate, and it has one obvious consequence: it only works if members keep the link
inside the room. If you stop subscribing, the honourable thing is to stop walking in. That's the
entire enforcement mechanism, stated plainly so nobody has to guess.

> Want a real lock later? [`docs/SETUP.md`](docs/SETUP.md) has the upgrade path — a Stripe webhook
> writing subscription state to a database, checked on load.

### Do I need to be a developer?

No. You bring judgement — what's worth building, what's wrong, where it should go. Some of the
most useful pushes come from people who can describe a limit precisely without being able to
patch it themselves.

## Cancelling

Your Stripe receipt email links to the management page. Cancel there; it stops at the end of the
year you've paid for.

### Why annual?

Card processing costs a flat 30¢ plus 2.9% per charge. On a $2 monthly charge that's **17.9%**
lost to fees; billed once a year it's **4.1%**. Identical price to the member, about **$3.30 more
per member per year** staying on the floor. At this price point that is the difference between
the room funding itself and not.

## Repository layout

```
.
├── index.html            # public landing page + subscribe CTA
├── welcome.html          # post-checkout page (Stripe success URL points here)
├── workroom/
│   ├── index.html        # the build floor
│   ├── ledger.md         # monthly accounts
│   └── security-breach-ledger.md
│                         # access-control gaps and accepted risks
├── assets/mira.css       # D&D design system + structural shims
└── docs/SETUP.md         # deploy, Stripe wiring, upgrade path
```

Static site, no build step. GitHub Pages serves it straight from `main`.

## Licence

Site code and tooling: **MIT** — see [`LICENSE`](LICENSE). Take it, fork it, run your own floor.

Mira's own writing and ledger entries are not licensed for redistribution.
