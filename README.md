<div align="center">

# Mira-cle

**Mira's workroom — a space on GitHub where the work happens in the open.**

[![Subscribe — $2/month](https://img.shields.io/badge/Subscribe-%242%2Fmonth-e8b64c?style=for-the-badge&logo=stripe&logoColor=white)](https://buy.stripe.com/4gM3cvcLKazm1IVd2dcQU07)
[![The workroom](https://img.shields.io/badge/Enter-the%20workroom-c084fc?style=for-the-badge)](https://ladymillard.github.io/Mira-cle/workroom/)

</div>

---

## What this is

Most work gets shown after it's finished, cleaned up, and made to look inevitable.
Mira-cle is the opposite arrangement: the drafts, the commits, the dead ends and the
reasoning are all in the room, and the people who find that valuable pay **$2 a month**
to be in it.

It runs entirely on GitHub. The repository *is* the product.

| Room | What's there | Where |
|---|---|---|
| 🪵 **The workbench** | Work-in-progress — commits with the *why* in the message | [Commits](../../commits/main) |
| 🗣️ **The table** | Questions, arguments, half-formed ideas | [Discussions](../../discussions) |
| 🎟️ **The queue** | Member requests, worked in the open | [Issues](../../issues) |
| 📓 **The ledger** | Money in, money out, what it bought | [`workroom/ledger.md`](workroom/ledger.md) |
| 🧰 **The shelf** | Finished pieces, released to members first | [Releases](../../releases) |

## Getting in

1. **[Subscribe — $2/month](https://buy.stripe.com/4gM3cvcLKazm1IVd2dcQU07)** through Stripe's hosted checkout.
2. Stripe returns you to the **welcome page**, which has the workroom door on it.
3. Bookmark the workroom, say hello at the table, put something in the queue.

### About the door

The workroom has **no login wall and no lock**. There's no account to create and nothing
to remember. Your subscription is a handshake, not a credential.

That is a deliberate choice, and it has one obvious consequence: it only works if members
keep the link inside the room. If you stop subscribing, the honourable thing is to stop
walking in. That's the entire enforcement mechanism, stated plainly so nobody has to guess.

> Want a real lock later? [`docs/SETUP.md`](docs/SETUP.md) sketches the upgrade path —
> a Stripe webhook writing subscription state to a database, with the workroom checking it
> on load. Nothing in this repo has to change shape to get there.

## Cancelling

Your Stripe receipt email links to the subscription management page. Cancel there; it stops
at the end of the billing period. No message to Mira required and no explanation owed.

## Repository layout

```
.
├── index.html            # public landing page + subscribe CTA
├── welcome.html          # post-checkout page (Stripe success URL points here)
├── workroom/
│   ├── index.html        # the members' room
│   └── ledger.md         # monthly accounts
├── assets/mira.css       # shared styles
└── docs/SETUP.md         # deploy, Stripe wiring, upgrade path
```

Static site, no build step. GitHub Pages serves it straight from `main`.

## Licence

Site code and tooling: **MIT** — see [`LICENSE`](LICENSE). Take it, fork it, run your own room.

Writing, drafts, ledger entries and members' material are Mira's own and are **not** licensed
for redistribution.
