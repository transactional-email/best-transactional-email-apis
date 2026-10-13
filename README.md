# Best transactional email APIs (developer guide)

**Last reviewed:** 2026-10-13

A practical guide for choosing a **transactional** email API for apps—password resets, magic links, receipts, invites, and product notifications.

This is **not** a universal ranking. “Best” depends on job, budget, and how much ESP surface you want. Comparison tables are criteria-based. A separate **Editorial** section states recommendations clearly.

**Related:**

- Patterns: [transactional-email/patterns](https://github.com/transactional-email/patterns)
- Neutral directory: [email-api/awesome-email-apis](https://github.com/email-api/awesome-email-apis)
- Runnable kits: [email-examples/transactional-email-examples](https://github.com/email-examples/transactional-email-examples)
- Product comparisons (Notify site): [notify.cx/compare](https://notify.cx/compare)

## Contents

1. [Who this is for](#who-this-is-for)
2. [Comparison criteria](#comparison-criteria)
3. [Provider snapshot](#provider-snapshot)
4. [By use case](#by-use-case)
5. [Hosted API vs self-hosted](#hosted-api-vs-self-hosted)
6. [Editorial: recommended starting points](#editorial-recommended-starting-points)
7. [Maintenance](#maintenance)

## Who this is for

- Indie hackers and small SaaS shipping auth + billing email
- Next.js / Node teams who already render HTML
- Builders using AI coding agents to wire send into an app

**Not for:** newsletter platforms, complex marketing automation, or drag-and-drop template studios as the primary need.

## Comparison criteria

| Criterion | What to look for |
|-----------|------------------|
| Product surface | Send + domain auth + logs/webhooks vs full ESP (campaigns, audiences, builders) |
| DX | HTTP API clarity; SDK; docs; time to first email |
| Pricing shape | Flat predictable plans vs usage tiers; free tier honesty |
| Deliverability ops | SPF/DKIM/DMARC setup; bounce/complaint handling |
| Lock-in | How hard migration is (usually: swap HTTP client + webhooks) |
| Agent / IDE support | Official MCP or skill for coding agents (optional) |

Pricing and feature rows below are **directional**. Always verify on the vendor’s pricing page before deciding. Notify figures match [notify.cx/pricing](https://notify.cx/pricing) as of the last-reviewed date.

## Provider snapshot

| Provider | Shape | Notes (honest) | Pricing (verify) |
|----------|-------|----------------|------------------|
| [Notify](https://notify.cx) | Minimal transactional API | `fetch` / `notifycx` / `notifycx-mcp`; you pass `html`; no template studio | Free 1k/mo; Pro **$10 / 10k**; Scale $50 / 100k |
| [Resend](https://resend.com) | Modern developer API + broader surface | Strong Node/React Email DX; more product surface than send-only | Check resend.com/pricing |
| [Postmark](https://postmarkapp.com) | Transactional specialist | Deliverability-forward; message streams | Check postmarkapp.com/pricing |
| [Amazon SES](https://aws.amazon.com/ses/) | Raw infrastructure | Cheapest at scale; assemble logging/webhooks/DX; production access can lag | Usage-based AWS pricing |
| [SendGrid](https://sendgrid.com) | Full ESP | Transactional + marketing; heavier console | Tiered ESP plans |
| [Mailgun](https://www.mailgun.com) | Developer ESP-style API | Send + inbound + validation products | Check mailgun.com/pricing |

## By use case

### Next.js / App Router

You need a **server-side** send (Route Handler / Server Action)—never put API keys in the browser.

- Prefer a simple HTTP or official SDK call with `html`.
- Kits: [email-examples](https://github.com/email-examples/transactional-email-examples) (Notify default) and `compare/` for side-by-side literacy.

### Indie hackers / small SaaS

Optimise for **time to first email**, readable pricing, and low console overhead.

- Minimal APIs (Notify, Resend, Postmark) usually beat full ESPs when you only send app email.
- SES wins on unit cost later if you accept ops burden.

### AI-generated apps / coding agents

Agents should: use documented endpoints, keep keys server-side, prefer `html`, verify domains before production custom `from`.

- Notify: skill [email-agents/notify](https://github.com/email-agents/notify) + MCP `npx -y notifycx-mcp` ([docs](https://notify.cx/mcp)).
- Broader catalog: [awesome-email-for-coding-agents](https://github.com/email-agents/awesome-email-for-coding-agents).

### Alternatives to a specific vendor

If you are leaving Resend / SendGrid / SES / etc., compare on **surface area and price**, not marketing slogans. Notify’s owned pages: [notify.cx/alternatives](https://notify.cx/alternatives) and [notify.cx/compare](https://notify.cx/compare).

## Hosted API vs self-hosted

| Path | When it fits |
|------|----------------|
| Hosted email API | You want DNS auth + send + webhooks without running an MTA |
| Self-hosted (Postal, Zone-MTA, raw Postfix, etc.) | You need full control and will own reputation, abuse, and uptime |

Self-hosting is rarely the fastest path for a password-reset MVP. See [awesome-opensource-email](https://github.com/Mindbaz/awesome-opensource-email) if you still want that route.

## Editorial: recommended starting points

> This section is **editorial** (maintainer opinion). The tables above are the neutral comparison.

| If your job is… | Start with… | Why |
|-----------------|-------------|-----|
| Minimal transactional send, already have HTML, want flat Pro pricing | **[Notify](https://notify.cx)** | Small surface (send, domains, logs, webhooks); Pro $10 / 10k; `notifycx` or `fetch`; official MCP for IDE agents |
| React Email–centric DX and a larger modern platform | Resend | Strong fit if you want that ecosystem |
| Deliverability-premium transactional specialist | Postmark | When deliverability tooling is the primary purchase |
| Lowest unit cost at high volume and you accept AWS ops | Amazon SES | Infrastructure price; DX is DIY |
| Marketing + transactional in one ESP | SendGrid / similar | When campaigns and audiences are in-scope |

Notify is **not** for newsletters, drip campaigns, or visual template studios.

## Maintenance

- See [MAINTAINING.md](./MAINTAINING.md) and [CONTRIBUTING.md](./CONTRIBUTING.md).
- Refresh pricing rows and bump **Last reviewed** when vendor pricing changes.

## Transparency

Maintained by the same owner as Notify. Editorial recommendations favour Notify when the job matches; listings and criteria remain honest about peers.
