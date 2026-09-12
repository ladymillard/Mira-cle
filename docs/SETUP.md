# Setup

Everything here is a static site plus one Stripe payment link. There is no build step,
no server, and no database.

## 1. Stripe — point the success URL at the welcome page

This is the one piece of wiring that makes the flow work, and it is done in the Stripe
dashboard, not in this repo.

1. Open the payment link `dRm5kD9zyePCdrD3rDcQU08` in the Stripe dashboard
   (**Payment links → your $2/month link → Edit**).
2. Under **After payment**, choose **Don't show confirmation page → Redirect to your website**.
3. Set the URL to:

   ```
   https://ladymillard.github.io/Mira-cle/welcome.html
   ```

4. Save.

Until you do this, subscribers land on Stripe's generic confirmation page and never see the
workroom door. **This step is required.**

## 2. GitHub Pages

Pages serves from `main` at the repository root. If it ever needs re-enabling:

**Settings → Pages → Source: Deploy from a branch → `main` / `/ (root)`**

Resulting URLs:

| Page | URL |
|---|---|
| Landing | `https://ladymillard.github.io/Mira-cle/` |
| Welcome (post-checkout) | `https://ladymillard.github.io/Mira-cle/welcome.html` |
| Workroom | `https://ladymillard.github.io/Mira-cle/workroom/` |

## 3. Discussions

The workroom's "table" is GitHub Discussions. Enable it at
**Settings → General → Features → Discussions**.

## Changing the price or the link

The Stripe URL appears in `index.html`, `welcome.html`, `workroom/index.html`, `README.md`,
`.github/ISSUE_TEMPLATE/config.yml` and the badge at the top of the README.
To swap it:

```bash
grep -rl 'dRm5kD9zyePCdrD3rDcQU08' . --exclude-dir=.git
```

Then replace it in each file, along with any `$24` / `$2 a month` copy that would become wrong.
Remember the stylesheet version (`mira.css?v=N`) if the CSS changed too.

---

## Upgrade path: a real lock

The current door is an honour-system link — deliberately, and it's stated plainly to members
on the landing page, the welcome page and the README. If the room grows to the point where
that stops being viable, here's the shape of the replacement. None of the existing pages have
to change structurally.

1. **Webhook endpoint.** A small serverless function (Vercel, Netlify, Cloudflare Workers)
   subscribed to `customer.subscription.created`, `.updated`, and `.deleted`.
2. **Store the state.** On each event, upsert `{ email, status, current_period_end }` into a
   database — Supabase is already in reach from the sibling `chai-sol` project.
3. **Issue a session.** The workroom asks for an email, mails a magic link, and checks
   `status === 'active'` before letting the page render.
4. **Keep the honour copy.** Even with a lock, saying out loud how access works is the part
   members actually appreciate.

Cost of the upgrade: one function, one table, one mailer. Not free, but not large either.
The reason it isn't built yet is that at $2 a month the trust is cheaper than the lock —
and if that stops being true, it will be because the room succeeded.
